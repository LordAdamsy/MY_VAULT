
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

### 使用

**通过添加清单文件引入第三方依赖espressif/led_strip**

配置方法：

配置两个结构体参数后实例化led_strip_handle_t结构体指针

typedef struct {
    int strip_gpio_num;      
    uint32_t max_leds;       
    led_pixel_format_t led_pixel_format; 
    led_model_t led_model;   
    struct {
        uint32_t invert_out: 1; 
    } flags;
} led_strip_config_t;

typedef struct {
    rmt_clock_source_t clk_src; 
    uint32_t resolution_hz;     
    size_t mem_block_symbols;      
    struct {
        uint32_t with_dma: 1;   
    } flags;
} led_strip_rmt_config_t;

led_strip_new_rmt_device(const led_strip_config_t \*led_config, const led_strip_rmt_config_t \*rmt_config, led_strip_handle_t \*ret_strip)

常用api可见led_strip.h

1. led_strip_set_pixel(led_strip_handle_t strip, uint32_t index, uint32_t red, uint32_t green, uint32_t blue)
2. led_strip_set_pixel_rgbw(led_strip_handle_t strip, uint32_t index, uint32_t red, uint32_t green, uint32_t blue, uint32_t white)
3. led_strip_refresh(led_strip_handle_t strip)
4. led_strip_clear(led_strip_handle_t strip)
5. led_strip_del(led_strip_handle_t strip)