# NetworkConfiguration

Version: V1.0

Module: 11_Case / Communication

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Wired Detector
- Wireless Detector（AP Mode）
- Pluto Series
- Gigabit Ethernet Detector

Related Documents:

- ../../06_Workflow/ConnectionWorkflow.md
- ../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- ../../09_DecisionTree/Communication/
- ../../17_Tools/Ping/
- ../../17_Tools/Wireshark/

---

# 1. Case Summary

## Case Name

Network Configuration Error

## Description

由于网络参数配置错误导致探测器无法正常通信或数据传输异常。

网络配置问题是现场支持中最常见的故障来源之一，既可能导致 **Connection Failed**，也可能导致 **Image Loss**、**Timeout** 等问题。

---

# 2. Applicable Products

适用于：

- 有线 Gigabit Ethernet 探测器
- 无线 AP Mode 探测器
- Pluto 系列
- SDK_AIO

---

# 3. Fault Phenomenon

现场常见现象：

- Detector Offline
- Connection Failed
- Ping Failed
- Image Loss
- Timeout
- Offset Generation Failed
- Gain Generation Failed

---

# 4. Root Cause Analysis

## 4.1 IP 地址配置错误

最常见原因。

包括：

- IP 不在同一网段
- 修改了错误网卡
- IP 冲突

---

## 4.2 AP Mode 配置错误

无线连接时：

修改了有线网卡。

没有修改无线网卡。

---

## 4.3 Jumbo Frame 未开启

导致：

- 图像丢包
- 校准失败
- 动态图像异常

---

## 4.4 Packet Size 设置错误

数据包大小不符合要求。

导致：

- Image Loss
- Receive Error

---

## 4.5 网卡驱动问题

包括：

- 驱动版本过旧
- 驱动异常
- 驱动兼容性问题

---

## 4.6 节能模式

包括：

- Energy Efficient Ethernet
- Green Ethernet
- 网卡节能

可能导致通信中断。

---

# 5. Diagnostic Process

## Step 1

确认连接方式：

- Wired
- AP Mode

---

## Step 2

确认修改的是正确网卡。

> **现场经验：**
>
> 探测器连接失败时，只需要修改当前连接探测器的网卡 IP，其余网卡保持不变。

AP Mode：

修改无线网卡。

---

## Step 3

检查：

- IP Address
- Subnet Mask

---

## Step 4

检查 Jumbo Frame。

确认：

已开启。

---

## Step 5

检查 Packet Size。

确认符合产品要求。

---

## Step 6

检查：

- 网卡驱动
- 节能配置

必要时升级驱动。

---

## Step 7

Ping Detector。

确认：

- 是否可达
- 是否稳定
- 是否丢包

---

# 6. Typical Field Experience

## Case 1

### Phenomenon

Connection Failed。

### Cause

修改了错误网卡。

### Solution

修改当前连接 Detector 的网卡。

恢复正常。

---

## Case 2

### Phenomenon

无线无法连接。

### Cause

AP Mode 修改了有线网卡。

### Solution

修改无线网卡。

恢复正常。

---

## Case 3

### Phenomenon

Image Loss。

### Cause

Jumbo Frame 未开启。

### Solution

开启 Jumbo Frame。

恢复正常。

---

## Case 4

### Phenomenon

Offset Generation Failed。

### Cause

Packet Size 设置异常。

### Solution

恢复推荐配置。

重新校准。

---

# 7. Verification

确认：

- Ping 正常
- Detector Online
- SDK 正常连接
- 图像采集正常
- 校准成功

---

# 8. Engineering Experience

## Experience 1

不要修改所有网卡。

只修改：

当前连接 Detector 的网卡。

---

## Experience 2

AP Mode：

修改无线网卡。

---

## Experience 3

Image Loss 时：

优先检查：

- Jumbo Frame
- Packet Size
- 网卡驱动

---

## Experience 4

网络配置恢复后：

建议重新启动 SDK。

---

# 9. Prevention

建议：

- 固定网络配置
- 使用统一网卡驱动版本
- 禁止节能模式
- 使用高质量网线
- 建立网络配置检查表

---

# 10. Related Documents

Workflow：

- ConnectionWorkflow.md

Failure Knowledge：

- CommunicationFailure.md

Decision Tree：

- Communication/

Tools：

- Ping
- Wireshark

---

# 11. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理网络配置相关现场案例。 |