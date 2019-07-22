### 产品设计总结
```
  总结主要从应用无感知、功能、稳定性和操作四方面梳理。
```

**1、应用无感知**
- 产品接入客户网络，不影响现有业务正常使用，内网上网对新加入设备无感知；
- 自适应环境
  - 产品应用到客户场景，三个主要输入：电源、网络数据和操作数据；
    - 应对电源故障需要有相关灾备机制；
      - 主要针对日志数据和配置数据的备份恢复；
        - 涉及到不完整数据截断丢弃
    - 应对数据需要满足任何极端场景，极端情况硬件资源发挥到极致；
      - 软件bypass，功能失效，平台（数据面或内核）直接转发；
        - 快速数据通道，新流直接转发，活跃流继续处理；
      - 硬件bypass，直接物理直连转发；
      - 数据冲击缓冲，自适应调整；
    - 应对操作数据需要防设备被入侵和操作异常导致系统崩溃
      - 操作关联用户权限控制；
      - 防入侵机制；
**2、功能**
- 产品满足客户场景痛点解决方案，具备功能进行问题分析、处理和维持；
- 客户问题来源于输入的网络数据，需具备数据分析、特征和行为采集，结合相关策略处理，同时输出分析和结果数据；
- 产品自身功能，主要输出系统运行数据展示，系统运行情况透明；
**3、稳定性**

**4、操作**