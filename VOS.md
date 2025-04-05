
# 1 **vosTypedefs.h**

### 1.1.1 数据结构定义及对应关系

#### 1.1.1.1 基本数据类型

- **定义**：
    
    - `VOS_UINT8`：无符号 8 位整数，对应 C 的 `unsigned char`。
    - `VOS_SINT8`：有符号 8 位整数，对应 C 的 `signed char`。
    - `VOS_UINT16`：无符号 16 位整数，对应 C 的 `unsigned short`。
    - `VOS_SINT16`：有符号 16 位整数，对应 C 的 `signed short`。
    - `VOS_UINT32`：无符号 32 位整数，对应 C 的 `unsigned int`。
    - `VOS_SINT32`：有符号 32 位整数，对应 C 的 `signed int`。
    - `VOS_FLOAT32`：32 位浮点数，对应 C 的 `float`。
    - `VOS_UINT64`：无符号 64 位整数，对应 C 的 `unsigned long long`。
    - `VOS_SINT64`：有符号 64 位整数，对应 C 的 `signed long long`。
- **用途**：
    
    - 提供跨平台的固定宽度数据类型，适用于需要明确位宽的场景（如网络协议、硬件驱动）。

---

#### 1.1.1.2 地址类型 (`VOS_ADDR`)

- **定义**：
    
    - 根据平台和架构定义：
        - Windows 64 位：`unsigned long long`。
        - Windows 32 位：`unsigned int`。
        - Unix 64 位：`unsigned long long`。
        - Unix 32 位：`unsigned int`。
        - 特定宏 `ACOREMCOS_MCORE` 定义时：`unsigned int`。
- **对应关系**：
    
    - 对应 C 的 `uintptr_t` 或 `unsigned int`/`unsigned long long`，用于表示内存地址。
- **用途**：
    
    - 提供跨平台的地址类型，适用于指针或内存地址操作。

---

#### 1.1.1.3 布尔类型 (`VOS_BOOL`)

- **定义**：
    
    - 在 C++ 中：
        - `VOS_BOOL`：对应 C++ 的 `bool`。
        - `VOS_TRUE` 和 `VOS_FALSE`：分别对应 `true` 和 `false`。
    - 在 C 中：
        - `VOS_BOOL`：对应 C 的 `char`。
        - `VOS_TRUE` 和 `VOS_FALSE`：分别定义为 `(char)1` 和 `(char)0`。
- **用途**：
    
    - 提供跨语言的布尔类型，兼容 C 和 C++。

---

#### 1.1.1.4 空类型 (`VOID`)

- **定义**：
    
    - `VOID`：对应 C 的 `void`。
- **用途**：
    
    - 提供统一的命名方式，适用于函数返回值为 `void` 的场景。

---

### 1.1.2 宏定义

#### 1.1.2.1 空指针 (`VOS_NULL`)

- **定义**：
    
    - `VOS_NULL`：对应 C 的 `NULL`。
    - 当前未启用（被 `#if 0` 包裹）。
- **用途**：
    
    - 提供统一的空指针表示。

---
# 2 **vosMem.h**

### 2.1.1 文件功能

