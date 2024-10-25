
对于[[Architecture]]中的架构：
1. 对于透明转发，卫星仅仅充当射频中继器，不作为NB-IoT协议的结束，并不充当NB-IoT协议中的BS，因此馈电链路采用NB-IoT-Uu接口
3. 对于再生负载，BS位于卫星上，馈电链路作为BS与核心网间的接口

### NB-IoT接入流程

#### 4步接入流程
$T_{RAO} > T_{msg1} + T_{RAR} + T_{CRT} + T_{RAR \; starting \; interval} + T_{CRT \; processing}$
根据3GPP标准 TS 36.213，$T_{RAR \; starting \; interval}$为msg1发送后的4ms或41ms。

#### RA失败可能的原因有：
1. 信道状态差：BS未检测到前导码，累积能量未达阈值，因此UE在RAR window内未收到RAR，提取BO值（back-off，退避）用于重传前的设置
2. 冲突：当多设备选择相同的前导码时，其都会收到相同的RAR，但只有一个UE会收到CRM（contention resolution message）。其他设备会在BO时间后开始新的接入流程。退避的策略能够减少RAO中的拥塞。用户在拥塞后，会选择一个位于[0,BO]内的值作为退避值。

	那么对于在第n个RAO冲突的UE而言，其在之后第k个BO interval发送的概率为：
	
![[Pasted image 20240825151520.png]]

#### 影响随机接入性能的另一个因素是前导码发送时分配的子载波数量

假设有S个空闲的子信道，N个用户，则有n个用户选择相同RAO的概率为：

$$P_{n,s} = \binom{N}{S} (\frac{1}{S})^n (\frac{S-1}{S})^{N-n}$$
那么只有一个用户选择一个RAO的概率为：
$$P_{1,s} = \frac{N}{S}e^{-\frac{N}{S}}$$
则用户重传的概率为：
$$N_{coll} = N(1-e^{-\frac{N}{S}})$$
而这些UE在第k个BO interval选择空闲频段发送的概率为$P_S · P_{BO}$，其中$P_s = 1/S$。
由于每个BO interval都有S个可选择载波，BO interval总数为$\frac{BO}{T_{RAO}}$，那么在第k个interval，上述需要重发的UE在S个子载波上发送的概率密度函数为：
$$
P_{n,s,k} = \binom{N_{coll}}{n} (P_s·P_{BO})^n (1-P_s·P{BO})^{(N_{coll}-n)}
$$
***
**对于二项分布：**
1. **若n很大p很小(n >= 100 && p <= 0.1或n >= 20 && p <= 0.05)则可近似为泊松分布**$P\{X = k\} = \frac{\lambda ^ k e^{-\lambda}}{k!},k = 0,1,2 ...$，$\lambda = np$
2. **若n很大，p不是很小且不接近于0和1(n >= 20)，则可近似为正态分布**
***
因此，对于上述概率密度,可近似为泊松分布,$\lambda = N_{coll}·P_s·P_{BO}$；产生碰撞的概率即为k=0与k=1以外的概率和(与原文献理解有出入)：
$$
P_{coll,s,k} = 1-(1+N_{coll}·P_s·P_{BO})e^{-N_{coll}·P_s·P_{BO}}
$$