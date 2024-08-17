
**自定义led.c与led.h**

### 关于led灯管WS2812B

![[251fe8047b7bc8764f1b459e6df85080.png]]

![[96c4f6391a8c6ca7fdc941da9979ed4a.png]]

![[40a6b620685942f5f1212f48f980fbf5.png]]

![[7134624c8c968e1f85cc5b24a9d450de 1.png]]

#### 数据结构

![[Pasted image 20240815191208.png]]

### 驱动方式
1. RMT红外遥控，通过发射器发射驱动脉冲
2. LEDC PWM产生脉冲驱动RGB LED

### 使用方式

**通过添加清单文件引入第三方依赖espressif/led_strip**

常用api可见led_strip.h