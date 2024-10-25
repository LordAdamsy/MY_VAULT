### RawSocket
1. void getTxQueneLen(int sock, const char \*netdev)
	获取网络设备netdev的传输队列长度
2. int setTxQueneLen(int sock, const char \*netdev, int queueLen)
	设置网络设备netdev的传输队列长度
3. int getSendBuffLen(int sock, const char \*netdev)
	<sys/socket.h>中的getsockopt可获取当前写缓冲区大小
4. int setSendBuffLen(int sock, const char \*netdev)
	<sys/socket.h>中的setsockopt可获取当前写缓冲区大小
5. int init(char \*netdev)
	创建socket，设置传输队列长度、缓冲区大小，并通过bind函数设置绑定的地址信息(需要强制转换sockaddr_ll指针到sockaddr指针)
6. int send(const char \*data, int len)
	向指定地址发送数据，系统调用sendto实现
7. TByteArray getMac(TByteArray name)
	遍历所有网络接口，找到mac地址，并从字符串转换为int后push_back到字符串`ret`内输出

### TsnMMAPSend
作为发送基类，声明send函数

### TsnMMAPSendPhy
继承TsnMMAPSend，实现发送函数(通过socket)与物理层消息生成函数（目标mac，本机mac，协议类型，消息头[消息类型，首包flag，会话数]，数据)

### TsnMMAPSendTraf
继承TsnMMAPSend，实现发送函数

