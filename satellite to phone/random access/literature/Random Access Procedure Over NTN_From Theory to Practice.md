### 蜂窝网络的随机接入流程

下行采用广播同步信号（primary and secondary synchronization signals）实现同步，若上行采用相同的方法则效率低且用户侧功率受限。因此上行同步采用随机接入流程。

两种接入流程：基于竞争的RA（4-step message between UEs and BS）以及基于非竞争的RA（2-step message）

![[Pasted image 20240819154638.png]]

#### message 1
UE完成下行同步后能够获得控制信道相关信息，如对于物理随机接入信道（PRACH）的配置索引
当PRACH时频资源（随机接入机会）存在时，UE向BS发送随机接入序列请求接入
通过接收时间，基站可以估计UE的RTT，并用于时间提前量（TA）的计算

**过程中UE为竞争接入，可能出现冲突。对于同样的接入机会对应唯一的RA序列，当UE的发送序列相同时说明出现冲突**

#### message 2
BS在一个RAO中持续检测RA序列，一旦检测到则会发送随机接入响应（RAR），即message 2.
RAR包括TA参数，用户后续发送上行数据需要的时频资源以及调制编码方式
通过给不同的用户分配不同的资源块避免冲突
message 1中产生的冲突会导致有些用户在RAR window中收不到RAR，说明接入失败

![[Pasted image 20240819162908.png]]
#### message 3
初始化具有UE特定ID（C-RNTI)的连接需求
基于冲突的RA存在此阶段，视为冲突解决阶段
非基于冲突的RA此阶段被跳过，因为用户已被特定认证
除用户ID外，UE还可以报告数据卷状态（data volume status）和功率余量
#### message 4
BS向UE发回确认，C-RNTI作为用户的永久ID
若在contention resolution timer中未收到确认则需重新再RAO中发送
message 3和4应用HARQ，包含表示ACK与NACK的额外信息

![[Pasted image 20240819165800.png]]
### NTN的RA流程中的挑战

#### RAO中UE和BA的失配
