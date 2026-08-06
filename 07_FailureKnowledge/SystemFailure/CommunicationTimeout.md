# CommunicationTimeout

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- DetectorOffline.md
- StartupFailure.md
- ExposureFailure.md
- WorkflowFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../SoftwareFailure/DriverFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../EnvironmentFailure/EMIFailure.md
- ../EnvironmentFailure/PowerQualityFailure.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Communication Timeout 描述数字平板探测器（Flat Panel Detector，FPD）在通信过程中由于规定时间内未收到预期响应而导致的各种超时故障，包括设备发现超时、连接超时、命令响应超时、图像传输超时及心跳超时等问题。

通信超时通常不是最终故障，而是系统运行异常的表现，需要进一步分析网络、Firmware、Driver、SDK、硬件及环境等多个层面的根本原因。

本文件回答的问题：

> **为什么 Detector 可以连接但总是超时？为什么曝光后一直等待图像？为什么通信偶尔正常、偶尔超时？**

---

# 2. Scope

适用于：

- Factory Test
- Reliability Test
- Installation
- Technical Support
- Field Service

适用于：

- Ethernet Communication
- Wireless Communication
- SDK Communication
- Driver Communication
- Firmware Communication

---

# 3. What is Communication Timeout

Communication Timeout 指：

**通信双方在规定时间内未完成预期的数据交换，从而触发 Timeout 机制并终止当前通信流程。**

主要表现：

- Connection Timeout
- Command Timeout
- Heartbeat Timeout
- Image Receive Timeout
- Exposure Timeout
- Detector Offline

---

# 4. Failure Classification

```text
Communication Timeout

├── Detector Discovery Timeout
├── Connection Timeout
├── Command Response Timeout
├── Image Transfer Timeout
├── Heartbeat Timeout
├── Exposure Timeout
└── SDK Timeout
```

---

# 5. Typical Symptoms

## 5.1 Detector Discovery Timeout

特点：

- 搜索 Detector 时间过长
- 无法发现设备

可能原因：

- Network Configuration Error
- Broadcast Failure

---

## 5.2 Connection Timeout

特点：

- 建立连接失败
- TCP 握手失败

可能原因：

- Network Failure
- Firewall
- Driver Failure

---

## 5.3 Command Response Timeout

特点：

- 命令发送成功
- Detector 无响应

可能原因：

- Firmware Busy
- FPGA Exception

---

## 5.4 Image Transfer Timeout

特点：

- 曝光结束
- 图像迟迟未返回

可能原因：

- Network Congestion
- Packet Loss
- Detector Processing Delay

---

## 5.5 Heartbeat Timeout

特点：

- Detector 突然 Offline
- 心跳丢失

可能原因：

- Communication Interrupted
- Firmware Restart

---

## 5.6 Exposure Timeout

特点：

- 曝光流程停止
- 软件等待超时

可能原因：

- Trigger Failure
- Image Generation Failure

---

## 5.7 SDK Timeout

特点：

- SDK API 返回 Timeout
- 应用程序等待失败

可能原因：

- Driver Failure
- Internal Communication Error

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Discovery Timeout | Network Configuration |
| Connection Timeout | Driver / Network |
| Command Timeout | Firmware |
| Image Timeout | Image Transmission |
| Heartbeat Timeout | Detector Restart |
| SDK Timeout | Driver Exception |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Communication Board | Packet Loss |
| Main Board | Detector Restart |
| FPGA | No Command Response |
| Power Module | Random Timeout |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| SDK | API Timeout |
| Driver | Connection Timeout |
| Firmware | Response Timeout |
| Application | Waiting Timeout |

---

# 9. Relationship with Environment

环境因素可能导致：

- EMI
- Network Interference
- Power Quality
- Switch Failure

因此需要检查：

- 网络设备
- 网线质量
- 接地状态
- 电源稳定性

---

# 10. Diagnostic Workflow

```text
Communication Timeout

↓

Detector Online？

↓

NO

↓

Detector Offline Analysis

↓

YES

↓

Network Normal？

↓

NO

↓

Network Inspection

↓

YES

↓

Command Response？

↓

NO

↓

Firmware Analysis

↓

YES

↓

Image Returned？

↓

NO

↓

Transmission Analysis

↓

YES

↓

SDK Analysis
```

---

# 11. Detection Methods

## Network Test

检查：

- Ping
- Packet Loss
- Network Delay

---

## Communication Log

检查：

- Timeout Position
- Error Code
- Retry Count

---

## Firmware Log

检查：

- Command Queue
- Processing Status
- Exception Log

---

## SDK Log

检查：

- API Return Value
- Timeout Event
- Retry Mechanism

---

## Packet Capture

使用 Wireshark 分析：

- TCP
- UDP
- Retransmission
- Lost Packet

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Detector Found but Cannot Connect | Connection Timeout |
| Exposure Finished but No Image | Image Transfer Timeout |
| Detector Randomly Offline | Heartbeat Timeout |
| SDK Waits Forever | API Timeout |
| Only Large Images Timeout | Network Congestion |
| Timeout After Firmware Upgrade | Firmware Processing Delay |

---

# 13. Engineering Recommendations

建议：

- 优先确认 Detector 是否在线。
- 检查网络质量、交换机及网线状态。
- 使用 Wireshark 抓包分析通信过程。
- 查看 Firmware Log 与 SDK Log。
- 检查 Timeout 参数是否符合产品规格。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## DetectorOffline

Heartbeat Timeout 最终可能导致 Offline。

---

## ExposureFailure

曝光失败可能表现为图像接收超时。

---

## CommunicationFailure

通信异常是 Timeout 的主要根因。

---

## EMIFailure

EMI 可导致数据包丢失及超时。

---

## DecisionTree

Communication Timeout 是系统通信分析的重要入口。

---

# 15. Knowledge Graph

```text
Communication Timeout

├── Discovery Timeout
├── Connection Timeout
├── Command Timeout
├── Image Transfer Timeout
├── Heartbeat Timeout
├── Exposure Timeout
└── SDK Timeout

↓

Network Verification

↓

Communication Log

↓

Firmware Log

↓

SDK Log

↓

Hardware Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Communication Timeout 是 Flat Panel Detector 系统中最常见的通信类故障之一，包括设备发现超时、连接超时、命令响应超时、图像传输超时、心跳超时及 SDK 超时等。其根因可能涉及网络、通信硬件、Firmware、Driver、SDK 或环境干扰。通过网络测试、通信日志分析、Firmware 日志、SDK 日志及抓包分析，可快速定位 Timeout 根因，并结合 Detector Offline、Communication Failure、Exposure Failure 与 DecisionTree 建立完整的通信故障分析体系。