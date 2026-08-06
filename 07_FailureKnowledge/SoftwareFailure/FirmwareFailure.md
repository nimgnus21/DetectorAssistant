# FirmwareFailure

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
- DriverFailure.md
- ../HardwareFailure/FPGAFailure.md
- ../../03_Hardware/FPGA.md
- ../../06_Workflow/PowerOnWorkflow.md
- ../../06_Workflow/AcquisitionWorkflow.md
- ../../06_Workflow/ShutdownWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Firmware Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Firmware（固件）的典型故障模式、形成机理、系统表现、检测方法及根因分析。

Firmware 是 Detector 软件系统中最底层的软件，运行于 FPGA、MCU 或其他控制器之上，负责完成系统初始化、硬件控制、状态管理、图像采集控制、通信协议处理及异常监测。

Firmware 连接上层 Driver 与底层 Hardware，是整个 Detector 正常运行的核心软件。

本文件回答的问题：

> **Firmware 为什么会发生故障？故障后会导致哪些系统及图像异常？**

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于：

- FPGA Firmware
- MCU Firmware
- Bootloader
- Embedded Controller

---

# 3. Firmware Overview

Firmware 的主要职责：

- System Initialization
- Hardware Initialization
- Power Management
- Timing Control
- Acquisition Control
- Readout Control
- Communication Processing
- Status Monitoring
- Error Reporting

系统位置：

```text
Host Software

↓

SDK

↓

Driver

↓

Firmware

↓

FPGA / MCU

↓

Hardware
```

Firmware 是连接软件系统与硬件系统的重要桥梁。

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| Firmware Corruption | 固件损坏 |
| Boot Failure | 启动失败 |
| Initialization Failure | 初始化失败 |
| Configuration Error | 配置错误 |
| Timing Failure | 时序异常 |
| State Machine Failure | 状态机异常 |
| Communication Processing Failure | 通信处理异常 |
| Resource Overflow | 资源溢出 |
| Watchdog Reset | 看门狗复位 |
| Firmware Version Mismatch | 固件版本不匹配 |

---

# 5. Failure Mechanisms

## 5.1 Firmware Corruption

固件文件损坏或加载失败。

影响：

- Firmware 无法运行
- Detector 无法启动

典型表现：

- Boot Failure
- Firmware Checksum Error

---

## 5.2 Boot Failure

Bootloader 无法正常加载 Firmware。

影响：

- 系统停留在启动阶段

典型表现：

- 无法 Ready
- Detector Offline

---

## 5.3 Initialization Failure

初始化流程异常。

包括：

- FPGA 初始化
- Memory 初始化
- Communication 初始化

典型表现：

- Initialization Failed
- Hardware Not Ready

---

## 5.4 Configuration Error

配置参数错误。

影响：

- 模块工作异常

典型表现：

- Calibration Failure
- Communication Failure

---

## 5.5 Timing Failure

内部控制时序异常。

影响：

- Acquisition Error
- Readout Error

典型表现：

- 图像异常
- Workflow 中断

---

## 5.6 State Machine Failure

状态切换异常。

影响：

- Workflow 无法继续执行

典型表现：

- Detector 卡死
- 无法退出 Busy 状态

---

## 5.7 Communication Processing Failure

通信协议处理异常。

影响：

- 指令无法执行
- 状态返回错误

典型表现：

- Timeout
- Invalid Response

---

## 5.8 Resource Overflow

缓存、队列或内存资源耗尽。

影响：

- Firmware 崩溃
- 数据丢失

---

## 5.9 Watchdog Reset

Firmware 长时间无响应。

影响：

- 系统自动复位

典型表现：

- Detector 自动重启
- 日志出现 Watchdog Reset

---

## 5.10 Firmware Version Mismatch

Firmware 与 Driver、SDK 或 FPGA 版本不匹配。

影响：

- 功能异常
- 通信异常

典型表现：

- 部分功能不可用
- 升级后异常

---

# 6. Typical Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| Detector Cannot Start | Boot Failure |
| Initialization Failed | Initialization Failure |
| Detector Busy Forever | State Machine Failure |
| Image Acquisition Failed | Timing Failure |
| Communication Timeout | Communication Processing Failure |
| Random Restart | Watchdog Reset |
| Feature Not Available | Version Mismatch |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| Power On | 初始化失败 |
| Acquisition | 图像采集失败 |
| Readout | 数据读取异常 |
| Communication | 通信异常 |
| Entire System | Detector 无法正常运行 |

---

# 8. Detection Methods

## Firmware Version Check

检查：

- Firmware Version
- Build Date
- Version Compatibility

---

## System Log

检查：

- Boot Log
- Initialization Log
- Error Log
- Exception Log

---

## Watchdog Status

检查：

- Reset Count
- Reset Reason

---

## Communication Test

验证：

- Command Response
- Status Response
- Error Code

---

## Firmware Upgrade Verification

检查：

- Firmware Integrity
- Checksum
- Upgrade Result

---

# 9. Root Cause Analysis

```text
Detector Failure

↓

Boot Success？

↓

NO

↓

Firmware Corruption

↓

YES

↓

Initialization Success？

↓

NO

↓

Configuration Error

↓

YES

↓

Workflow Normal？

↓

NO

↓

Timing / State Machine Failure

↓

YES

↓

Check Driver
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Upgrade Interrupted | 固件升级中断 |
| Firmware Corruption | 固件损坏 |
| Wrong Firmware Version | 固件版本错误 |
| Configuration Loss | 配置丢失 |
| Watchdog Reset | 程序异常复位 |
| Logic Bug | 固件逻辑缺陷 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单一功能异常 |
| Moderate | Workflow 中断 |
| Major | Detector 无法采集 |
| Critical | Detector 无法启动 |

---

# 12. Engineering Recommendations

建议：

- 保持 Firmware、Driver、SDK 版本一致。
- 升级 Firmware 前备份配置及 Calibration 数据。
- 升级完成后验证 Firmware Checksum。
- 收集完整 System Log 后进行分析。
- 排除 FPGA、Power、Memory 等硬件故障后，再确认 Firmware 故障。

---

# 13. Relationship with Other Modules

## DriverFailure

Driver 调用 Firmware 提供的功能接口。

---

## FPGAFailure

Firmware 控制 FPGA 工作流程。

---

## PowerOnWorkflow

Firmware 完成系统初始化。

---

## AcquisitionWorkflow

Firmware 控制曝光与采集流程。

---

## DecisionTree

Firmware Failure 是以下诊断的重要节点：

- Detector Cannot Start
- Initialization Failed
- Busy State
- Communication Timeout
- Watchdog Reset

---

# 14. Knowledge Graph

```text
Bootloader

↓

Firmware

├── Boot Failure
├── Initialization Failure
├── Configuration Error
├── Timing Failure
├── State Machine Failure
├── Communication Failure
├── Resource Overflow
├── Watchdog Reset
└── Version Mismatch

↓

FPGA / MCU

↓

Hardware

↓

Workflow

↓

System Symptoms

↓

DecisionTree
```

---

# 15. Summary

Firmware Failure 是 Flat Panel Detector 软件系统中最底层、最关键的软件故障之一，其主要表现为启动失败、初始化异常、时序错误、状态机异常、通信处理异常及版本不匹配等。由于 Firmware 控制整个 Detector 的运行流程，因此故障通常影响系统初始化、图像采集、通信控制及设备状态管理。故障分析应结合 Firmware Version、System Log、Watchdog 状态、Configuration 及硬件状态进行综合判断，为 DecisionTree 和现场维修提供可靠依据。