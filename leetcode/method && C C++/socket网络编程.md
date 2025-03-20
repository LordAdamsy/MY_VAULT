1. 转换字节序，网络的字节序和本机的字节序可能不同，会导致计算结果有误
	大端字节序：MSB存储于最低内存地址 LSB存储于最高内存地址
	小端字节序：MSB存储于最高内存地址 LSB存储于最低内存地址
	字节序的转换函数：
```cpp
uint32_t htonl(uint32_t hostlong);    //主机字节序转换为网络字节序
uint16_t htons(uint16_t hostshort); 
uint32_t ntohl(uint32_t netlong);    ////网络字节序转换为主机字节序
uint16_t ntohs(uint16_t netshort);
```
2. 地址转换函数：
```cpp
#include <netinet/in.h>
#include <arpa/inet.h>

int inet_ aton(const char *cp,struct in_addr *inp);//将点分十进制转换为网络字节序的结构
in_addr_t inet_addr(const char *cp);    //将点分十进制IP地址转换为32位整数
char *inet_ntoa(struct in_addr in)；    //将网络字节序的结构转换为点分十进制
```
3. a).流式套接字SOCK_STREAM(TCP协议):面向连接服务，可靠数据服务，无差错无重复发送，按顺序接收
	b).数据报套接字SOCK_DGRAM(UDP协议):无连接服务，不提供无错保证，数据可能丢失重复，接收顺序混乱
	c).原始套接字SOCK_RAW:将应用层直接封装成ip层能认识的协议格式

注意字节序
改套接字地址定义在<netinet/in.h>中
```cpp
struct sockaddr_in {
    sa_family_t sin_family;   // 地址族，对于 IPv4 应为 AF_INET
    uint16_t sin_port;       // 端口号，网络字节序
    struct in_addr sin_addr;  // IPv4 地址
    char sin_zero[8];        // 填充，确保结构体长度一致
};

struct in_addr {
    in_addr_t s_addr;         // IPv4 地址，网络字节序
};
```
### SOCKET函数
头文件:<sys/socket.h>
1. int socket()