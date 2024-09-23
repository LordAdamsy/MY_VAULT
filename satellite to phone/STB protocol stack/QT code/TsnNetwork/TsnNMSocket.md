### INetWork.h
定义了抽象类INetWork，包括纯虚函数init(),recv()和send()，初始化，发送和接收
### TsnNMSocket.h
定义TsnNMSocket类，继承QObject和INetWork
定义发送和接收recv()和send()为槽
定义信号以及类成员等
### TsnNMSocket.cpp
实现TsnNMSocket类，实现构造函数
```cpp
TsnNMSocket::TsnNMSocket()
    : m_udpSocket(nullptr)
    , m_pThread(nullptr)
{
    m_dstIP = TsnAppData::instance()->AppCfg.phyIP;
    m_dstPort = TsnAppData::instance()->AppCfg.dstPort;
    m_srcPort = TsnAppData::instance()->AppCfg.srcPort;
}
```

init()函数中实例化QudpSocket对象，需要指定父类指针：
```cpp
m_udpSocket = new QUdpSocket(this);
```
将readyRead()信号与recv()操进行绑定，当套接字有数据可读取时会触发recv()

recv()判断接收缓冲区内是否有待处理的数据报，若有数据报则读取数据，后与内核模块交互，根据数据首字节的信息触发不同的信号
```cpp
    switch (type)
    {
        case NM_TYPE_STATUS:
            emit sig_recvKernelStatus(ba);
            break;
        case NM_TYPE_CONFIG_ECHO:
            emit sig_recvKernelConfig(ba);
            break;
        case NM_TYPE_INIT_SYNC_CTRL_DONE_CMD:
            break;
        case NM_TYPE_INIT_EPH_TF_REQ:
            emit sig_recvKernelInitTFRequest(ba);
            break;
        case NM_TYPE_TF_ADJ_EPH_REQ:
            emit sig_recvKernelTFRequest(ba);
            break;

        default:
            break;
    }
```

