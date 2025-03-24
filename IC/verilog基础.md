

Verilog 是一种硬件描述语言（HDL），主要用于数字电路的设计、仿真和综合。其代码结构围绕**模块（Module）**展开，每个模块代表一个具有特定功能的硬件组件。以下是 Verilog 的基本代码结构和核心概念：

---

### **1. 基本代码结构**
#### **(1) 模块定义**
模块是 Verilog 的基本单元，通过 `module` 和 `endmodule` 定义，包含**端口声明**和**内部逻辑**。
```verilog
module 模块名 (
    // 端口声明
    input  端口1,      // 输入端口
    output 端口2,      // 输出端口
    inout  双向端口    // 双向端口（较少使用）
);
    // 内部信号/变量声明
    wire  信号1;       // 线网类型（用于连续赋值）
    reg   信号2;       // 寄存器类型（用于时序逻辑）

    // 功能描述（组合逻辑/时序逻辑）
    assign 信号1 = ...;  // 连续赋值（组合逻辑）
    always @(...) begin  // 过程块（时序或组合逻辑）
        // 行为描述
    end

endmodule
```

#### **(2) 示例：2输入与门**
```verilog
module and_gate (
    input  a,    // 输入端口 a
    input  b,    // 输入端口 b
    output y     // 输出端口 y
);
    assign y = a & b;  // 组合逻辑：y = a AND b
endmodule
```

---

### **2. 核心概念**
#### **(1) 端口类型**
| 类型      | 说明                                                                 |
|-----------|----------------------------------------------------------------------|
| `input`   | 输入端口，信号从外部传入模块。                                       |
| `output`  | 输出端口，信号从模块传递到外部。                                     |
| `inout`   | 双向端口（如总线），需谨慎使用，通常用于三态逻辑。                   |

#### **(2) 数据类型**
| 类型      | 说明                                                                 |
|-----------|----------------------------------------------------------------------|
| `wire`    | 线网类型，表示物理连线，用于连续赋值（`assign`）或模块间连接。       |
| `reg`     | 寄存器类型，用于存储值，通常在 `always` 块中赋值（不一定是实际寄存器）。 |
| `integer` | 整数类型，一般用于仿真和测试。                                       |

#### **(3) 赋值方式**
| 类型            | 语法                | 适用场景                     |
|-----------------|---------------------|------------------------------|
| **连续赋值**    | `assign 信号 = 表达式;` | 组合逻辑（如门电路、加法器）。 |
| **阻塞赋值**    | `=`（在 `always` 块中） | 组合逻辑（按顺序执行）。       |
| **非阻塞赋值**  | `<=`（在 `always` 块中）| 时序逻辑（并行执行，如触发器）。 |

---

### **3. 行为描述**
#### **(1) 组合逻辑**
- 使用 `assign` 或 `always @(*)` 块：
  ```verilog
  // 使用 assign
  assign sum = a + b;

  // 使用 always 块
  always @(*) begin
      if (sel) begin
          out = a;
      end else begin
          out = b;
      end
  end
  ```

#### **(2) 时序逻辑**
- 使用 `always @(posedge clk)` 描述时钟边沿触发的逻辑（如触发器）：
  ```verilog
  reg [7:0] count;
  always @(posedge clk or posedge reset) begin
      if (reset) begin
          count <= 8'b0;    // 复位时清零
      end else begin
          count <= count + 1; // 每个时钟周期加1
      end
  end
  ```

#### **(3) 初始块（仅用于仿真）**
- `initial` 块在仿真开始时执行一次，常用于测试平台：
  ```verilog
  initial begin
      clk = 0;
      reset = 1;
      #10 reset = 0;  // 10 时间单位后释放复位
  end
  ```
- 详细见[[initial]]

---

### **4. 参数化设计**
- 使用 `parameter` 定义模块常量，提高代码复用性：
  ```verilog
  module counter #(
      parameter WIDTH = 8  // 默认位宽为8
  ) (
      input  clk,
      output reg [WIDTH-1:0] count
  );
      always @(posedge clk) begin
          count <= count + 1;
      end
  endmodule

  // 实例化时重载参数
  counter #(.WIDTH(16)) u_counter (clk, count);
  ```

---

### **5. 模块实例化**
- 通过实例化连接子模块，构建层次化设计：
  ```verilog
  module top;
      wire a, b, y;
      // 实例化与门模块
      and_gate u_and (.a(a), .b(b), .y(y));
  endmodule
  ```

---

### **6. 测试平台（Testbench）**
- 用于验证设计功能，通常包含激励生成和结果检查：
  ```verilog
  module tb_and_gate;
      reg  a, b;
      wire y;

      // 实例化被测模块
      and_gate u_dut (.a(a), .b(b), .y(y));

      // 生成测试激励
      initial begin
          a = 0; b = 0;
          #10 a = 1;
          #10 b = 1;
          #10 $finish;
      end

      // 打印结果
      always @(a or b) begin
          $display("a=%b, b=%b, y=%b", a, b, y);
      end
  endmodule
  ```

---

### **7. 常见注意事项**
1. **组合逻辑锁存器问题**：  
   在 `always` 块中，若未覆盖所有条件分支，会隐含生成锁存器。  
   **解决**：使用 `default` 或确保所有条件分支已赋值。

2. **时序逻辑的复位**：  
   明确同步复位或异步复位，并在敏感列表中正确声明：
   ```verilog
   // 异步复位
   always @(posedge clk or posedge reset) begin ... end
   // 同步复位
   always @(posedge clk) begin ... end
   ```

3. **非阻塞赋值与阻塞赋值**：  
   - **时序逻辑**：使用 `<=`（非阻塞赋值）。  
   - **组合逻辑**：使用 `=`（阻塞赋值）。

---

### **总结**
- **模块化设计**：以 `module` 为核心，通过实例化构建复杂系统。  
- **明确逻辑类型**：区分组合逻辑（`assign` 或 `always @(*)`）和时序逻辑（`always @(posedge clk)`）。  
- **仿真与综合**：`initial` 和 `$display` 等语句仅用于仿真，不可综合。  
- **参数化与重用**：使用 `parameter` 提高代码灵活性。  