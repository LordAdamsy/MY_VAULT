### **adj(时频偏调整)**
1. 在不同的物理上行信道(PUSCH,PUCCH,PRACH)条件下计算时频偏与功率调整量
2. 依据调制编码方式(mcs)和带宽(bw)计算补偿值
3. 计算PRACH/PUCCH和PUSCH功率配置参数，

### **fsm状态机**
#### **用户状态机usr**
1. 抽象基类`UserState`
2. 用户上下文`UserContext`，包括用户状态，状态转换方法，内核信息配置方法，触发信号与槽函数等
3. 待机状态`StandBy`，每0.5s触发检测同步状态是否为已完成，若完成则发送测距请求并进入测距状态
4. 测距状态`RangingState`，每1s触发超时，若3s后还未接收到测距响应则进入待机状态；若收到测距响应则解析消息，向内核发送时间调整值，进入随机接入状态
5. 随机接入状态`RAState`，2s内未接收到随机接入响应则进入待机状态；否则判断响应类型，无误情况下解析消息，发送时间调整值并进入廉洁状态，更新下行SLID列表:
```cpp
emit m_pContext->sig_mutiSmacQueue_addSlid(TsnAppData::instance()->KRTCfg.stbnid );
```
6. 连接状态`ConnectionState`，根据接收到的Cas(Connection Admission Control Sublayer)的消息不同(上行链路维持、NAS、RRC)调用不同的处理函数；若在1s内没有收到链路维持消息或广播消息，则连接断开，进入待机状态。若RRC消息解析为连接释放，且没有业务，则进入心跳状态
7. 心跳状态`HeartBeatState`，S1定时器超时后发送心跳，5s后(S2定时器判断)未收到心跳回复则进入测距响应状态，说明UE与网络连接断开
#### **同步状态机sync**
1. 虚基类`SyncState`
2. 同步上下文`SyncContext`，类似用户上下文，负责状态转换，记录状态，向物理层发送消息(方法未实现)等
3. 起始状态`SyncBoot`，向物理层配置默认参数，通过在mainwindow中连接信号和槽函数触发实现