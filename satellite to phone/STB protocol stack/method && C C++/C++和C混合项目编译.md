C++支持函数重载，在编译时会对函数重命名；而C语言不支持重载，因此混合项目中cpp的函数在链接时会无法找到从而报错

**解决方法：**
在C++文件对应的头文件中，对声明的函数使用`extern "C"`关键字，使其以C语言的方式处理

```cpp
#ifndef RECV_FRAME_H
#define RECV_FRAME_H 

#ifdef __cplusplus
extern "C" void recv_frame(int i);
#else
void recv_frame(int i);
#endif 

#endif
```
