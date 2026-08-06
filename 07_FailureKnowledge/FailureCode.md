# FailureCode

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
- FailureClassification.md
- FailureAnalysisMethod.md
- ../06_Workflow/
- ../09_DecisionTree/
- ../08_Service/

---

# 1. Purpose

Failure Code 定义数字平板探测器（Flat Panel Detector，FPD）的统一故障代码规范。

统一的 Failure Code 用于标识 Detector 在运行过程中产生的异常事件，便于软件记录、日志分析、远程诊断、售后支持及故障统计分析。

本文件回答的问题是：

> **如何唯一标识一个故障？**

---

# 2. Scope

适用于：

- Detector Firmware
- SDK
- Host Software
- Factory Test
- Engineering Debug
- Service Tool
- Technical Support

适用于所有 Detector Runtime Error、Warning 及 Diagnostic Information。

---

# 3. Design Principles

Failure Code 应遵循以下原则：

- 唯一性（Unique）
- 可扩展性（Scalable）
- 可读性（Readable）
- 可追溯性（Traceable）
- 与模块对应（Module-Oriented）

一个 Failure Code 仅对应一种故障类型。

---

# 4. Failure Code Structure

推荐编码格式：

```text
FC-XX-XXXX
```

例如：

```text
FC-HW-0001
FC-CA-0105
FC-CM-0203
```

其中：

| 字段 | 说明 |
|------|------|
| FC | Failure Code |
| XX | 模块分类 |
| XXXX | 顺序编号 |

---

# 5. Module Code Definition

| Module | Code |
|---------|------|
| Hardware | HW |
| Software | SW |
| Calibration | CA |
| Communication | CM |
| Image | IM |
| Power | PW |
| Environment | EN |
| System | SY |

例如：

```text
FC-HW-0001
```

表示：

Hardware Failure No.0001

---

# 6. Hardware Failure Code

示例：

| Failure Code | Description |
|---------------|-------------|
| FC-HW-0001 | Scintillator Failure |
| FC-HW-0002 | Photodiode Failure |
| FC-HW-0003 | TFT Failure |
| FC-HW-0004 | Gate Driver Failure |
| FC-HW-0005 | Readout ASIC Failure |
| FC-HW-0006 | FPGA Failure |
| FC-HW-0007 | Main Board Failure |
| FC-HW-0008 | Memory Failure |

---

# 7. Software Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-SW-0001 | Firmware Startup Failure |
| FC-SW-0002 | Firmware Upgrade Failure |
| FC-SW-0003 | Configuration Error |
| FC-SW-0004 | SDK Initialization Failure |
| FC-SW-0005 | Driver Error |

---

# 8. Calibration Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-CA-0001 | Offset Calibration Failed |
| FC-CA-0002 | Gain Calibration Failed |
| FC-CA-0003 | Defect Calibration Failed |
| FC-CA-0004 | Template Version Mismatch |
| FC-CA-0005 | Calibration Data Missing |

---

# 9. Communication Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-CM-0001 | Ethernet Connection Failed |
| FC-CM-0002 | Wi-Fi Connection Failed |
| FC-CM-0003 | Host Connection Timeout |
| FC-CM-0004 | Image Transmission Failed |
| FC-CM-0005 | Communication Interrupted |

---

# 10. Image Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-IM-0001 | Line Artifact |
| FC-IM-0002 | Dead Pixel |
| FC-IM-0003 | Bright Pixel |
| FC-IM-0004 | Noise |
| FC-IM-0005 | Ghost |
| FC-IM-0006 | Image Lag |
| FC-IM-0007 | Uniformity Failure |
| FC-IM-0008 | Image Distortion |

---

# 11. Power Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-PW-0001 | Battery Failure |
| FC-PW-0002 | External Power Failure |
| FC-PW-0003 | Voltage Abnormal |
| FC-PW-0004 | Over Current |
| FC-PW-0005 | Power Management Failure |

---

# 12. Environment Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-EN-0001 | High Temperature |
| FC-EN-0002 | Low Temperature |
| FC-EN-0003 | High Humidity |
| FC-EN-0004 | Condensation |
| FC-EN-0005 | Electromagnetic Interference |

---

# 13. System Failure Code

| Failure Code | Description |
|---------------|-------------|
| FC-SY-0001 | Startup Failure |
| FC-SY-0002 | Initialization Failure |
| FC-SY-0003 | Workflow Interrupted |
| FC-SY-0004 | Resource Conflict |
| FC-SY-0005 | System Synchronization Failure |

---

# 14. Failure Severity

建议结合故障等级使用。

| Severity | Description | Action |
|-----------|-------------|--------|
| INFO | 提示信息 | 无需处理 |
| WARNING | 一般异常 | 建议检查 |
| ERROR | 功能异常 | 需要处理 |
| CRITICAL | 严重故障 | 停止使用 |

例如：

```text
FC-HW-0005

Severity

CRITICAL
```

---

# 15. Failure Code Lifecycle

```text
Failure Occurred

↓

Generate Failure Code

↓

Write Log

↓

Display Error

↓

Diagnostic Analysis

↓

Decision Tree

↓

Service

↓

Resolved

↓

Close Failure Record
```

---

# 16. Logging Requirements

建议每条 Failure Code 至少记录以下信息：

| Item | Description |
|------|-------------|
| Failure Code | 故障代码 |
| Severity | 故障等级 |
| Timestamp | 时间 |
| Detector SN | 序列号 |
| Firmware Version | 固件版本 |
| Workflow Stage | 所属 Workflow |
| Module | 所属模块 |
| Description | 故障描述 |

---

# 17. Relationship with Other Modules

## Failure Classification

定义故障属于哪一类别。

---

## Failure Analysis Method

定义如何分析该故障。

---

## Workflow

提供故障发生阶段。

---

## DecisionTree

根据 Failure Code 自动进入对应诊断路径。

---

## Service

根据 Failure Code 制定维修方案。

---

# 18. Engineering Notes

工程建议：

- Failure Code 一旦发布，不应重复使用。
- 保持向后兼容，避免修改已有编码。
- 新增故障应按模块顺序扩展编号。
- 日志、SDK 和 UI 应使用统一的 Failure Code。
- 同一故障在不同软件层应保持一致的编码。

---

# 19. Knowledge Graph

```text
Failure

↓

Failure Classification

↓

Failure Code

↓

Workflow

↓

Failure Analysis

↓

Decision Tree

↓

Service

↓

Resolved
```

---

# 20. Summary

Failure Code 建立了 DetectorAssistant 的统一故障编码体系，通过模块化、唯一化、可扩展的编码规则，实现 Hardware、Software、Calibration、Communication、Image、Power、Environment 和 System 故障的统一标识。该规范为日志记录、远程诊断、DecisionTree 导航及售后服务提供统一的数据基础，是整个故障管理体系的重要组成部分。