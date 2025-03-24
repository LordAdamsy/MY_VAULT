

在 Verilog 中，`parameter` 的作用域默认是**模块内局部**的，无法直接跨模块访问。所谓“跨模块使用 `parameter`”，通常是指通过以下两种方式实现参数在多个模块间的传递或共享：

---

### **1. 通过模块实例化传递参数**
在实例化子模块时，可以通过**参数重载**（Parameter Override）将父模块的 `parameter` 值传递给子模块。这是最常见的跨模块参数传递方式。

#### **示例**
```verilog
// 子模块（定义参数）
module SubModule #(
  parameter WIDTH = 8  // 默认值
) (
  input  [WIDTH-1:0] data_in,
  output [WIDTH-1:0] data_out
);
  // 子模块逻辑
endmodule

// 父模块（传递参数给子模块）
module TopModule;
  // 定义父模块的参数
  parameter PARENT_WIDTH = 16;

  // 实例化子模块，并传递参数
  SubModule #(
    .WIDTH(PARENT_WIDTH)  // 将父模块的 PARENT_WIDTH 传递给子模块的 WIDTH
  ) u_sub (
    .data_in ( ... ),
    .data_out( ... )
  );
endmodule
```

#### **关键点**：
- 子模块通过 `#(parameter ...)` 定义可配置参数。
- 父模块在实例化子模块时，通过 `#(.PARAM_NAME(VALUE))` 语法重载子模块参数。
- 参数值可以是父模块自身的 `parameter`、`localparam` 或直接常量。

---

### **2. 通过 `define 宏定义全局常量**
若需要多个模块共享同一常量，可使用 `` `define`` 定义全局宏，但需注意其与 `parameter` 的区别。

#### **示例**
```verilog
// 在头文件（如 defines.vh）中定义全局宏
`define GLOBAL_WIDTH 32

// 模块A
module ModuleA;
  reg [`GLOBAL_WIDTH-1:0] data;  // 使用宏
endmodule

// 模块B
module ModuleB;
  wire [`GLOBAL_WIDTH-1:0] result;  // 使用同一宏
endmodule
```

#### **`define` vs `parameter`**
| 特性                | `define` (宏)               | `parameter`               |
|---------------------|----------------------------|---------------------------|
| **作用域**           | 全局（需通过 `include 包含）| 模块内局部                |
| **可重载性**         | 不可重载                   | 可在实例化时重载          |
| **类型安全**         | 无（纯文本替换）           | 支持类型（如整数、实数）  |
| **推荐用途**         | 全局常量、代码模板         | 模块级参数化配置          |

---

### **3. 常见问题与错误**

#### **(1) 错误：直接跨模块引用 `parameter`**
```verilog
module ModuleA;
  parameter WIDTH = 8;
endmodule

module ModuleB;
  reg [ModuleA.WIDTH-1:0] data;  // 错误！无法直接访问其他模块的 parameter
endmodule
```
**解决**：通过实例化传递参数或使用 `define` 宏。

#### **(2) 参数传递类型不匹配**
```verilog
module SubModule #(parameter WIDTH = 8) (...);
  // ...
endmodule

module TopModule;
  SubModule #(.WIDTH("16")) u_sub (...);  // 错误！"16" 是字符串，非整数
endmodule
```
**解决**：确保传递的值类型与参数定义一致。

#### **(3) 多层参数传递**
```verilog
module Grandchild #(parameter SIZE = 4) (...);
  // ...
endmodule

module Child #(parameter CHILD_SIZE = 8) (...);
  Grandchild #(.SIZE(CHILD_SIZE)) u_grandchild (...);  // 将参数传递给孙子模块
endmodule

module Top;
  Child #(.CHILD_SIZE(16)) u_child (...);  // 参数从 Top -> Child -> Grandchild
endmodule
```

---

### **4. 总结**
- **`parameter` 跨模块使用**的本质是通过**实例化时的参数传递**或**全局宏定义**实现。
- **优先使用 `parameter`**：适合模块化设计，支持重载，类型安全。
- **慎用 `define`**：适合全局常量，但需注意命名冲突和可维护性。
- **典型场景**：
  - 数据总线宽度、存储器深度等模块级配置 → `parameter`。
  - 全局时钟周期、调试标志 → `define`。