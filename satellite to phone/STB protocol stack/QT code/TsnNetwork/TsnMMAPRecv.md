## **TsnMMAPSocket**
### TsnMMAPSocket.h
定义`block_desc`结构体，包括tpacket_hdr_v1结构体，即每个数据包帧的头部，描述环形缓冲区内存块的信息

定义`ring`结构体，包括iovec指针与tpacket_req3指针等，分别用于描述聚集/分散IO操作和配置使用PACKET_MMAP接口的原始套接字的接收环形缓冲区。

定义TsnMMAPSocket类，包括读取和发送等成员函数，以及`ring`结构体，tpacket3_hdr结构体(包含捕获到的帧的相关信息，理论长度，状态，时间戳，网络层与MAC字段等信息)和sockaddr_ll结构体(表示数据链路层的套接字地址)
### TsnMMAPSocket.cpp
实现TsnMMAPSocket类的方法，包括初始化套接字setup_socket：
1. 声明套接字
2. 配置packet_ersion等相关参数
3. 初始化与配置环形缓冲区ring的相关信息(m_ring.req)
4. 根据m_ring.req来配置套接字以使用接收环形缓冲区
5. 应用mmap将套接字映射到内存，m_ring.map存放内存空间首地址
6. 初始化`m_ring_rd`，通过malloc申请iovec指针数组，通过assert判断申请是否成功，并将内存空间与iovec结构体实现映射，方便高效IO操作
7. 初始化网络接口`m_sock_ll`，并绑定套接字与网络接口
实现：
1. 内存块中包数量统计(pkt_num_in_block)
2. 获取内存块中第一个数据包地址(set_ppd)
3. 通过套接字向绑定的网络接口发送数据(send)
4. 从内存块中取数据包地址(get_pkt_in_block，引用传递，获取MAC层头在数据包缓冲区中的偏移量，并修改m_ppd到下一个数据包的首地址)
5. 内存块清空(flush_block)
6. 读取内存块地址(block_desc \*read(int block_num))
7. 拆解套接字(teardown_socket)
## **TsnMMAPRecv**
### TsnMMAPRecv.h
定义TsnMMAPRecv类，继承**QThread**

成员函数包括mac地址与ip地址的处理、接收数据出处理等，成员包括mac与ip地址，adaptername与TsnMMAPSocket类对象指针
### TsnMMAPRecv.cpp
1. 构造函数与析构函数的初始化，`m_bExit`布尔变量确定线程是否需要结束
2. 设置AdapterName(setAdapterName)
3. 返回与mac和IP地址
4. 获取MAC地址(getMacAddr)，通过linux系统调用ioctl，套接字配置指向网口，`ifr`为ifreq结构体，存放获取的MAC地址
5. 获取IP地址，方法同4
6. 发送数据，同TsnMMAPSocket.send()
7. 实现run方法，获取MAC地址，实例化TsnMMAPSocket对象，通过pllfd结构体监视socket文件描述符的行为。初始为POLLIN，通过poll方法等待socket上有事件发生(接收数据)。之后读取初始内存块地址，调用函数processRcvData处理数据，依次处理每个内存块中的数据。需要结束套接字时设置布尔变量`m_bExit`为1即可
## **TsnMMAPRecvPhy**
### TsnMMAPRecvPhy.h
定义物理层接收类TsnMMAPRecvPhy
### TsnMMAPRecvPhy.cpp
实现虚函数processRcvData
接收端核对发送端mac地址是否有误，无误则进行接收
网口字节数与已处理网口数增加
依据物理层策略上下文对数据进行处理
### **TsnMMAPRecvTraf**
### TsnMMAPRecvTraf.cpp
实现对Arp请求和回复的处理
处理arp回复和请求：
```cpp
if (MAKE_WORD(arp->op[0], arp->op[1]) == TsnARP::ARP_REPLY) //表示ARP回复
    {
        quint32 ip = MAKE_UINT(arp->src_ip[0], arp->src_ip[1], arp->src_ip[2], arp->src_ip[3]);
        TByteArray mac((const char *)arp->src_mac, 6);

        pArp->hashUpdate(ip, mac);

        pAppData->dlStatus.rcv_arp_res_num++;
    }
    else if (MAKE_WORD(arp->op[0], arp->op[1]) == TsnARP::ARP_REQUEST) //ARP请求
    {
        //发送回复
        TByteArray macAddr = this->macAddr();
        TByteArray replyba = pArp->proxy_arp((TsnARP::IP_ARP *)p, macAddr);

        if (replyba.empty())
        {
            return;
        }

        pAppData->dlStatus.rcv_arp_req_num++;

        TByteArray ethHeader;
        ethHeader.append((const char *)arp->src_mac, 6);
        ethHeader.append(macAddr);
        ethHeader.push_back(0x08);
        ethHeader.push_back((uchar)0x06);
        ethHeader.append(replyba);

        if (0 == send((const uchar *)ethHeader.data(), ethHeader.size()))
            pAppData->dlStatus.snd_ip_failed_num++;

    }
```
其中的宏定义：
```cpp
#define MAKE_UINT(a,b,c,d) ((a<<24) | (b<<16) | (c<<8) | d)

#define MAKE_WORD(a,b) ((ushort)(((uchar)(b))|(((ushort)((uchar)(a)))<<8)))
```

当为arp请求时调用proxy_arp返回mac地址