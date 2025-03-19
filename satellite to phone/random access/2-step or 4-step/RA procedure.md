## 2-step（TS 38.321-i30）
### 2-step随机接入的资源选择
.
├─ if CFRA的资源已配置(*rach-ConfigDedicated*)并且至少1个SSB的SS-  │   RSRP超过*msgA-RSRP-ThresholdSSB*，则执行CFRA流程，并选择前导码组
│ └─ 
├─ else CBRA
│	├─ 若有SSB符合条件则选取，否则任选SSB
│	├─ 根据负载大小等参数选择前导码组(若未曾选过)，若选过则选取同样│   │  的前导码组
│	├─ 随机选取与SSB相关的前导码