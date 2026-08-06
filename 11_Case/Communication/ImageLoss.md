# ImageLoss

Version: V1.0

Module: 11_Case / Communication

Status: Released

Severity: ★★★★★

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Dynamic Flat Panel Detector
- Static Flat Panel Detector（GigE）
- Pluto Series
- Gigabit Ethernet Detector

Related Documents:

- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- ../../08_ImageDiagnosis/NoiseArtifact/
- ../../09_DecisionTree/Communication/ImageLoss.md
- ../../17_Tools/Wireshark/
- ../../17_Tools/Ping/

---

# 1. Case Summary

## Case Name

Image Loss

## Description

探测器能够正常连接，但图像采集过程中发生图像丢失。

SDK 或采集软件通常提示：

- Image Loss
- Lost Frame
- Frame Missing
- Acquisition Failed
- Offset Generation Failed（由丢帧引起）

Image Loss 是动态平板、高帧率模式及校准过程中最常见的问题之一。

---

# 2. Applicable Products

适用于：

- Gigabit Ethernet Detector
- Pluto 系列
- 动态平板
- 静态平板（网络传输）

---

# 3. Environment

典型连接方式：

```text
PC
    │
Gigabit Ethernet
    │
Detector
```

或

```text
PC
    │
Switch
    │
Detector
```

---

# 4. Fault Phenomenon

现场常见表现：

- SDK 提示 Image Loss
- 图像连续性中断
- 图像播放卡顿
- 丢失部分 Frame
- Offset 模板生成失败
- Gain 校准失败
- Defect 校准失败

---

# 5. Root Cause Analysis

根据现场经验，Image Loss 主要来源于数据传输异常，而非探测器成像异常。

主要原因包括：

## 5.1 Jumbo Frame 未开启

Gigabit Detector 推荐开启 Jumbo Frame。

若关闭：

可能导致大数据包分片。

产生丢包。

---

## 5.2 Packet Size 设置错误

Packet Size 不符合产品要求。

导致：

- Frame Loss
- Receive Error

---

## 5.3 网卡驱动异常

驱动版本过旧。

驱动兼容性问题。

---

## 5.4 Frame Rate 设置过高

超过 PC 数据处理能力。

超过网络带宽。

导致持续丢帧。

---

## 5.5 节能模式

Windows 网卡节能。

PCIe 节能。

绿色以太网。

均可能影响实时数据传输。

---

## 5.6 网络硬件问题

包括：

- 网线质量差
- 网口接触不良
- 交换机性能不足

---

# 6. Diagnostic Process

建议按以下顺序排查。

---

## Step 1

确认是否稳定复现。

记录：

- 是否每次都发生
- 是否固定位置发生
- 是否高帧率发生

---

## Step 2

检查 Jumbo Frame。

确认：

已开启 Jumbo Frame。

---

## Step 3

检查网卡配置。

确认：

- Packet Size
- Receive Buffer
- Interrupt Moderation
- 节能模式

符合产品要求。

---

## Step 4

检查网卡驱动。

建议：

升级至验证版本。

---

## Step 5

降低 Frame Rate。

现场经验：

若降低帧率后恢复正常。

通常说明：

PC 或网络带宽不足。

---

## Step 6

使用 Wireshark。

观察：

- Packet Loss
- Retransmission
- Receive Error

确认是否存在网络异常。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Image Loss。

### Cause

Jumbo Frame 未开启。

### Solution

开启 Jumbo Frame。

恢复正常。

---

## Case 2

### Phenomenon

Offset Generation Failed。

### Cause

采集过程中发生丢帧。

### Solution

调整网络配置。

重新生成 Offset。

恢复正常。

---

## Case 3

### Phenomenon

动态图像连续丢帧。

### Cause

Frame Rate 设置过高。

### Solution

降低采集帧率。

恢复正常。

---

# 8. Verification

满足以下条件：

- 无 Image Loss 提示
- 连续采集正常
- 校准成功
- 图像完整
- 无连续丢帧

即可判定恢复。

---

# 9. Engineering Experience

## Experience 1

Image Loss 时：

优先检查：

- Jumbo Frame
- 网卡驱动
- Packet Size

不要立即怀疑 Detector。

---

## Experience 2

若同时出现：

- Image Loss
- Offset Generation Failed

通常首先排查网络配置。

---

## Experience 3

降低 Frame Rate 后恢复正常。

多数情况下说明：

PC 配置或网络性能不足。

---

## Experience 4

若网络配置全部正常。

建议进一步抓包分析。

不要仅凭软件提示判断 Detector 故障。

---

# 10. Prevention

建议：

- 使用千兆以上网卡
- 开启 Jumbo Frame
- 使用验证版本驱动
- 禁用网卡节能
- 使用高质量网线
- 校准前确认网络稳定

---

# 11. Related Documents

Workflow：

- ImageTransmissionWorkflow.md

Failure Knowledge：

- CommunicationFailure.md

Decision Tree：

- ImageLoss.md

Tools：

- Wireshark
- Ping

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Image Loss 现场案例及排查经验。 |

