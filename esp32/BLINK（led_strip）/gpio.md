
**需要包含头文件drver/gpio.h**

#define GPIO_KEY 0 

void key_init(void)
{
    gpio_config_t key_conf;
    key_conf.intr_type = GPIO_INTR_DISABLE;
    key_conf.mode = GPIO_MODE_INPUT_OUTPUT;
    key_conf.pin_bit_mask = 1ULL << GPIO_KEY;
    key_conf.pull_down_en = GPIO_PULLDOWN_DISABLE;
    key_conf.pull_up_en = GPIO_PULLUP_ENABLE;
    gpio_config(&key_conf);
}

### 常用函数
1. gpio_config(@param:pointer)
2. gpio_set_level(gpio_number, elec level)
3. gpio_get_level(gpio_number)