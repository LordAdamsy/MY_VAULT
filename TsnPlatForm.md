### 0.1.1 1. **`RawSocket.h`**

- **功能**：提供基于 Raw Socket 的网络接口操作。
    
- **外部接口函数**：
    
    int init_raw_socket(const char \*iface, raw_socket_info \*info);
    
    - **功能**：初始化 Raw Socket 并获取网络接口索引。
    - **参数**：
        - [iface](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：网络接口名称。
        - [info](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：存储 Raw Socket 信息的结构体指针。
    
    void send_ethernet_frame(raw_socket_info \*info, const unsigned char \*data, size_t data_len);
    
    - **功能**：发送以太网帧。
    - **参数**：
        - [info](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：Raw Socket 信息。
        - [data](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：要发送的数据。
        - [data_len](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：数据长度。
    
    VOS_SINT16 receive_ethernet_frame(raw_socket_info \*info, VOS_UINT8 \*buffer);
    
    - **功能**：接收以太网帧。
    - **参数**：
        - [info](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：Raw Socket 信息。
        - [buffer](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：存储接收数据的缓冲区。
    
    void close_raw_socket(raw_socket_info \*info);
    
    - **功能**：关闭 Raw Socket。
    - **参数**：
        - [info](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：Raw Socket 信息。

---

### 0.1.2 2. **[MMAPSocket.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**

- **功能**：提供基于内存映射的网络接口操作。
    
- **外部接口函数**：
    
    VOS_SINT32 setup_socket(const VOS_SINT8 \*netdev, struct MMAPSocket \*msock);
    
    - **功能**：设置内存映射的 Socket。
    - **参数**：
        - [netdev](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：网络设备名称。
        - [msock](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：内存映射 Socket 结构体。
    
    VOS_SINT32 mmap_socket_send(struct MMAPSocket \*msock, const VOS_UINT8 \*data, VOS_SINT32 len);
    
    - **功能**：发送数据包。
    - **参数**：
        - [msock](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：内存映射 Socket。
        - [data](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：要发送的数据。
        - [len](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：数据长度。
    
    struct block_desc \*mmap_socket_read(struct MMAPSocket \*msock, VOS_SINT32 block_num);
    
    - **功能**：读取数据块。
    - **参数**：
        - [msock](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：内存映射 Socket。
        - [block_num](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：数据块编号。

---

### 0.1.3 3. **`SerialPort.h`**

- **功能**：提供串口操作接口。
    
- **外部接口函数**：
    
    VOS_SINT32 createSerialPort(const VOS_SINT8 \*portName, VOS_SINT32 baudRate);
    
    - **功能**：创建串口。
    - **参数**：
        - [portName](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：串口名称。
        - [baudRate](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：波特率。
    
    VOS_SINT32 serialPortRead(VOS_SINT32 fd, VOS_SINT8 \*buffer, VOS_SINT32 size);
    
    - **功能**：读取串口数据。
    - **参数**：
        - [fd](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：文件描述符。
        - [buffer](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：存储读取数据的缓冲区。
        - [size](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：缓冲区大小。
    
    void closeSerialPort(VOS_SINT32 fd);
    
    - **功能**：关闭串口。
    - **参数**：
        - [fd](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：文件描述符。

---

### 0.1.4 4. **`TsnNetLink.h`**

- **功能**：提供基于 Netlink 的网络接口操作。
    
- **外部接口函数**：
    
    VOS_SINT32 netlink_init(void);
    
    - **功能**：初始化 Netlink 通信。
    
    VOS_SINT32 netlink_send(const void \*data, VOS_SINT32 len);
    
    - **功能**：发送 Netlink 数据。
    - **参数**：
        - [data](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：要发送的数据。
        - [len](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：数据长度。
    
    VOS_SINT32 netlink_recv(void \*buf, VOS_SINT32 len);
    
    - **功能**：接收 Netlink 数据。
    - **参数**：
        - [buf](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：存储接收数据的缓冲区。
        - [len](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：缓冲区大小。
    
    void netlink_close(void);
    
    - **功能**：关闭 Netlink 通信。

---

### 0.1.5 5. **`NjIf.h`**

- **功能**：提供与物理层和控制层的接口操作。
    
- **外部接口函数**：
    
    VOID stb_init(ker_stb \*stb);
    
    - **功能**：初始化 [stb](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 结构体。
    - **参数**：
        - [stb](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：指向 [ker_stb](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 结构体的指针。
    
    ker_stb \*get_ker_stb(void);
    
    - **功能**：获取 [ker_stb](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 结构体实例。

---

### 0.1.6 6. **`TsnEthTools.h`**

- **功能**：提供以太网工具函数。
- **外部接口函数**：
    
    VOS_SINT32 setGRO(const VOS_SINT8 *name);
    
    - **功能**：设置网卡的 GRO（Generic Receive Offload）。
    - **参数**：
        - [name](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：网卡名称。

---

### 0.1.7 7. **`PlatformTool.h`**

- **功能**：提供平台工具函数。
- **外部接口函数**：
    
    void AcoreCpuStatics(VOS_UINT32 timerId, void *tmr, void *env);
    
    - **功能**：统计 CPU 使用情况。
    - **参数**：
        - [timerId](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：定时器 ID。
        - [tmr](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：定时器指针。
        - [env](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)：环境参数。

---

### 0.1.8 总结

`TsnPlatForm` 文件夹中的头文件定义了多种外部接口函数，涵盖了以下功能：

1. **网络接口操作**：
    
    - Raw Socket（`RawSocket.h`）。
    - 内存映射 Socket（[MMAPSocket.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)）。
    - Netlink 通信（`TsnNetLink.h`）。
2. **串口操作**：
    
    - 串口创建、读取和关闭（`SerialPort.h`）。
3. **平台工具**：
    
    - CPU 使用统计（`PlatformTool.h`）。
    - 网卡 GRO 设置（`TsnEthTools.h`）。
4. **物理层和控制层接口**：
    
    - [stb](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 结构体初始化和获取（`NjIf.h`）。

这些接口为系统的底层通信和平台操作提供了统一的封装，便于上层模块调用和管理。