## NB-IoT
3GPP为物联网（IoT）定义了几种关键的随机接入（Random Access, RA）技术，这些技术主要针对NB-IoT系统。NB-IoT的随机接入过程对于初始接入建立无线链路和调度请求至关重要，它包括多个步骤，如UE发送随机接入前导码、网络发送随机接入响应、UE传输其身份信息以及网络发送争用解决消息等 。

NB-IoT的随机接入信道（NPRACH）是新设计的，因为传统的LTE PRACH带宽为1.08 MHz，超出了NB-IoT上行链路带宽。NPRACH前导码由4个符号组构成，每个符号组包括一个CP和5个符号，采用单音频率跳变波形 。为了支持覆盖扩展，NPRACH前导码可以重复多达128次 。

## NB-IoT/NTN
在3GPP Release 17中，启动了针对IoT的非地面网络（NTN）的研究项目，以评估和调整NB-IoT空中接口以适应NTN的特点。这项研究的一个主要目标是评估随机接入过程以及在卫星上估计上行同步参数 。在卫星通信中，由于存在较大的时间到达（ToA）和载波频率偏移（CFO），传统的地面网络设计方法可能无法提供准确的估计性能。为了解决这个问题，有研究提出了一种基于非采样二进制小波变换的新算法，该方法能够在不先补偿CFO的情况下检测传入的前导码并估计它们的时间到达 。

此外，还有研究关注于提高NB-IoT系统中NPRACH性能，包括检测率、虚警率和到达时间估计的准确性。这些研究通过模拟结果展示了NB-IoT系统的整体潜力 。

### 相关3GPP技术报告与技术规范

1. **3GPP TR 36.763**：研究NB-IoT/eMTC对非地面网络（NTN）的支持。该文档详细讨论了在NTN环境中部署NB-IoT和eMTC时需要考虑的各种方面，包括物理层的调整、随机接入过程、以及与现有3GPP网络的兼容性等。

2. **3GPP TS 36.304**：描述了E-UTRA（Evolved Universal Terrestrial Radio Access）用户设备在空闲模式下的程序，包括与随机接入过程相关的要求。

3. **3GPP TS 45.820**:描述了3GPP对于低吞吐量物联网的支持，主要面向机器类型通信（MTC）设备，包括随机接入、评估方法、物理层设计等，特别是那些对成本、能耗和网络覆盖有特别需求的应用场景。

4. **3GPP TS 36.213**:详细规定了E-UTRA系统中物理层的程序，包括同步过程、功率控制、随机接入等。

5. 《NB-IoT Random Access for Non-Terrestrial Networks: Preamble Detection and Uplink Synchronization》研究了NB-IoT在NTN环境下的随机接入技术，特别是针对卫星信道损伤的解决方案。

6. 《A Primer on 3GPP Narrowband Internet of Things (NB-IoT)》描述了NB-IoT的随机接入、资源映射、调度与HARQ等方法。





## TS 36.304

全称为 "Evolved Universal Terrestrial Radio Access (E-UTRA); User Equipment (UE) procedures in idle mode"。详细规定了UE在空闲模式下的无线接入网（RAN）部分的程序，包括但不限于以下几个主要内容：

1. **PLMN选择**：UE在开机时应选择公共陆地移动网络（PLMN），并根据NAS（非接入层）提供的信息选择相关RAT（无线接入技术）。

2. **小区选择与重选**：UE应根据空闲模式下的测量和小区选择标准选择合适的小区进行驻留。当UE在当前小区上驻留时，应定期搜索更好的小区，并根据小区重选标准进行重选。

3. **小区状态与预留**：文档中定义了小区状态和预留机制，允许运营商对小区选择和重选过程进行控制。

4. **接入控制**：定义了基于访问类别或ACDC类别的接入控制机制，以进行负载控制。

5. **紧急呼叫**：如果需要，可以限制紧急呼叫，UE在驻留的小区中根据特定的字段判断是否允许发起紧急呼叫。

6. **测量与报告**：UE应执行测量以支持小区选择和重选，并在满足特定条件时将测量结果报告给网络。

7. **系统信息的接收与监控**：UE应监控小区广播的系统信息，并在系统信息发生变化时进行相应的处理。

8. **MBMS（多媒体广播/多播服务）**：UE应根据规范接收MBMS服务，并在进入新的MBSFN区域或SC-PTM传输区域时获取相应的控制信息。

9. **Sidelink操作**：包括Sidelink通信、V2X Sidelink通信、Sidelink发现和同步过程，以及Sidelink小区选择和重选。

10. **日志测量和可接入性测量**：UE可以配置在RRC_IDLE模式下记录测量结果，并在RRC连接建立过程失败时记录相关信息。

11. **移动性历史信息**：UE存储其曾经服务的小区的历史信息。


## TS 36.213

全称为 "Evolved Universal Terrestrial Radio Access (E-UTRA); Physical layer procedures"。它详细规定了E-UTRA系统中物理层的程序，主要内容包括：

1. **同步过程**：包括小区搜索和定时同步，UE通过这些过程与小区建立时间和频率同步 。

2. **功率控制**：涉及上行链路功率控制，以及与NPUSCH（Narrowband Physical Uplink Shared Channel）相关的功率头寸 。

3. **随机接入过程**：定义了UE如何通过PRACH（Physical Random Access Channel）进行随机接入，以及与NPRACH（Narrowband Physical Random Access Channel）相关的程序 。

4. **物理下行共享信道（PDSCH）相关过程**：包括CQI（Channel Quality Indicator）报告和MIMO反馈机制。

5. **物理上行共享信道（PUSCH）相关过程**：涉及UE探测和HARQ（Hybrid Automatic Repeat Request）ACK/NACK检测。

6. **物理下行共享控制信道（PDCCH）过程**：包括共享信道分配。

7. **多点传送相关过程**：涉及多小区传输的物理层程序。

8. **物理层测量**：包括UE和E-UTRAN中的物理层测量，测量结果的报告，切换测量，空闲模式测量等 。

9. **物理信道和调制**：涉及物理资源的定义和结构，物理信号的产生方法，以及上行和下行物理层信道的定义、结构、帧格式 。

10. **复用和信道编码**：描述了传输信道和控制信道数据的处理，包括复用技术，信道编码方案，以及第一层/第二层控制信息的编码、交织和速率匹配过程 。

11. **中继节点程序**：描述了物理信道和调制，复用和信道编码，中继节点程序 。

12. **NB-IoT 相关程序流程**：Release 13 及以后版本中，针对窄带物联网技术，包括同步程序、功率控制、随机接入程序、NB-PDSCH 和 NB-PUSCH 相关程序等 。

