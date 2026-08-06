# Timeout

Version: V1.0

Module: 11_Case / Communication

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector
- Pluto Series

Related Documents:

- ../../06_Workflow/ConnectionWorkflow.md
- ../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- ../../09_DecisionTree/Communication/
- ../../17_Tools/Ping/
- ../../17_Tools/Wireshark/

---

# 1. Case Summary

## Case Name

Communication Timeout

## Description

SDK 或上位机在规定时间内未收到探测器响应，导致通信超时。

Timeout 并不一定表示探测器损坏，而是表示一次正常通信流程未能在规定时间内完成。

---

# 2. Applicable Products

适用于：

- Gigabit Ethernet Detector
- Pluto 系列
- 动态平板
- 静态平板

---

# 3. Fault Phenomenon

现场常见现象：

- Connection Timeout
- Acquisition Timeout
- Detector No Response
- Wait Response Timeout
- SDK 长时间等待
- 图像无法返回

---

# 4. Root Cause Analysis

## 4.1 网络通信异常

包括：

- 网络延迟
- 丢包
- 网络中断

---

## 4.2 Detector 未正常响应

包括：

- Firmware 卡死
- Detector 初始化失败
- Detector Busy

---

## 4.3 SDK 配置异常

例如：

- Timeout 参数过短
- SDK 配置错误
- Detector 配置错误

---

## 4.4 PC 性能不足

包括：

- CPU 占用过高
- 内存不足
- 系统资源不足

---

## 4.5 网络配置错误

包括：

- IP 配置错误
- Jumbo Frame
- Packet Size
- 网卡驱动异常

---

# 5. Diagnostic Process

## Step 1

确认：

Detector 是否 Online。

---

## Step 2

Ping Detector。

观察：

- 是否超时
- 是否丢包
- 延迟是否稳定

---

## Step 3

检查：

- 网卡配置
- Jumbo Frame
- Packet Size

---

## Step 4

检查：

SDK 日志。

确认：

Timeout 发生阶段：

- Connection
- Acquisition
- Image Transfer

---

## Step 5

重新启动：

- SDK
- Detector

再次验证。

---

## Step 6

若仍失败：

抓取网络数据包进行分析。

---

# 6. Typical Field Experience

## Case 1

### Phenomenon

Connection Timeout。

### Cause

IP 配置错误。

### Solution

重新配置网络。

恢复正常。

---

## Case 2

### Phenomenon

Acquisition Timeout。

### Cause

Detector Busy。

### Solution

重新启动 Detector。

恢复正常。

---

## Case 3

### Phenomenon

动态采集频繁 Timeout。

### Cause

Frame Rate 设置过高。

### Solution

降低 Frame Rate。

恢复正常。

---

# 7. Verification

满足以下条件：

- 无 Timeout 提示
- Detector 响应正常
- 图像采集正常
- 连续运行稳定

即可确认故障解决。

---

# 8. Engineering Experience

## Experience 1

Timeout 不等于 Detector 故障。

首先确认：

- 网络
- SDK
- Detector 状态

---

## Experience 2

若 Ping 正常：

优先检查：

- SDK
- Firmware
- License

---

## Experience 3

动态模式 Timeout：

应重点检查：

- Frame Rate
- 网络带宽
- PC 性能

---

## Experience 4

Timeout 与 Image Loss 经常同时出现。

建议联合排查网络配置。

---

# 9. Prevention

建议：

- 固定网络配置
- 使用稳定版本 Firmware
- 定期升级网卡驱动
- 保证 PC 性能满足要求
- 连续运行验证稳定性

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
| V1.0 | 2026-08 | 初版建立，整理 Timeout 通信故障案例。 |