# Ping

## Purpose

用于验证主机与探测器之间的基础 IP 连通性，并记录响应、丢包和延迟。

## Use When

- 初始网络配置完成后
- Detector not found / Unable to connect
- 间歇性连接异常
- 怀疑网络不稳定或数据传输异常

## Standard Output

记录：

- Target IP
- Test time
- Reply status
- Packet loss
- Latency summary

## Escalation

- 无响应：检查物理连接、IP/Subnet 与 Connection DecisionTree
- 存在丢包：进入 Packet Loss 排查，必要时使用 Wireshark

## Related Documents

- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [Connection DecisionTree](../../09_DecisionTree/Connection/)
- [Unable To Connect](../../07_FailureKnowledge/ConnectionFailure/UnableToConnect.md)
- [Packet Loss](../../07_FailureKnowledge/ImageFailure/PacketLoss.md)
- [Wireshark](../Wireshark/README.md)
