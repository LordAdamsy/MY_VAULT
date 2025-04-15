

以下是SystemVerilog核心数据类型与语法的结构化总结：

---

### 0.1.1 一、**基本数据类型**
#### 0.1.1.1 **二值逻辑（1-bit）**
   - `bit`：二值逻辑（0/1），默认初始值为0
   - `byte`：8位有符号整数（-128~127）
   - `shortint`：16位有符号整数
   - `int`：32位有符号整数
   - `longint`：64位有符号整数

#### 0.1.1.2 **四值逻辑（4-state）**
   - `logic`：四值逻辑（0/1/X/Z），替代`reg`和`wire`
   - `integer`：32位四值有符号整数
   - `time`：64位无符号整数（仿真时间）

#### 0.1.1.3 **其他类型**
   - `real`：双精度浮点数
   - `shortreal`：单精度浮点数
   - `string`：动态字符串（支持操作如`len()`, `substr()`）

---

### 0.1.2 二、**复合数据类型**
#### 0.1.2.1 **定宽数组**
   ```systemverilog
   int arr1[0:7];        // 8元素数组（索引0~7）
   logic [3:0] arr2[4];  // 4个4-bit元素
   ```

#### 0.1.2.2 **动态数组**
   ```systemverilog
   int dyn_arr[];         // 声明
   dyn_arr = new[5];      // 分配5元素空间
   ```

#### 0.1.2.3 **关联数组**
   ```systemverilog
   bit [7:0] assoc_arr[string];  // 字符串索引
   assoc_arr["key"] = 8'hFF;     // 赋值
   ```

#### 0.1.2.4 **队列（Queue）**
   ```systemverilog
   int q[$] = {1,2,3};   // 声明并初始化
   q.push_back(4);       // 插入尾部 → {1,2,3,4}
   ```

#### 0.1.2.5 **结构体（Struct）**
   ```systemverilog
   typedef struct {
       bit [31:0] addr;
       logic [7:0] data;
   } Packet;
   Packet pkt;           // 实例化
   ```

#### 0.1.2.6 **枚举（Enum）**
   ```systemverilog
   enum {IDLE, START, DATA} state;  // 默认0,1,2
   enum logic [1:0] {RED=2'b01, GREEN=2'b10} color;
   ```

---

### 0.1.3 三、**关键语法**
#### 0.1.3.1 **模块定义**
   ```systemverilog
   module MyModule #(
       parameter WIDTH = 8
   ) (
       input  logic clk,
       output logic [WIDTH-1:0] out
   );
   endmodule
   ```

#### 0.1.3.2 **过程块**
   - **Always块**：
     ```systemverilog
     always_comb begin    // 组合逻辑
         y = a & b;
     end

     always_ff @(posedge clk) begin  // 时序逻辑
         q <= d;
     end
     ```

   - **Initial块**（仅仿真）：
     ```systemverilog
     initial begin
         #10;  // 延迟10时间单位
         $display("Simulation start");
     end
     ```

#### 0.1.3.3 **控制结构**
   - **条件语句**：
     ```systemverilog
     unique if (a > b) begin  // unique确保互斥
         // 分支1
     end else if (a == b) begin
         // 分支2
     end else begin
         // 默认分支
     end
     ```

   - **循环**：
     ```systemverilog
     for (int i=0; i<8; i++) begin
         arr[i] = i;
     end

     foreach (arr[j]) begin  // 自动遍历数组
         $display(arr[j]);
     end
     ```

#### 0.1.3.4 **任务与函数**
   ```systemverilog
   function automatic int add(input int a, b);
       return a + b;
   endfunction

   task send_packet(ref Packet pkt);
       // 任务代码（可包含时序控制）
   endtask
   ```

#### 0.1.3.5 **接口（Interface）**
   ```systemverilog
   interface BusIf;
       logic [31:0] addr;
       logic [7:0]  data;
       modport Master (output addr, input data);
   endinterface

   module Top;
       BusIf bus();  // 实例化接口
       Master u_master(.bus(bus));
   endmodule
   ```

#### 0.1.3.6 **断言（Assertion）**
   ```systemverilog
   assert property (@(posedge clk) 
       a |-> ##1 b  // a为真时，下一周期b必须为真
   ) else $error("Assertion failed");
   ```

---

### 0.1.4 四、**关键特性对比**
| **特性**          | **Verilog**              | **SystemVerilog**              |
|--------------------|--------------------------|---------------------------------|
| 数据类型           | 基础类型（reg/wire）     | 增强类型（logic, struct, enum）|
| 数组               | 定宽数组                 | 动态数组/关联数组/队列         |
| 过程块             | always/initial           | always_comb/always_ff/always_latch |
| 接口               | 无                       | 支持接口（interface）          |
| 面向对象           | 不支持                   | 支持类（class）和继承           |

---

### 0.1.5 五、**最佳实践**
1. **优先使用`logic`**：替代`reg`和`wire`，简化设计
2. **明确过程块类型**：用`always_comb`/`always_ff`替代通用`always`
3. **利用接口封装**：减少模块间连线复杂度
4. **使用枚举代替宏**：增强代码可读性和类型安全