[vosMem.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件主要提供内存管理相关的函数接口，用于动态分配和释放内存。

---

### 2.1.2 数据结构定义

[vosMem.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件中未定义任何数据结构，仅包含函数声明。

---

### 2.1.3 函数及参数定义

#### 2.1.3.1 1. `VOSMalloc`

void* VOSMalloc(VOS_UINT32 size);

- **功能**：
    
    - 动态分配指定大小的内存。
- **参数**：
    
    - `size`：要分配的内存大小，类型为 `VOS_UINT32`（无符号 32 位整数）。
- **返回值**：
    
    - 成功时返回分配的内存指针。
    - 如果分配失败，返回 `NULL`。
- **用途**：
    
    - 用于在运行时分配内存，适合需要动态内存管理的场景。

---

#### 2.1.3.2 2. `VOSFree`

void VOSFree(void \*p);

- **功能**：
    
    - 释放由 `VOSMalloc` 分配的内存。
- **参数**：
    
    - `p`：指向要释放的内存的指针，类型为 `void*`。
- **返回值**：
    
    - 无返回值。
- **用途**：
    
    - 用于释放动态分配的内存，避免内存泄漏。

---

### 2.1.4 C 语言中数据结构的对应关系

- `VOS_UINT32`：对应 C 的 `unsigned int`，用于表示内存大小。
- `void*`：标准 C 类型，用于表示通用指针。

---
# 3 **vosMutex.h**

### 3.1.1 文件功能

[vosMutex.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了互斥锁（Mutex）相关的操作接口，用于线程同步和资源保护。

---

### 3.1.2 数据结构定义

[vosMutex.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件中未定义具体的数据结构，互斥锁通过指针 (`void*`) 进行操作。

- **C 语言对应**：
    - `void*`：表示通用指针，用于抽象互斥锁的具体实现。

---

### 3.1.3 函数及参数定义

#### 3.1.3.1 1. [VOSCreateMutex](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

VOS_BOOL VOSCreateMutex(VOS_BOOL lock, void **pMutex);

- **功能**：
    
    - 创建一个互斥锁。
- **参数**：
    
    - `lock`：是否在创建时立即锁定互斥锁，类型为 `VOS_BOOL`。
    - `pMutex`：指向互斥锁对象的指针，类型为 `void**`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于初始化互斥锁，确保线程安全。

---

#### 3.1.3.2 2. `VOSDeleteMutex`

VOS_BOOL VOSDeleteMutex(void *pMutex);

- **功能**：
    
    - 删除一个互斥锁。
- **参数**：
    
    - `pMutex`：指向要删除的互斥锁对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放互斥锁资源，避免资源泄漏。

---

#### 3.1.3.3 3. `VOSLockMutex`

VOS_BOOL VOSLockMutex(void *pMutex, VOS_UINT32 timeOut);

- **功能**：
    
    - 尝试锁定互斥锁，支持超时机制。
- **参数**：
    
    - `pMutex`：指向要锁定的互斥锁对象的指针，类型为 `void*`。
    - `timeOut`：等待锁定的超时时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于线程间同步，避免资源竞争。

---

#### 3.1.3.4 4. `VOSUnlockMutex`

VOS_BOOL VOSUnlockMutex(void *pMutex);

- **功能**：
    
    - 解锁一个已锁定的互斥锁。
- **参数**：
    
    - `pMutex`：指向要解锁的互斥锁对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放互斥锁，允许其他线程访问资源。

---

#### 3.1.3.5 5. `VOSLockMutexNoWait`

VOS_BOOL VOSLockMutexNoWait(void *pMutex);

- **功能**：
    
    - 尝试立即锁定互斥锁，不等待。
- **参数**：
    
    - `pMutex`：指向要锁定的互斥锁对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于尝试获取互斥锁，如果锁不可用则立即返回。

---

### 3.1.4 C 语言中数据结构的对应关系

- `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示超时时间。
- `void*`：表示通用指针，用于抽象互斥锁的具体实现。

---
# 4 **vosSem.h**

### 4.1.1 文件功能

[vosSem.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了信号量（Semaphore）和事件组（Event Group）相关的操作接口，用于线程同步和事件管理。

---

### 4.1.2 数据结构定义

[vosSem.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件中未定义具体的数据结构，信号量和事件组通过指针 (`void*`) 进行操作。

- **C 语言对应**：
    - `void*`：表示通用指针，用于抽象信号量和事件组的具体实现。

---

### 4.1.3 函数及参数定义

#### 4.1.3.1 1. `GetSemValue`

VOS_BOOL GetSemValue(void *pSem, VOS_SINT32 *sval);

- **功能**：
    
    - 获取信号量的当前值。
- **参数**：
    
    - `pSem`：指向信号量对象的指针，类型为 `void*`。
    - `sval`：用于存储信号量当前值的指针，类型为 `VOS_SINT32*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于查询信号量的当前状态。

---

#### 4.1.3.2 2. `VOSCreateSem`

VOS_BOOL VOSCreateSem(VOS_UINT32 initVal, VOS_UINT32 maxVal, void **ppSem);

- **功能**：
    
    - 创建一个信号量。
- **参数**：
    
    - `initVal`：信号量的初始值，类型为 `VOS_UINT32`。
    - `maxVal`：信号量的最大值，类型为 `VOS_UINT32`。
    - `ppSem`：指向信号量对象指针的指针，类型为 `void**`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于初始化信号量，确保线程同步。

---

#### 4.1.3.3 3. `VOSDeleteSem`

VOS_BOOL VOSDeleteSem(void *pSem);

- **功能**：
    
    - 删除一个信号量。
- **参数**：
    
    - `pSem`：指向要删除的信号量对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放信号量资源，避免资源泄漏。

---

#### 4.1.3.4 4. `VOSWaitSem`

VOS_BOOL VOSWaitSem(void *pSem, VOS_UINT32 timeOut);

- **功能**：
    
    - 等待信号量，支持超时机制。
- **参数**：
    
    - `pSem`：指向信号量对象的指针，类型为 `void*`。
    - `timeOut`：等待信号量的超时时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于线程间同步，避免资源竞争。

---

#### 4.1.3.5 5. `VOSReleaseSem`

VOS_BOOL VOSReleaseSem(void *pSem);

- **功能**：
    
    - 释放信号量。
- **参数**：
    
    - `pSem`：指向信号量对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于增加信号量的值，允许其他线程访问资源。

---

#### 4.1.3.6 6. `VOSCreateEventG`

void* VOSCreateEventG(void);

- **功能**：
    
    - 创建一个事件组。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 成功返回事件组对象的指针，失败返回 `NULL`。
- **用途**：
    
    - 用于初始化事件组，支持事件管理。

---

#### 4.1.3.7 7. `VOSDeleteEventG`

VOS_BOOL VOSDeleteEventG(void *pEventG);

- **功能**：
    
    - 删除一个事件组。
- **参数**：
    
    - `pEventG`：指向要删除的事件组对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放事件组资源，避免资源泄漏。

---

#### 4.1.3.8 8. `VOSGetEventG`

VOS_BOOL VOSGetEventG(void *pEventG, VOS_UINT32 timeOut, VOS_UINT32 *event);

- **功能**：
    
    - 等待事件组中的事件，支持超时机制。
- **参数**：
    
    - `pEventG`：指向事件组对象的指针，类型为 `void*`。
    - `timeOut`：等待事件的超时时间（毫秒），类型为 `VOS_UINT32`。
    - `event`：用于存储触发的事件值的指针，类型为 `VOS_UINT32*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于线程间事件同步。

---

#### 4.1.3.9 9. `VOSSetEventG`

VOS_BOOL VOSSetEventG(void *pEventG, VOS_UINT32 event);

- **功能**：
    
    - 设置事件组中的事件。
- **参数**：
    
    - `pEventG`：指向事件组对象的指针，类型为 `void*`。
    - `event`：要设置的事件值，类型为 `VOS_UINT32`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于触发事件，通知等待的线程。

---

### 4.1.4 C 语言中数据结构的对应关系

- `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示信号量值、超时时间或事件值。
- `VOS_SINT32`：对应 C 的 `signed int`，表示信号量的当前值。
- `void*`：表示通用指针，用于抽象信号量和事件组的具体实现。

---
# 5 **byteOrder.h**

### 5.1.1 文件功能

[byteOrder.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了字节序转换相关的函数接口，用于在主机字节序和网络字节序之间进行数据转换。

---

### 5.1.2 数据结构定义

[byteOrder.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件中未定义具体的数据结构，仅包含函数声明。

- **C 语言对应**：
    - `VOS_UINT8`：对应 C 的 `unsigned char`，表示字节。
    - `VOS_UINT16`：对应 C 的 `unsigned short`，表示 16 位无符号整数。
    - `VOS_UINT32`：对应 C 的 `unsigned int`，表示 32 位无符号整数。
    - `VOS_UINT64`：对应 C 的 `unsigned long long`，表示 64 位无符号整数。

---

### 5.1.3 函数及参数定义

#### 5.1.3.1 1. `GetNet32`

VOS_UINT32 GetNet32(VOS_UINT8 \*pAddr);

- **功能**：
    
    - 从网络字节序的 4 字节数组中读取 32 位无符号整数，并转换为主机字节序。
- **参数**：
    
    - `pAddr`：指向网络字节序数据的指针，类型为 `VOS_UINT8*`。
- **返回值**：
    
    - 转换后的 32 位无符号整数，类型为 `VOS_UINT32`。

---

#### 5.1.3.2 2. `GetNet24`

VOS_UINT32 GetNet24(VOS_UINT8 \*pAddr);

- **功能**：
    
    - 从网络字节序的 3 字节数组中读取 24 位无符号整数，并转换为主机字节序。
- **参数**：
    
    - `pAddr`：指向网络字节序数据的指针，类型为 `VOS_UINT8*`。
- **返回值**：
    
    - 转换后的 24 位无符号整数，类型为 `VOS_UINT32`。

---

#### 5.1.3.3 3. `GetNet16`

VOS_UINT16 GetNet16(VOS_UINT8 \*pAddr);

- **功能**：
    
    - 从网络字节序的 2 字节数组中读取 16 位无符号整数，并转换为主机字节序。
- **参数**：
    
    - `pAddr`：指向网络字节序数据的指针，类型为 `VOS_UINT8*`。
- **返回值**：
    
    - 转换后的 16 位无符号整数，类型为 `VOS_UINT16`。

---

#### 5.1.3.4 4. `GetNet64`

VOS_UINT64 GetNet64(VOS_UINT8 \*pAddr);

- **功能**：
    
    - 从网络字节序的 8 字节数组中读取 64 位无符号整数，并转换为主机字节序。
- **参数**：
    
    - `pAddr`：指向网络字节序数据的指针，类型为 `VOS_UINT8*`。
- **返回值**：
    
    - 转换后的 64 位无符号整数，类型为 `VOS_UINT64`。

---

#### 5.1.3.5 5. `FillNet32`

void FillNet32(VOS_UINT8 \*pAddr, VOS_UINT32 val);

- **功能**：
    
    - 将 32 位无符号整数从主机字节序转换为网络字节序，并填充到 4 字节数组中。
- **参数**：
    
    - `pAddr`：指向目标数组的指针，类型为 `VOS_UINT8*`。
    - `val`：要转换的 32 位无符号整数，类型为 `VOS_UINT32`。
- **返回值**：
    
    - 无返回值。

---

#### 5.1.3.6 6. `FillNet24`

void FillNet24(VOS_UINT8 \*pAddr, VOS_UINT32 val);

- **功能**：
    
    - 将 24 位无符号整数从主机字节序转换为网络字节序，并填充到 3 字节数组中。
- **参数**：
    
    - `pAddr`：指向目标数组的指针，类型为 `VOS_UINT8*`。
    - `val`：要转换的 24 位无符号整数，类型为 `VOS_UINT32`。
- **返回值**：
    
    - 无返回值。

---

#### 5.1.3.7 7. `FillNet16`

void FillNet16(VOS_UINT8 \*pAddr, VOS_UINT16 val);

- **功能**：
    
    - 将 16 位无符号整数从主机字节序转换为网络字节序，并填充到 2 字节数组中。
- **参数**：
    
    - `pAddr`：指向目标数组的指针，类型为 `VOS_UINT8*`。
    - `val`：要转换的 16 位无符号整数，类型为 `VOS_UINT16`。
- **返回值**：
    
    - 无返回值。

---

#### 5.1.3.8 8. `FillNet64`

void FillNet64(VOS_UINT8 \*pAddr, VOS_UINT64 val);

- **功能**：
    
    - 将 64 位无符号整数从主机字节序转换为网络字节序，并填充到 8 字节数组中。
- **参数**：
    
    - `pAddr`：指向目标数组的指针，类型为 `VOS_UINT8*`。
    - `val`：要转换的 64 位无符号整数，类型为 `VOS_UINT64`。
- **返回值**：
    
    - 无返回值。

---

### 5.1.4 C 语言中数据结构的对应关系

- `VOS_UINT8`：对应 C 的 `unsigned char`，表示字节。
- `VOS_UINT16`：对应 C 的 `unsigned short`，表示 16 位无符号整数。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示 32 位无符号整数。
- `VOS_UINT64`：对应 C 的 `unsigned long long`，表示 64 位无符号整数。

---
# 6 **vosQueue.h**

### 6.1.1 文件功能

[vosQueue.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了消息队列的相关操作接口，用于线程间的消息传递和同步。

---

### 6.1.2 数据结构定义

#### 6.1.2.1 1. `SVOSQueueAttri`

- **定义**：
    
    typedef struct {
    
        VOS_UINT8 name[VOS_NAME_LEN+1]; // 队列名称
    
        VOS_UINT32 msgLen;              // 单条消息的最大长度
    
        VOS_UINT32 msgNum;              // 队列中消息的最大数量
    
    } SVOSQueueAttri;
    
- **C 语言对应**：
    
    - 对应 C 的 `struct` 类型。
    - `name`：对应 C 的 `unsigned char` 数组，用于存储队列名称。
    - `msgLen` 和 `msgNum`：对应 C 的 `unsigned int`，分别表示消息长度和消息数量。
- **用途**：
    
    - 用于描述队列的属性，包括名称、单条消息的长度和队列的容量。

---

#### 6.1.2.2 2. `VOSQueue_S`

- **定义**：
    
    typedef struct {
    
        VOS_UINT32 msgIdx;  // 消息索引
    
        VOS_UINT32 msgType; // 消息类型
    
        VOS_SINT8 *pcBuf;   // 消息内容的指针
    
        VOS_UINT32 msgLen;  // 消息长度
    
    } VOSQueue_S;
    
- **C 语言对应**：
    
    - 对应 C 的 `struct` 类型。
    - `msgIdx` 和 `msgType`：对应 C 的 `unsigned int`，分别表示消息的索引和类型。
    - `pcBuf`：对应 C 的 `signed char*`，表示消息内容的指针。
    - `msgLen`：对应 C 的 `unsigned int`，表示消息的长度。
- **用途**：
    
    - 用于描述队列中的单条消息，包括消息的索引、类型、内容和长度。

---

### 6.1.3 函数及参数定义

#### 6.1.3.1 1. `VOSCreateQueue`

VOS_BOOL VOSCreateQueue(void \*pAttri, void \*pQueue);

- **功能**：
    
    - 创建一个消息队列。
- **参数**：
    
    - `pAttri`：指向队列属性结构体（`SVOSQueueAttri`）的指针，类型为 `void*`。
    - `pQueue`：指向队列对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于初始化一个消息队列。

---

#### 6.1.3.2 2. `VOSDeleteQueue`

VOS_BOOL VOSDeleteQueue(void \*pQueue);

- **功能**：
    
    - 删除一个消息队列。
- **参数**：
    
    - `pQueue`：指向要删除的队列对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放队列资源，避免资源泄漏。

---

#### 6.1.3.3 3. `VOSSendToQueue`

VOS_BOOL VOSSendToQueue(void \*pQueue, void \*pMsg, VOS_UINT32 msgSize, VOS_UINT32 timeOut);

- **功能**：
    
    - 向队列中发送消息。
- **参数**：
    
    - `pQueue`：指向队列对象的指针，类型为 `void*`。
    - `pMsg`：指向要发送的消息的指针，类型为 `void*`。
    - `msgSize`：消息的大小，类型为 `VOS_UINT32`。
    - `timeOut`：发送消息的超时时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于将消息添加到队列中。

---

#### 6.1.3.4 4. `VOSReceiveFromQueue`

VOS_BOOL VOSReceiveFromQueue(void \*pQueue, void \*pMsg, VOS_UINT32 msgSize, VOS_UINT32 timeOut);

- **功能**：
    
    - 从队列中接收消息。
- **参数**：
    
    - `pQueue`：指向队列对象的指针，类型为 `void*`。
    - `pMsg`：指向存储接收消息的缓冲区指针，类型为 `void*`。
    - `msgSize`：缓冲区的大小，类型为 `VOS_UINT32`。
    - `timeOut`：接收消息的超时时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于从队列中读取消息。

---

#### 6.1.3.5 5. `VOSGetMsgNum`

VOS_UINT32 VOSGetMsgNum(void \*pQueue);

- **功能**：
    
    - 获取队列中当前消息的数量。
- **参数**：
    
    - `pQueue`：指向队列对象的指针，类型为 `void*`。
- **返回值**：
    
    - 返回队列中当前消息的数量，类型为 `VOS_UINT32`。
- **用途**：
    
    - 用于查询队列的状态。

---

### 6.1.4 C 语言中数据结构的对应关系

- `VOS_UINT8`：对应 C 的 `unsigned char`，用于表示字节。
- `VOS_UINT32`：对应 C 的 `unsigned int`，用于表示无符号整数。
- `VOS_SINT8`：对应 C 的 `signed char`，用于表示有符号字节。
- `void*`：表示通用指针，用于抽象队列和消息的具体实现。

---
# 7 **List.h**

### 7.1.1 文件功能

[List.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了单链表、双链表、哈希表和简单二叉树的相关操作接口，用于实现常用的数据结构操作。

---

### 7.1.2 数据结构定义

#### 7.1.2.1 单链表 (`slist_t`)

- **定义**：
    
    - `slist_node_t`：单链表节点，包含指向下一个节点的指针。
    - `slist_t`：单链表结构，包含节点计数、链表头和链表尾指针。
- **用途**：
    
    - 用于实现单链表的数据结构，支持基本的链表操作。

---

#### 7.1.2.2 双链表 (`list_t`)

- **定义**：
    
    - `list_node_t`：双链表节点，包含指向前后节点的指针。
    - `list_t`：双链表结构，包含节点计数、忙碌标志和链表节点。
- **用途**：
    
    - 用于实现双链表的数据结构，支持双向遍历和插入操作。

---

#### 7.1.2.3 哈希表 (`hashtab_t`)

- **定义**：
    
    - `hash_node_t`：哈希表节点，包含指向下一个节点的指针。
    - `hashtab_t`：哈希表结构，包含哈希函数、比较函数、键值获取函数、哈希桶数组等。
- **用途**：
    
    - 用于实现哈希表的数据结构，支持快速查找和插入操作。

---

#### 7.1.2.4 二叉树 (`bi_tree_t`)

- **定义**：
    
    - `bi_tree_node_t`：二叉树节点，包含指向父节点、左子节点、右子节点的指针，以及平衡因子或颜色。
    - `bi_tree_t`：二叉树结构，包含根节点、节点计数、高度、比较函数和键值获取函数。
- **用途**：
    
    - 用于实现简单的二叉树或平衡二叉树，支持插入、删除和查找操作。

---

### 7.1.3 函数及参数定义

#### 7.1.3.1 单链表操作

1. **`slInit`**
    
    - **功能**：初始化单链表。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
2. **`slCount`**
    
    - **功能**：获取单链表的节点数量。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `const slist_t*`。
3. **`slPopHead`**
    
    - **功能**：弹出单链表的头节点。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
4. **`slReadHead`**
    
    - **功能**：读取单链表的头节点。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
5. **`slPushTail`**
    
    - **功能**：将节点插入到单链表的尾部。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
        - `N`：指向要插入的节点，类型为 `slist_node_t*`。
6. **`slFirst`**
    
    - **功能**：获取单链表的第一个节点。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
7. **`slNext`**
    
    - **功能**：获取单链表中指定节点的下一个节点。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
        - `pNode`：指向当前节点，类型为 `slist_node_t*`。
8. **`slDelete`**
    
    - **功能**：删除单链表中的指定节点。
    - **参数**：
        - `Q`：指向单链表的指针，类型为 `slist_t*`。
        - `N`：指向要删除的节点，类型为 `slist_node_t*`。

---

#### 7.1.3.2 双链表操作

1. **`ListInit`**
    
    - **功能**：初始化双链表。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `list_t*`。
2. **`ListCount`**
    
    - **功能**：获取双链表的节点数量。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `const list_t*`。
3. **`ListFirst`**
    
    - **功能**：获取双链表的第一个节点。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `const list_t*`。
4. **`ListLast`**
    
    - **功能**：获取双链表的最后一个节点。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `const list_t*`。
5. **`ListNext`**
    
    - **功能**：获取双链表中指定节点的下一个节点。
    - **参数**：
        - `pNode`：指向当前节点，类型为 `const list_node_t*`。
6. **`ListPrev`**
    
    - **功能**：获取双链表中指定节点的前一个节点。
    - **参数**：
        - `pNode`：指向当前节点，类型为 `const list_node_t*`。
7. **`ListInsertBefore`**
    
    - **功能**：在双链表中指定节点之前插入新节点。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `list_t*`。
        - `pNext`：指向目标节点，类型为 `list_node_t*`。
        - `pNode`：指向要插入的节点，类型为 `list_node_t*`。
8. **`ListDelete`**
    
    - **功能**：删除双链表中的指定节点。
    - **参数**：
        - `pList`：指向双链表的指针，类型为 `list_t*`。
        - `pNode`：指向要删除的节点，类型为 `list_node_t*`。

---

#### 7.1.3.3 哈希表操作

1. **`HashInit`**
    
    - **功能**：初始化哈希表。
    - **参数**：
        - `hashtab`：指向哈希表的指针，类型为 `hashtab_t*`。
2. **`HashInsert`**
    
    - **功能**：向哈希表中插入节点。
    - **参数**：
        - `hashtab`：指向哈希表的指针，类型为 `hashtab_t*`。
        - `node`：指向要插入的节点，类型为 `hash_node_t*`。
3. **`HashFind`**
    
    - **功能**：在哈希表中查找节点。
    - **参数**：
        - `hashtab`：指向哈希表的指针，类型为 `const hashtab_t*`。
        - `key`：指向要查找的键，类型为 `const void*`。

---

#### 7.1.3.4 二叉树操作

1. **`bi_tree_init`**
    
    - **功能**：初始化二叉树。
    - **参数**：
        - `tree`：指向二叉树的指针，类型为 `bi_tree_t*`。
2. **`bi_tree_insert`**
    
    - **功能**：向二叉树中插入节点。
    - **参数**：
        - `tree`：指向二叉树的指针，类型为 `bi_tree_t*`。
        - `node`：指向要插入的节点，类型为 `bi_tree_node_t*`。
3. **`bi_tree_find`**
    
    - **功能**：在二叉树中查找节点。
    - **参数**：
        - `tree`：指向二叉树的指针，类型为 `bi_tree_t*`。
        - `key`：指向要查找的键，类型为 `void*`。

---
# 8 **vosSys.h**

### 8.1.1 文件功能

[vosSys.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了系统相关的操作接口，包括断言、时间获取等功能。

---

### 8.1.2 数据结构定义

[vosSys.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件中未定义具体的数据结构，仅包含函数声明。

- **C 语言对应**：
    - `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
    - `VOS_UINT32`：对应 C 的 `unsigned int`，表示无符号 32 位整数。
    - `VOS_SINT64`：对应 C 的 `signed long long`，表示有符号 64 位整数。

---

### 8.1.3 函数及参数定义

#### 8.1.3.1 1. `VOSAssert`

void VOSAssert(VOS_BOOL flag);

- **功能**：
    
    - 用于断言检查，如果 `flag` 为假（`VOS_FALSE`），则触发断言。
- **参数**：
    
    - `flag`：布尔值，类型为 `VOS_BOOL`，表示断言条件。
- **用途**：
    
    - 用于调试时检查程序状态，确保某些条件为真。

---

#### 8.1.3.2 2. `_VOSAbort`

void \_VOSAbort(const char \*file, VOS_UINT32 line, const char \*str);

- **功能**：
    
    - 触发程序中止，并输出错误信息。
- **参数**：
    
    - `file`：字符串，类型为 `const char*`，表示出错的文件名。
    - `line`：无符号整数，类型为 `VOS_UINT32`，表示出错的行号。
    - `str`：字符串，类型为 `const char*`，表示错误描述信息。
- **用途**：
    
    - 用于在程序遇到严重错误时中止执行，并提供调试信息。

---

#### 8.1.3.3 3. `VOSGetTime`

VOS_SINT64 VOSGetTime(void);

- **功能**：
    
    - 获取当前系统时间（以毫秒为单位）。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 当前时间，类型为 `VOS_SINT64`，单位为毫秒。
- **用途**：
    
    - 用于获取系统的当前时间戳，适合时间记录或计算。

---

#### 8.1.3.4 4. `VOSGetTimeUs`

VOS_SINT64 VOSGetTimeUs(void);

- **功能**：
    
    - 获取当前系统时间（以微秒为单位）。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 当前时间，类型为 `VOS_SINT64`，单位为微秒。
- **用途**：
    
    - 用于获取高精度的系统时间戳，适合精确时间测量。

---

#### 8.1.3.5 5. `GetMonnotonicTime`

VOS_SINT64 GetMonnotonicTime(void);

- **功能**：
    
    - 获取单调递增的时间（以毫秒为单位）。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 单调递增时间，类型为 `VOS_SINT64`，单位为毫秒。
- **用途**：
    
    - 用于测量时间间隔，避免因系统时间调整导致的时间跳变问题。

---

### 8.1.4 C 语言中数据结构的对应关系

- `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示无符号 32 位整数。
- `VOS_SINT64`：对应 C 的 `signed long long`，表示有符号 64 位整数。
- `const char*`：对应 C 的字符串指针，用于传递文件名或描述信息。

---
# 9 **vosTask.h**

### 9.1.1 文件功能

[vosTask.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了任务管理相关的操作接口，包括任务的创建、删除、挂起、恢复等功能。

---

### 9.1.2 数据结构定义

#### 9.1.2.1 1. `VOS_TASK_FUN`

- **定义**：
    
    typedef void (\*VOS_TASK_FUN)(void \*);
    
- **C 语言对应**：
    
    - 对应 C 的函数指针类型。
    - 表示任务的入口函数，接受一个 `void*` 类型的参数，无返回值。
- **用途**：
    
    - 用于定义任务的执行函数。

---

#### 9.1.2.2 2. `SVOSTaskAttri`

- **定义**：
    
    typedef struct {
    
        char name[VOS_NAME_LEN + 1]; // 任务名称
    
        VOS_UINT32 stkSize;          // 堆栈大小
    
        VOS_UINT32 priority;         // 任务优先级
    
        VOS_TASK_FUN func;           // 任务入口函数
    
        void *pArg;                  // 任务入口函数的参数
    
    } SVOSTaskAttri, \*PSVOSTaskAttri;
    
- **C 语言对应**：
    
    - 对应 C 的 `struct` 类型。
    - `name`：对应 C 的 `char` 数组，用于存储任务名称。
    - `stkSize` 和 `priority`：对应 C 的 `unsigned int`，分别表示任务的堆栈大小和优先级。
    - `func`：对应任务的入口函数，类型为 `VOS_TASK_FUN`。
    - `pArg`：对应任务入口函数的参数，类型为 `void*`。
- **用途**：
    
    - 用于描述任务的属性，包括名称、堆栈大小、优先级、入口函数及其参数。

---

### 9.1.3 函数及参数定义

#### 9.1.3.1 1. `VOSCreateTask`

VOS_BOOL VOSCreateTask(void \*pAttri, void \*\*pTask);

- **功能**：
    
    - 创建一个任务。
- **参数**：
    
    - `pAttri`：指向任务属性结构体（`SVOSTaskAttri`）的指针，类型为 `void*`。
    - `pTask`：指向任务对象的指针，类型为 `void**`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于初始化并启动一个任务。

---

#### 9.1.3.2 2. `VOSDeleteTask`

VOS_BOOL VOSDeleteTask(void \*pTask);

- **功能**：
    
    - 删除一个任务。
- **参数**：
    
    - `pTask`：指向要删除的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放任务资源，避免资源泄漏。

---

#### 9.1.3.3 3. `VOSSuspendTask`

VOS_BOOL VOSSuspendTask(void \*pTask);

- **功能**：
    
    - 挂起一个任务。
- **参数**：
    
    - `pTask`：指向要挂起的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于暂停任务的执行。

---

#### 9.1.3.4 4. `VOSResumeTask`

VOS_BOOL VOSResumeTask(void \*pTask);

- **功能**：
    
    - 恢复一个挂起的任务。
- **参数**：
    
    - `pTask`：指向要恢复的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于恢复任务的执行。

---

#### 9.1.3.5 5. `VOSGetTask`

void \*VOSGetTask(void);

- **功能**：
    
    - 获取当前任务的标识。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 返回当前任务的标识，类型为 `void*`。
- **用途**：
    
    - 用于获取当前正在运行的任务信息。

---

#### 9.1.3.6 6. `VOSSetTask`

void VOSSetTask(void \*id);

- **功能**：
    
    - 设置当前任务的标识。
- **参数**：
    
    - `id`：任务标识，类型为 `void*`。
- **返回值**：
    
    - 无。
- **用途**：
    
    - 用于设置当前任务的上下文。

---

#### 9.1.3.7 7. `VOSTaskSleep`

void VOSTaskSleep(VOS_UINT32 time);

- **功能**：
    
    - 让当前任务休眠指定的时间。
- **参数**：
    
    - `time`：休眠时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 无。
- **用途**：
    
    - 用于让任务进入休眠状态，释放 CPU 资源。

---

### 9.1.4 C 语言中数据结构的对应关系

- `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示无符号 32 位整数。
- `void*`：表示通用指针，用于抽象任务对象和参数。
- `VOS_TASK_FUN`：对应 C 的函数指针类型，用于定义任务的入口函数。

---
# 10 **vosTimer.h**

### 10.1.1 文件功能

[vosTask.h](vscode-file://vscode-app/d:/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) 文件提供了任务管理相关的操作接口，包括任务的创建、删除、挂起、恢复等功能。

---

### 10.1.2 数据结构定义

#### 10.1.2.1 1. `VOS_TASK_FUN`

- **定义**：
    
    typedef void (\*VOS_TASK_FUN)(void \*);
    
- **C 语言对应**：
    
    - 对应 C 的函数指针类型。
    - 表示任务的入口函数，接受一个 `void*` 类型的参数，无返回值。
- **用途**：
    
    - 用于定义任务的执行函数。

---

#### 10.1.2.2 2. `SVOSTaskAttri`

- **定义**：
    
    typedef struct {
    
        char name[VOS_NAME_LEN + 1]; // 任务名称
    
        VOS_UINT32 stkSize;          // 堆栈大小
    
        VOS_UINT32 priority;         // 任务优先级
    
        VOS_TASK_FUN func;           // 任务入口函数
    
        void *pArg;                  // 任务入口函数的参数
    
    } SVOSTaskAttri, \*PSVOSTaskAttri;
    
- **C 语言对应**：
    
    - 对应 C 的 `struct` 类型。
    - `name`：对应 C 的 `char` 数组，用于存储任务名称。
    - `stkSize` 和 `priority`：对应 C 的 `unsigned int`，分别表示任务的堆栈大小和优先级。
    - `func`：对应任务的入口函数，类型为 `VOS_TASK_FUN`。
    - `pArg`：对应任务入口函数的参数，类型为 `void*`。
- **用途**：
    
    - 用于描述任务的属性，包括名称、堆栈大小、优先级、入口函数及其参数。

---

### 10.1.3 函数及参数定义

#### 10.1.3.1 1. `VOSCreateTask`

VOS_BOOL VOSCreateTask(void \*pAttri, void \*\*pTask);

- **功能**：
    
    - 创建一个任务。
- **参数**：
    
    - `pAttri`：指向任务属性结构体（`SVOSTaskAttri`）的指针，类型为 `void*`。
    - `pTask`：指向任务对象的指针，类型为 `void**`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于初始化并启动一个任务。

---

#### 10.1.3.2 2. `VOSDeleteTask`

VOS_BOOL VOSDeleteTask(void \*pTask);

- **功能**：
    
    - 删除一个任务。
- **参数**：
    
    - `pTask`：指向要删除的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于释放任务资源，避免资源泄漏。

---

#### 10.1.3.3 3. `VOSSuspendTask`

VOS_BOOL VOSSuspendTask(void \*pTask);

- **功能**：
    
    - 挂起一个任务。
- **参数**：
    
    - `pTask`：指向要挂起的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于暂停任务的执行。

---

#### 10.1.3.4 4. `VOSResumeTask`

VOS_BOOL VOSResumeTask(void \*pTask);

- **功能**：
    
    - 恢复一个挂起的任务。
- **参数**：
    
    - `pTask`：指向要恢复的任务对象的指针，类型为 `void*`。
- **返回值**：
    
    - 成功返回 `VOS_TRUE`，失败返回 `VOS_FALSE`。
- **用途**：
    
    - 用于恢复任务的执行。

---

#### 10.1.3.5 5. `VOSGetTask`

void \*VOSGetTask(void);

- **功能**：
    
    - 获取当前任务的标识。
- **参数**：
    
    - 无。
- **返回值**：
    
    - 返回当前任务的标识，类型为 `void*`。
- **用途**：
    
    - 用于获取当前正在运行的任务信息。

---

#### 10.1.3.6 6. `VOSSetTask`

void VOSSetTask(void \*id);

- **功能**：
    
    - 设置当前任务的标识。
- **参数**：
    
    - `id`：任务标识，类型为 `void*`。
- **返回值**：
    
    - 无。
- **用途**：
    
    - 用于设置当前任务的上下文。

---

#### 10.1.3.7 7. `VOSTaskSleep`

void VOSTaskSleep(VOS_UINT32 time);

- **功能**：
    
    - 让当前任务休眠指定的时间。
- **参数**：
    
    - `time`：休眠时间（毫秒），类型为 `VOS_UINT32`。
- **返回值**：
    
    - 无。
- **用途**：
    
    - 用于让任务进入休眠状态，释放 CPU 资源。

---

### 10.1.4 C 语言中数据结构的对应关系

- `VOS_BOOL`：对应 C 的 `char`（在 C++ 中为 `bool`），表示布尔值。
- `VOS_UINT32`：对应 C 的 `unsigned int`，表示无符号 32 位整数。
- `void*`：表示通用指针，用于抽象任务对象和参数。
- `VOS_TASK_FUN`：对应 C 的函数指针类型，用于定义任务的入口函数。

---
