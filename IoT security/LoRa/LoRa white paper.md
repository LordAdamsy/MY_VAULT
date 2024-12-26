### 简介
`LoRa`：低功率广域网络(LPWAN)协议，支持低成本的安全双向移动物联网通信，M2M(machine-to-machine)，智慧城市和工业应用
**低功耗 + 大规模设备接入**
端到端加密的物联网

### 流程

完整性保护：空口保护 + HTTPS/VPNs

![[Pasted image 20241219102318.png]]

#### 设备激活
入网(终端设备激活)成功后需在本地保存好DevAddr\[32bit，网络中终端的唯一标识\]，NwkSKey\[保证传输数据完整性\]，AppSKey\[保证数据传输机密性\]用于后续通信
##### ABP(个性化激活，Activation by Personalization)
提前在终端硬编码保存DevAddr，NwkSKey和AppSKey，在整个生命周期中保持不变
##### OTAA(空中激活，Over-the-Air Activation)
终端设备在入网前和服务器端提前约定好AppEUI(JoinEUI)\[不同设备入网使用不同的服务器可以使用应用标识区分\]，DevEUI\[终端唯一设备标识，出厂前就固定到存储器中\]和AppKey\[AES加密算法密钥\]
###### Join-Request
未加密，以AppKey生成的密文的前4字节作为MIC校验
包含终端特征码(DevEUI)，随机数和应用标识
###### Join-Accept
采用APPKey加密，包含：
1. `JoinNonce` 用于计算NwkSKey和AppSKey
2. `NetID` 网络ID，也用于计算NwkSKey和AppSKey
3. `DevAddr` 当前网络中的终端节点唯一标识 32bits

``` 
AppSKey = AES(AppKey, 0x1 + AppNounce + NetID + DevNonce)
NwkSKey = AES(AppKey, 0x2 + AppNounce + NetID + DevNonce)
```

### 安全缺陷

参考：
- LoRa Alliance. 2017. LoRaWAN v1.1 Specification.
- Eef van Es, Harald Vranken, and Arjen Hommersom. 2018. Denial-of-Service Attacks on LoRaWAN. In Proceedings of the 13th International Conference on Availability, Reliability and Security (ARES '18). Association for Computing Machinery, New York, NY, USA, Article 17, 1–6. https://doi.org/10.1145/3230833.3232804

1. 信令漏洞
	3类终端
	- A类：终端开两段定长固定位置的接收窗
	- B类：除A类窗外可开额外接收窗(广播且未加密和签名)
	- C类：不发消息时一直监听
	信令安全性无法得到保障
	
	可能的解决方案：网络侧通过私钥对信令签名保证信令不可伪造
	
2. 下行路由漏洞(卫星物联网场景需要天线对星，不存在此种问题)
3. join-accept重放攻击等
