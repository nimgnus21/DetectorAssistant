# CalibrationDataFailure

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
- OffsetCalibrationFailure.md
- GainCalibrationFailure.md
- BadPixelCalibrationFailure.md
- ../SoftwareFailure/ConfigurationFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../HardwareFailure/MemoryFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../../05_Calibration/
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

CalibrationDataFailure 描述数字平板探测器（Flat Panel Detector，FPD）在 Calibration Data（校准数据）管理过程中发生的各种异常，包括 Calibration File 丢失、Calibration Table 损坏、参数不匹配、版本冲突及数据加载失败等问题。

Calibration Data 是 Detector 正常工作的核心配置数据，负责保存 Offset、Gain、Bad Pixel 等校准结果。若 Calibration Data 出现异常，即使 Calibration 已正确完成，也可能导致图像质量异常。

本文件回答的问题：

> **为什么 Calibration 已完成，但 Detector 图像仍异常？为什么升级或更换主板后 Calibration 失效？**

---

# 2. Scope

适用于：

- Factory Calibration
- Detector Repair
- Firmware Upgrade
- Main Board Replacement
- Detector Initialization
- Technical Support
- Field Service

适用于：

- Calibration File
- Calibration Table
- Calibration Database
- Calibration Backup
- Calibration Restore

---

# 3. What is Calibration Data Failure

Calibration Data Failure 指：

**Calibration 数据在生成、存储、加载、校验、恢复或版本管理过程中发生异常，导致 Detector 无法正确使用校准参数。**

主要表现：

- Calibration File Missing
- Calibration File Corrupted
- Calibration Load Failed
- Calibration Version Mismatch
- Calibration CRC Error
- Calibration Lost After Upgrade
- Calibration Lost After Board Replacement

---

# 4. Failure Classification

```text
Calibration Data Failure

├── Data Missing
├── Data Corruption
├── Data Load Failure
├── Data Save Failure
├── Version Mismatch
├── CRC Verification Failure
├── Backup Failure
└── Restore Failure
```

---

# 5. Typical Symptoms

## 5.1 Calibration File Missing

特点：

- Calibration 无法加载
- 系统恢复默认参数

可能原因：

- File Deleted
- Storage Failure
- Incorrect Installation

---

## 5.2 Calibration Data Corruption

特点：

- Calibration 文件存在
- 无法正常使用

可能原因：

- Flash Memory Error
- Unexpected Power Loss
- File Corruption

---

## 5.3 Calibration Load Failure

特点：

- 启动时提示 Calibration Load Failed
- Image Quality 异常

可能原因：

- File Format Error
- Firmware Incompatible
- Configuration Error

---

## 5.4 Calibration Save Failure

特点：

- Calibration 完成
- 数据未写入存储介质

可能原因：

- Storage Full
- Flash Failure
- Write Permission Error

---

## 5.5 Version Mismatch

特点：

- Firmware 更新后 Calibration 无效

可能原因：

- Calibration Format Changed
- Firmware Version Incompatible

---

## 5.6 CRC Verification Failure

特点：

- Calibration 校验失败
- 文件被判定无效

可能原因：

- Data Corruption
- Incomplete Transmission

---

## 5.7 Backup Failure

特点：

- Calibration 无法备份
- 无恢复数据

可能原因：

- Storage Failure
- Backup Process Interrupted

---

## 5.8 Restore Failure

特点：

- Calibration 恢复失败
- Detector 使用默认参数

可能原因：

- Backup File Invalid
- Restore Process Failure

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| File Missing | Storage Error |
| File Corrupted | Flash Failure |
| Load Failure | Firmware Compatibility |
| Save Failure | Write Failure |
| Version Mismatch | Firmware Upgrade |
| CRC Error | Data Corruption |
| Restore Failure | Backup Invalid |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Flash Memory | Calibration File Lost |
| Main Board | Storage Failure |
| FPGA | Parameter Loading Failure |
| DDR Memory | Temporary Data Error |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Calibration Load Failure |
| Configuration | Parameter Mismatch |
| Driver | File Access Failure |
| SDK | Calibration Import Failure |

---

# 9. Relationship with Calibration

Calibration Data Failure 可影响：

- Offset Calibration
- Gain Calibration
- Bad Pixel Calibration

即使 Calibration 流程执行成功，只要 Calibration Data 无法正确保存或加载，最终图像仍可能异常。

---

# 10. Diagnostic Workflow

```text
Calibration Data Failure

↓

Calibration File Exists？

↓

NO

↓

Storage

↓

YES

↓

CRC Correct？

↓

NO

↓

Data Corruption

↓

YES

↓

Version Match？

↓

NO

↓

Firmware Compatibility

↓

YES

↓

Load Successful？

↓

NO

↓

Configuration

↓

YES

↓

Image Normal？

↓

NO

↓

Calibration Verification

↓

Calibration Data Normal
```

---

# 11. Detection Methods

## File Integrity Verification

检查：

- File Size
- File Format
- File Timestamp
- File Permission

---

## CRC Verification

验证：

- CRC
- Checksum
- Integrity

---

## Version Verification

检查：

- Firmware Version
- Calibration Version
- Configuration Version

---

## Backup Verification

确认：

- Backup File Exists
- Backup Complete
- Restore Available

---

## Log Analysis

检查：

- Calibration Log
- Storage Log
- Firmware Log
- Error Code

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Calibration Lost After Upgrade | Version Mismatch |
| Calibration Missing After Board Replacement | Storage Initialization |
| Calibration File Corrupted | Flash Failure |
| CRC Verification Failed | Data Corruption |
| Cannot Restore Calibration | Backup Invalid |
| Image Abnormal After Successful Calibration | Calibration Data Load Failure |

---

# 13. Engineering Recommendations

建议：

- Firmware 升级前备份全部 Calibration Data。
- 更换 Main Board 后恢复 Calibration Data 或重新执行完整 Calibration。
- 定期验证 Calibration 文件完整性。
- 建立 Calibration Data 版本管理机制。
- 发现 CRC 错误时禁止继续使用当前 Calibration 数据。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## OffsetCalibrationFailure

Offset Table 管理异常。

---

## GainCalibrationFailure

Gain Table 管理异常。

---

## BadPixelCalibrationFailure

Bad Pixel Map 管理异常。

---

## MemoryFailure

Calibration Data 存储异常的重要来源。

---

## DecisionTree

Calibration Data Failure 是 Calibration 故障分析的重要节点。

---

# 15. Knowledge Graph

```text
Calibration Data Failure

├── File Missing
├── Data Corruption
├── Load Failure
├── Save Failure
├── Version Mismatch
├── CRC Failure
├── Backup Failure
└── Restore Failure

↓

Calibration Data Management

↓

Storage Verification

↓

Hardware Analysis

├── Flash
├── Main Board
├── FPGA
└── Memory

↓

Software Analysis

├── Firmware
├── Configuration
├── Driver
└── SDK

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Calibration Data Failure 是 Flat Panel Detector 校准管理过程中重要的系统性故障，主要涉及 Calibration 数据的生成、存储、加载、校验、备份及恢复等环节。其根因通常包括 Flash Memory 故障、Main Board 存储异常、Firmware 版本不兼容、Configuration 错误及数据损坏等。通过文件完整性检查、CRC 校验、版本验证、备份恢复测试及日志分析，可快速定位 Calibration Data 异常，并结合 Hardware Failure、Software Failure 与 DecisionTree 建立完整的校准数据故障分析体系。