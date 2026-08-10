# Wireshark

## Purpose

用于在网络层面保留数据传输异常证据，重点服务于疑似丢包、异常流量或图像传输中断问题。

## Use When

- Ping 已提示丢包或网络不稳定
- 图像出现疑似数据缺失条带
- 连接/采图存在间歇性中断
- 需要将网络证据提供给进一步分析

## Required Evidence

记录：

- 抓包时间窗口
- Host / Detector IP
- 复现步骤
- 相关 Detector.log
- 异常图像（如适用）

## Boundary

Wireshark 只用于确认网络传输方向，不应仅凭抓包结果直接判定探测器硬件故障。

## Related Documents

- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Packet Loss](../../07_FailureKnowledge/ImageFailure/PacketLoss.md)
- [Connection DecisionTree](../../09_DecisionTree/Connection/)
- [Ping](../Ping/README.md)
