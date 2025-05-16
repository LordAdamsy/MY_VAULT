


以下是 C++ 中常见的会导致程序崩溃的代码写法及其原理分析，涵盖内存管理、指针操作、多线程等问题：

---

### 0.1.1 **一、内存管理错误**
#### 0.1.1.1 **空指针解引用**
```cpp
int* ptr = nullptr;
*ptr = 42; // 崩溃：访问空指针
```

#### 0.1.1.2 **野指针（悬垂指针）**
```cpp
int* ptr = new int(10);
delete ptr;
*ptr = 20; // 崩溃：访问已释放内存
```

#### 0.1.1.3 **双重释放（Double Free）**
```cpp
int* ptr = new int;
delete ptr;
delete ptr; // 崩溃：重复释放同一内存
```

#### 0.1.1.4 **内存泄漏导致资源耗尽**
```cpp
while (true) {
    int* ptr = new int[1000000]; // 最终因内存耗尽崩溃
}
```

#### 0.1.1.5 **堆溢出（Heap Overflow）**
```cpp
char* buffer = new char[10];
memset(buffer, 'A', 20); // 崩溃：写入越界破坏堆结构
delete[] buffer;
```

---

### 0.1.2 **二、数组与缓冲区问题**
#### 0.1.2.1 **数组越界访问**
```cpp
int arr[5] = {0};
arr[5] = 10; // 崩溃：越界访问（栈损坏）
```

#### 0.1.2.2 **栈溢出（Stack Overflow）**
```cpp
void infinite_recursion() {
    int data[1000]; // 大局部变量加速栈溢出
    infinite_recursion();
}
infinite_recursion(); // 崩溃：栈空间耗尽
```

#### 0.1.2.3 **使用未初始化的指针**
```cpp
int* ptr;
*ptr = 5; // 崩溃：指针指向随机地址
```

---

### 0.1.3 **三、多线程问题**
#### 0.1.3.1 **数据竞争（Data Race）**
```cpp
int counter = 0;
void increment() { for (int i=0; i<1000000; ++i) ++counter; }

std::thread t1(increment);
std::thread t2(increment);
t1.join(); t2.join();
// 崩溃：未同步的竞争写操作（可能破坏内存）
```

#### 0.1.3.2 **析构后访问共享资源**
```cpp
std::vector<int>* vec = new std::vector<int>;
std::thread t([&] {
    vec->push_back(42); // 崩溃：若主线程先delete
});
delete vec;
t.join();
```

---

### 0.1.4 **四、未定义行为（UB）**
#### 0.1.4.1 **类型转换错误**
```cpp
float* f = new float(3.14f);
int* i = reinterpret_cast<int*>(f);
*i = 0; // 崩溃：违反严格别名规则（取决于编译器）
```

#### 0.1.4.2 **虚函数表损坏**
```cpp
class Base { public: virtual void foo() {} };
class Derived : public Base {};

Base* b = new Base;
Derived* d = static_cast<Derived*>(b);
d->foo(); // 崩溃：错误转型导致虚表指针无效
```

#### 0.1.4.3 **违反严格别名规则**
```cpp
int a = 10;
float* b = reinterpret_cast<float*>(&a);
*b = 20.0f; // 崩溃：通过不兼容类型访问内存
```

---

### 0.1.5 **五、资源管理错误**
#### 0.1.5.1 **文件操作后未关闭**
```cpp
for (int i=0; ; ++i) {
    FILE* f = fopen("test.txt", "w"); // 最终因句柄耗尽崩溃
}
```

#### 0.1.5.2 **智能指针的循环引用**
```cpp
struct Node {
    std::shared_ptr<Node> next;
};
auto n1 = std::make_shared<Node>();
auto n2 = std::make_shared<Node>();
n1->next = n2;
n2->next = n1; // 内存泄漏（但不会直接崩溃）
```

---

### 0.1.6 **六、其他致命操作**
#### 0.1.6.1 **调用纯虚函数**
```cpp
class Base { public: virtual void foo() = 0; };
class Derived : public Base { public: void foo() override {} };

Base* b = new Derived;
delete b;
b->foo(); // 崩溃：对象已销毁，虚表无效
```

#### 0.1.6.2 **非法指令执行**
```cpp
void (*func)() = reinterpret_cast<void(*)()>(0xDEADBEEF);
func(); // 崩溃：跳转到非法地址
```

#### 0.1.6.3 **修改字符串字面量**
```cpp
char* str = "read-only";
str[0] = 'W'; // 崩溃：写入只读内存段
```

#### 0.1.6.4 **Lambda 捕获悬空引用**
```cpp
std::function<void()> func;
{
    int x = 10;
    func = [&x]() { std::cout << x; }; // x 已销毁
}
func(); // 崩溃：悬空引用
```

#### 0.1.6.5 **使用已销毁的临时对象**
```cpp
const std::string& s = std::string("hello");
std::cout << s; // 崩溃：临时对象已销毁（未延长生命周期）
```

---

### 0.1.7 **总结**
| **崩溃类型**         | **示例数量** | **典型场景**                  |
|----------------------|-------------|------------------------------|
| 内存管理错误          | 5           | 空指针、双重释放、堆溢出       |
| 数组与缓冲区问题      | 3           | 越界、栈溢出、未初始化指针     |
| 多线程问题            | 2           | 数据竞争、析构后访问           |
| 未定义行为            | 3           | 类型转换、虚表损坏、严格别名   |
| 资源管理错误          | 2           | 句柄泄漏、循环引用             |
| 其他致命操作          | 5           | 非法指令、修改字面量、悬空引用 |

**注意事项**：
- 部分崩溃行为依赖操作系统和编译器（如栈溢出大小阈值）。
- 未定义行为可能导致不可预测结果（不一定是崩溃）。
- 实际开发中应使用工具（如 AddressSanitizer、Valgrind）检测此类问题。