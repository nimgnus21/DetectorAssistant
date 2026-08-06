# DetectorOffline

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
- StartupFailure.md
- ShutdownFailure.md
- CommunicationTimeout.md
- ExposureFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../HardwareFailure/PowerFailure.md
- ../SoftwareFailure/DriverFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../EnvironmentFailure/EMIFailure.md
- ../EnvironmentFailure/PowerQualityFailure.md
- ../../06_Workflow/StartupWorkflow.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Detector Offline 描述数字平板探测器（Flat Panel Detector，FPD）无法被工作站识别、无法建立通信连接或运行过程中突然离线（Offline）的各种故障。

Detector Offline 是现场最常见、影响最大的系统级故障之一，其根因可能来自供电、网络通信、驱动、Firmware、硬件故障或环境干扰。

本文件回答的问题：

> **为什么 Detector 无法连接？为什么运行过程中突然 Offline？如何快速定位 Detector Offline 的真正原因？**

---

# 2. Scope

适用于：

- Factory Test
- Installation
- Acceptance Test
- Preventive Maintenance
- Technical Support
- Field Service

适用于：

- Wired Detector
- Wireless Detector
- Ethernet Communication
- Wireless Communication
- Detector Discovery

---

# 3. What is Detector Offline

Detector Offline 指：

**工作站无法检测到 Detector，或者 Detector 在运行过程中失去连接，导致无法继续完成图像采集及曝光流程。**

主要表现：

- Detector Not Found
- Detector Offline
- Connection Lost
- Device Not Responding
- Cannot Acquire Image
- Exposure Failed

---

# 4. Failure Classification

```text
Detector Offline

├── Startup Offline
├── Runtime Offline
├── Communication Lost
├── Network Configuration Error
├── Firmware Offline
├── Power Loss
└── Hardware Failure
```

---

# 5. Typical Symptoms

## 5.1 Startup Offline

特点：

- 开机后 Detector 不在线
- 软件无法发现 Detector

可能原因：

- 电源未启动
- 网络配置错误
- Firmware 未启动

---

## 5.2 Runtime Offline

特点：

- 正常工作过程中突然离线
- 曝光中断

可能原因：

- 通信中断
- 电源异常
- Firmware Crash

---

## 5.3 Communication Lost

特点：

- Ping 不通
- 网络连接断开

可能原因：

- 网线损坏
- 网口异常
- Switch 故障

---

## 5.4 Network Configuration Error

特点：

- Detector 存在
- 无法建立连接

可能原因：

- IP 地址错误
- 子网掩码错误
- DHCP 配置异常

---

## 5.5 Firmware Offline

特点：

- Detector 上电
- Firmware 无响应

可能原因：

- Firmware Crash
- Boot Failure
- FPGA 初始化失败

---

## 5.6 Power Loss

特点：

- Detector 完全无响应
- LED 熄灭

可能原因：

- Adapter Failure
- Battery Low（Wireless）
- Internal Power Failure

---

## 5.7 Hardware Failure

特点：

- 更换软件后仍 Offline
- 更换电脑仍 Offline

可能原因：

- Main Board Failure
- Communication Board Failure

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Startup Offline | Firmware / Power |
| Runtime Offline | Communication |
| Communication Lost | Cable / Switch |
| Network Error | IP Configuration |
| Firmware Offline | Boot Failure |
| Hardware Offline | Main Board Failure |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Power Module | Detector Cannot Start |
| Communication Board | Link Down |
| Main Board | Offline |
| FPGA | Firmware Not Running |
| Ethernet Interface | No Network Link |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Driver | Detector Not Detected |
| SDK | Connection Failed |
| Firmware | Initialization Failed |
| Application | Offline Alarm |

---

# 9. Relationship with Environment

环境因素可能导致：

- EMI
- Power Quality
- Network Instability
- Temperature Related Restart

因此应同时检查：

- 网络环境
- 电源环境
- 电磁干扰

---

# 10. Diagnostic Workflow

```text
Detector Offline

↓

Power ON？

↓

NO

↓

Power Analysis

↓

YES

↓

Network Link？

↓

NO

↓

Cable / Switch

↓

YES

↓

Ping Detector？

↓

NO

↓

IP Configuration

↓

YES

↓

Firmware Running？

↓

NO

↓

Firmware Analysis

↓

YES

↓

Application Connected？

↓

NO

↓

Driver / SDK

↓

Detector Online
```

---

# 11. Detection Methods

## Power Verification

检查：

- LED
- Power Indicator
- Internal Voltage

---

## Network Verification

检查：

- Link LED
- Ping
- ARP
- Ethernet Status

---

## IP Configuration

检查：

- IP Address
- Subnet Mask
- Gateway

---

## Firmware Verification

检查：

- Boot Log
- Firmware Version
- FPGA Status

---

## Application Verification

检查：

- Driver
- SDK
- Detector Discovery
- Error Log

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Detector Not Found After Installation | IP Configuration Error |
| Detector Randomly Offline | Communication Failure |
| Offline During Exposure | Power Failure |
| Detector Cannot Ping | Network Failure |
| Firmware Update Causes Offline | Firmware Failure |
| Detector Offline After Lightning | Hardware Damage |

---

# 13. Engineering Recommendations

建议：

- 优先检查供电及网络连接。
- 确认 Detector 与工作站网络参数一致。
- 使用 Ping、ARP 等工具验证通信状态。
- 查看 Firmware 是否正常启动。
- 更换网线、交换机或工作站进行交叉验证。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## StartupFailure

启动失败可能导致 Detector Offline。

---

## CommunicationTimeout

通信超时通常是 Offline 的前兆。

---

## CommunicationFailure

分析底层通信故障。

---

## PowerFailure

供电异常可能导致 Detector 掉线。

---

## DecisionTree

Detector Offline 是现场服务中最重要的诊断入口之一。

---

# 15. Knowledge Graph

```text
Detector Offline

├── Startup Offline
├── Runtime Offline
├── Communication Lost
├── Network Error
├── Firmware Offline
├── Power Failure
└── Hardware Failure

↓

Power Verification

↓

Network Verification

↓

Firmware Verification

↓

Application Verification

↓

Hardware Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Detector Offline 是 Flat Panel Detector 最常见的系统级故障之一，涉及供电、网络通信、Firmware、驱动、应用程序及硬件等多个层面。其典型表现包括设备无法发现、运行中掉线、曝光中断及无法采集图像。通过供电检查、网络验证、Firmware 状态确认、应用连接验证及交叉测试，可快速定位 Offline 根因，并结合 Hardware Failure、Software Failure、Environment Failure 与 DecisionTree 建立完整的 Detector Offline 故障分析体系。