# SoftwareFailure

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Parent Module:
- 07_FailureKnowledge

Related Modules:
- ../HardwareFailure/
- ../../06_Workflow/
- ../../05_Calibration/
- ../../09_DecisionTree/
- ../../10_FAQ/

---

# 1. Purpose

Software Failure 模块用于描述数字平板探测器（Flat Panel Detector，FPD）软件系统的典型故障、形成原因、表现形式、诊断方法及处理思路。

与 Hardware Failure 不同，本模块重点关注：

- Firmware
- Driver
- SDK
- Calibration
- Configuration
- Communication
- Software Upgrade

等软件系统异常。

本模块回答的问题：

> **Detector 软件系统为什么会发生故障？如何快速定位软件问题？**

---

# 2. Scope

适用于：

- Detector Firmware
- Detector Driver
- Detector SDK
- Calibration Software
- Configuration System
- Communication Software
- Upgrade System

适用于：

- Factory Test
- Engineering Debug
- Software Development
- Field Service
- Technical Support

---

# 3. Module Objectives

Software Failure 模块旨在建立完整的软件故障知识体系，实现：

- 软件故障分类标准化
- 软件异常定位流程统一
- 软件问题快速排查
- 软件与硬件故障区分
- DecisionTree 提供知识支持
- Workflow 提供异常定位依据

---

# 4. Software Architecture Overview

Detector 软件系统可分为以下几个层级：

```text
Host Application

↓

SDK

↓

Detector Driver

↓

Communication Protocol

↓

Firmware

↓

FPGA

↓

Hardware
```

各层职责如下：

| Layer | Responsibility |
|--------|----------------|
| Host Application | 图像采集、控制及用户交互 |
| SDK | API 调用与设备控制 |
| Driver | 操作系统驱动与设备接口 |
| Communication | 数据传输与协议解析 |
| Firmware | Detector 内部控制逻辑 |
| FPGA | 数字控制与图像处理 |
| Hardware | 信号采集与硬件执行 |

---

# 5. Software Failure Classification

Software Failure 分为以下几类：

| Category | Description |
|----------|-------------|
| Firmware Failure | 固件异常 |
| Driver Failure | 驱动异常 |
| SDK Failure | SDK 调用异常 |
| Calibration Failure | 校准软件异常 |
| Configuration Failure | 配置异常 |
| Communication Failure | 通信异常 |
| Upgrade Failure | 软件升级异常 |

各文档分别描述对应软件模块的故障模式及诊断方法。

---

# 6. Relationship with Hardware Failure

软件故障与硬件故障经常具有相似表现，但根因不同。

例如：

| Symptom | Possible Software Cause | Possible Hardware Cause |
|----------|-------------------------|-------------------------|
| Detector Cannot Start | Firmware Failure | Power Failure |
| Image Missing | SDK Failure | FPGA Failure |
| Communication Timeout | Driver Failure | Main Board Failure |
| Calibration Failed | Configuration Failure | TFT Failure |
| Image Corruption | Firmware Failure | Memory Failure |

因此，在故障分析时，应结合 Software 与 Hardware 两个模块进行综合判断。

---

# 7. Relationship with Workflow

Software Failure 与 Workflow 密切相关。

对应关系如下：

| Workflow | Related Software Failure |
|----------|--------------------------|
| PowerOnWorkflow | Firmware Failure |
| ConnectionWorkflow | Driver Failure |
| CommunicationWorkflow | Communication Failure |
| AcquisitionWorkflow | Firmware Failure |
| ReadoutWorkflow | Firmware / SDK Failure |
| CalibrationWorkflow | Calibration Failure |
| ImageGenerationWorkflow | SDK Failure |
| ImageTransmissionWorkflow | Communication Failure |
| ShutdownWorkflow | Firmware Failure |

Workflow 用于确定故障发生阶段。

Software Failure 用于确定软件根因。

---

# 8. Relationship with DecisionTree

DecisionTree 中的软件诊断主要包括：

```text
Detector Cannot Connect

↓

Driver

↓

SDK

↓

Communication

↓

Firmware

↓

Hardware
```

以及：

```text
Calibration Failed

↓

Configuration

↓

Firmware

↓

Hardware
```

Software Failure 为 DecisionTree 提供软件层诊断依据。

---

# 9. Document Navigation

Software Failure 模块包含以下文档：

| Document | Description |
|-----------|-------------|
| FirmwareFailure.md | 固件故障分析 |
| DriverFailure.md | 驱动故障分析 |
| SDKFailure.md | SDK 故障分析 |
| CalibrationFailure.md | 校准软件故障分析 |
| ConfigurationFailure.md | 配置故障分析 |
| CommunicationFailure.md | 通信故障分析 |
| UpgradeFailure.md | 软件升级故障分析 |

---

# 10. Recommended Reading Order

建议按软件架构自下而上学习：

```text
Firmware Failure

↓

Driver Failure

↓

SDK Failure

↓

Configuration Failure

↓

Calibration Failure

↓

Communication Failure

↓

Upgrade Failure
```

理解底层控制后，再学习上层软件模块，有助于快速建立完整的软件系统知识体系。

---

# 11. Engineering Recommendations

建议：

- 软件故障分析应优先确认 Firmware Version、Driver Version、SDK Version 是否匹配。
- 升级软件前，应备份 Calibration 数据及 Configuration 文件。
- 软件升级完成后，应执行完整功能验证。
- 对于无法确认的软件异常，应结合 Workflow、System Log、DecisionTree 进行分析。
- 若软件排查无异常，应进一步参考 **HardwareFailure** 模块确认是否存在硬件故障。

---

# 12. Learning Path

推荐学习路径：

```text
README

↓

Firmware Failure

↓

Driver Failure

↓

SDK Failure

↓

Configuration Failure

↓

Calibration Failure

↓

Communication Failure

↓

Upgrade Failure

↓

DecisionTree

↓

Workflow

↓

Field Troubleshooting
```

---

# 13. Cross References

本模块建议结合以下内容共同学习：

- **HardwareFailure/**：区分软件故障与硬件故障。
- **06_Workflow/**：理解故障发生阶段。
- **05_Calibration/**：理解校准流程及异常处理。
- **09_DecisionTree/**：掌握标准诊断流程。
- **10_FAQ/**：快速定位常见软件问题。

---

# 14. Summary

Software Failure 模块建立了 Detector 软件系统的完整故障知识体系，覆盖 Firmware、Driver、SDK、Calibration、Configuration、Communication 及 Upgrade 等核心软件模块。通过统一的软件故障分类、诊断流程及文档结构，可帮助工程师快速区分软件与硬件问题，提高现场故障定位效率，并为 Workflow、DecisionTree 及 Service 提供标准化的软件故障分析依据。