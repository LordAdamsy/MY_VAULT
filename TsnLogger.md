### 0.1.1 1. **`TsnLogger.h`**

- **功能**：定义日志记录和调试接口，提供日志级别控制和日志输出功能。

#### 0.1.1.1 外部接口函数

1. **[writeLog](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**
    
    void writeLog(VOS_UINT32 level, VOS_UINT32 line, const VOS_SINT8 *fmt, ...);
    
    - **功能**：记录日志信息。
    - **参数**：
        - [level](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：日志级别，类型为 [VOS_UINT32](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)，支持以下级别：
            - [LOG_LEVEL_DEBUG](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：调试信息。
            - `LOG_LEVEL_INFO`：普通信息。
            - [LOG_LEVEL_WARNING](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：警告信息。
            - [LOG_LEVEL_CRITICAL](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：严重错误信息。
            - [LOG_LEVEL_FATAL](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：致命错误信息。
        - [line](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：日志所在的代码行号。
        - [fmt](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：日志格式字符串，支持可变参数。
2. **[tsn_debug](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**
    
    void tsn_debug(const VOS_SINT8 *fmt, ...);
    
    - **功能**：记录调试信息。
    - **参数**：
        - [fmt](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：调试信息的格式字符串，支持可变参数。

#### 0.1.1.2 宏定义

- **日志级别宏**：
    
```C
#define LogDebug(fmt, ...) writeLog(LOG_LEVEL_DEBUG, __LINE__, fmt, ##__VA_ARGS__)
#define LogInfo(fmt, ...) writeLog(LOG_LEVEL_INFO, __LINE__, fmt, ##__VA_ARGS__)
#define LogWarning(fmt, ...) writeLog(LOG_LEVEL_WARNING, __LINE__, fmt, ##__VA_ARGS__)
#define LogCritical(fmt, ...) writeLog(LOG_LEVEL_CRITICAL, __LINE__, fmt, ##__VA_ARGS__)
#define LogFatal(fmt, ...) writeLog(LOG_LEVEL_FATAL, __LINE__, fmt, ##__VA_ARGS__)
```
    
    - **功能**：提供日志记录的快捷接口，分别对应不同的日志级别。

---

### 0.1.2 2. **`TsnLogger.c`**

- **功能**：实现日志记录和调试接口的具体逻辑。

#### 0.1.2.1 外部接口函数

1. **[writeLog](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**
    
    - **功能**：根据日志级别和格式化字符串记录日志信息。
    - **实现细节**：
        - 根据日志级别控制是否输出日志。
        - 支持通过配置文件控制日志输出的开关。
        - 日志信息可以输出到控制台或文件。
2. **[tsn_debug](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**
    
    - **功能**：记录调试信息。
    - **实现细节**：
        - 格式化调试信息。
        - 输出到控制台或通过网络发送调试信息。

---

### 0.1.3 总结

1. **外部接口函数**：
    
    - [writeLog](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：记录日志信息，支持多种日志级别。
    - [tsn_debug](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：记录调试信息。
2. **功能**：
    
    - 提供日志记录和调试功能。
    - 支持日志级别控制（如 `DEBUG`、`INFO`、`WARNING` 等）。
    - 日志信息可以输出到控制台、文件或通过网络发送。
3. **用途**：
    
    - 用于记录系统运行时的状态信息、调试信息和错误信息，便于问题定位和系统维护。

这些接口为系统提供了统一的日志记录和调试功能，便于开发和运维人员监控系统运行状态。