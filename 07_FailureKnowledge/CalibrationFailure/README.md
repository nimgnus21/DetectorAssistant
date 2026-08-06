# CalibrationFailure

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
- CalibrationDataFailure.md
- ../SoftwareFailure/README.md
- ../ImageFailure/OffsetArtifact.md
- ../ImageFailure/GainArtifact.md
- ../ImageFailure/BadPixelArtifact.md
- ../../05_Calibration/README.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Calibration Failure 模块用于描述数字平板探测器（Flat Panel Detector，FPD）校准过程中可能出现的各种故障，包括校准失败、校准结果异常、校准数据损坏及校准后图像异常等问题。

Calibration 是保证 Detector 图像质量的核心流程，任何校准异常均可能导致图像均匀性下降、噪声增加、坏点补偿失效及图像伪影等问题。

本模块建立标准化的 Calibration Failure 分类、故障分析及诊断方法，为研发、生产测试及现场维修提供统一参考。

---

# 2. Scope

适用于：

- Factory Calibration
- Installation Calibration
- Maintenance Calibration
- Periodic Calibration
- Engineering Debug
- Technical Support
- Field Service

包括：

- Offset Calibration
- Gain Calibration
- Bad Pixel Calibration
- Calibration Data Management

---

# 3. Calibration Failure Architecture

```text
Calibration Failure

├── Offset Calibration Failure
├── Gain Calibration Failure
├── Bad Pixel Calibration Failure
└── Calibration Data Failure
```

各子模块职责如下：

| Module | Description |
|----------|-------------|
| OffsetCalibrationFailure | Offset 校准异常分析 |
| GainCalibrationFailure | Gain 校准异常分析 |
| BadPixelCalibrationFailure | 坏点校准异常分析 |
| CalibrationDataFailure | 校准文件、参数及数据异常 |

---

# 4. Calibration Workflow

标准 Calibration 流程如下：

```text
Preparation

↓

Detector Initialization

↓

Offset Calibration

↓

Gain Calibration

↓

Bad Pixel Calibration

↓

Calibration Verification

↓

Save Calibration Data

↓

Image Validation
```

任一阶段异常均属于 Calibration Failure。

---

# 5. Common Failure Symptoms

典型表现包括：

- Calibration Failed
- Calibration Timeout
- Calibration Interrupted
- Calibration Result Invalid
- Calibration Data Missing
- Calibration Data Corrupted
- Offset Not Updated
- Gain Not Updated
- Bad Pixel Compensation Failed
- Image Quality Worse After Calibration

---

# 6. Failure Classification

## 6.1 Process Failure

校准流程未完成。

例如：

- Timeout
- Communication Failure
- Detector Offline

---

## 6.2 Algorithm Failure

校准算法计算失败。

例如：

- Offset Calculation Error
- Gain Calculation Error
- Bad Pixel Detection Error

---

## 6.3 Data Failure

校准数据异常。

例如：

- File Missing
- CRC Error
- Wrong Version
- Parameter Mismatch

---

## 6.4 Hardware Related Failure

硬件导致校准失败。

例如：

- ADC Failure
- Photodiode Failure
- TFT Failure
- Readout ASIC Failure

---

## 6.5 Environment Related Failure

环境导致校准异常。

例如：

- Temperature Drift
- Unstable Power
- EMI
- X-ray Instability

---

# 7. Relationship with Image Failure

Calibration Failure 可直接导致：

| Image Failure | Related Calibration |
|---------------|---------------------|
| Offset Artifact | Offset Calibration |
| Gain Artifact | Gain Calibration |
| Uniformity Failure | Gain Calibration |
| Bad Pixel Artifact | Bad Pixel Calibration |
| Noise Artifact | Offset / Gain Calibration |
| Ghost Artifact | Offset Calibration |

---

# 8. Relationship with Hardware Failure

可能涉及：

- ADC
- TFT
- Photodiode
- Readout ASIC
- FPGA
- Main Board
- Power Module

硬件异常通常表现为：

- Calibration 无法完成
- Calibration 结果异常
- Calibration 重复失败

---

# 9. Relationship with Software Failure

主要涉及：

- Firmware Failure
- Configuration Failure
- Driver Failure
- SDK Failure
- Communication Failure

软件异常通常表现为：

- Calibration 无法启动
- Calibration 参数错误
- Calibration 文件无法保存
- Calibration 数据无法加载

---

# 10. Standard Diagnostic Workflow

```text
Calibration Failure

↓

Calibration Started？

↓

NO

↓

Software

↓

YES

↓

Calibration Completed？

↓

NO

↓

Communication

↓

YES

↓

Calibration Saved？

↓

NO

↓

Storage

↓

YES

↓

Image Verified？

↓

NO

↓

Hardware

↓

YES

↓

Calibration Passed
```

---

# 11. Troubleshooting Principles

推荐按照以下顺序排查：

1. 检查 Detector 是否正常连接。
2. 检查当前 Calibration Workflow 是否完整执行。
3. 检查 Calibration Log。
4. 检查 Calibration Data 是否正确保存。
5. 验证 Offset、Gain、Bad Pixel 校准结果。
6. 检查 Hardware Module 是否正常。
7. 使用 DecisionTree 完成 Root Cause Analysis。

---

# 12. Related Documents

## OffsetCalibrationFailure

分析 Offset 校准失败。

---

## GainCalibrationFailure

分析 Gain 校准失败。

---

## BadPixelCalibrationFailure

分析坏点校准失败。

---

## CalibrationDataFailure

分析校准文件及数据异常。

---

## DecisionTree

Calibration Failure 是故障诊断的重要入口之一。

---

# 13. Knowledge Graph

```text
Calibration Failure

├── Offset Calibration
├── Gain Calibration
├── Bad Pixel Calibration
└── Calibration Data

↓

Calibration Workflow

↓

Image Verification

↓

Hardware Analysis

↓

Software Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 14. Summary

Calibration Failure 是 Flat Panel Detector 图像质量异常的重要来源，涵盖 Offset、Gain、Bad Pixel 校准及 Calibration Data 管理等多个环节。通过标准化的 Workflow、Log 分析、数据验证及硬件检查，可快速定位校准失败原因，并结合 Image Failure、Hardware Failure、Software Failure 及 DecisionTree 建立完整的校准故障分析体系。