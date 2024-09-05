![[ip_packet.png]]

1. 版本(version)
2. 头长度(header length):指的是字长，当为1111时首部长度达
	到60字节。若首部长度非4的整数倍则需要填充
3. 区分服务(TOS):3bit优先级，现已弃用；4bit TOS(type of
	service)指定数据包的服务类型；1bit MBZ，通常设置为0
4. 总长度(total length):单位为字节
5. 标识(identification):唯一标识ip数据包，用于分片和重组
6. 标志(flag):
<p align="center">0 | DF | MF</p>
	MF(more fragment):MF=1表示后面还有分片，MF=0表示这是若干数据报片中的最后一个
	DF(don't fragment):DF=0时才允许分片
7. 片偏移(fragment offset):指示分片后的数据包在原始数据包
	中的位置，以<font color="yellow">8字节</font>作为单位，相对于原始数据包的开头
8. 生存时间字段(time to live, TTL):指定了数据包在网络中能
	够经过的最大路由器跳数(路由器转发次数)。当字段为0时数据包被丢弃并向原发送者发送ICMP超时消息
9. 协议(protocol):
<center>
| 字段值 | 协议类型 | <br>
|  1  | ICMP |<br>
|  2  | IGMP |<br>
|  6   | TCP  |<br>
|  17  | UDP  |<br>
|  89  | OSPF |<br>
</center>
10. 首部检验和:CRC16，只校验数据包的头，不校验数据部分
11. 源地址:32bit
12. 目的IP地址:32bit







