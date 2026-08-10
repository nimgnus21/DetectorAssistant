# Tools

## Purpose

现场工具模块用于把具体诊断工具接入技术支持流程。工具不是独立知识终点，应从故障现象、DecisionTree 或 SOP 进入，并输出可用于验证、定位或升级分析的证据。

## Tool Map

| Tool | Primary Use | Typical Entry |
|---|---|---|
| SDKTool | SDK、校正、固件、License、模式配置 | Software / Calibration / Firmware |
| Ping | 连通性基础验证 | Connection / UnableToConnect |
| Wireshark | 网络通信与数据包分析 | PacketLoss / Communication |
| Offset Viewer | Offset 图像检查 | HorizontalLine / Calibration |
| ImageJ | 图像测量与异常特征分析 | Image Failure |
| Log Viewer | Debug Log / 软件日志分析 | Software Failure / Error Code |
| FTP | 文件传输与现场资料获取 | Log / Firmware / Remote Support |
| Hex | 原始数据与文件内容检查 | Advanced Analysis / Escalation |

## Recommended Use Path

```text
Customer Symptom
    ↓
FailureKnowledge / DecisionTree
    ↓
Select Tool
    ↓
Collect or Analyze Evidence
    ↓
Verification
    ↓
Case or Escalation
```

## Key Cross-links

- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [Decision Tree](../09_DecisionTree/README.md)
- [Image Troubleshooting SOP](../10_SOP/ImageTroubleshooting.md)
- [Network Configuration SOP](../10_SOP/NetworkConfiguration.md)
- [Calibration SOP](../10_SOP/Calibration.md)
- [Firmware Upgrade SOP](../10_SOP/FirmwareUpgrade.md)
- [Case Module](../11_Case/README.md)

## Maintenance Rule

新增工具或工具文档时，必须补充：

1. 适用故障场景。
2. 输入文件或前置条件。
3. 操作目标。
4. 输出结果。
5. 正常判定标准。
6. 异常或无法判定时的升级方向。
7. 关联的 FailureKnowledge、DecisionTree 或 SOP。
