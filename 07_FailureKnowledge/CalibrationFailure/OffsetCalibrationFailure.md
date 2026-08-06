# OffsetCalibrationFailure

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
- GainCalibrationFailure.md
- BadPixelCalibrationFailure.md
- CalibrationDataFailure.md
- ../ImageFailure/OffsetArtifact.md
- ../HardwareFailure/ADCFailure.md
- ../HardwareFailure/PowerFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/OffsetCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Offset Calibration Failure 描述数字平板探测器（Flat Panel Detector，FPD）在 Offset Calibration（零点校准）过程中可能发生的故障，包括校准失败、Offset 数据异常、校准结果异常及其对图像质量的影响。

Offset Calibration 是 Detector 图像校正的第一步，其目的是在无 X-ray 曝光条件下采集 Detector 的 Dark Signal，为后续图像提供统一的灰度基准。

任何 Offset Calibration 异常都可能导致背景灰度异常、图像均匀性下降、Ghost Artifact、Noise Artifact 等问题。

本文件回答的问题：

> **为什么 Offset Calibration 会失败？如何快速定位 Offset 校准异常的根因？**

---

# 2. Scope

适用于：

- Factory Calibration
- Installation Calibration
- Preventive Maintenance
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Offset Calibration
- Dark Image Acquisition
- Offset Table Generation
- Offset Verification

---

# 3. What is Offset Calibration Failure

Offset Calibration Failure 指：

**Detector 无法正确采集、计算、保存或应用 Offset 数据，导致 Offset 校准失败或校准结果异常。**

主要表现：

- Offset Calibration Failed
- Calibration Timeout
- Offset Table Invalid
- Offset Drift
- Offset Not Updated
- Calibration Passed but Image Abnormal

---

# 4. Failure Classification

```text
Offset Calibration Failure

├── Calibration Start Failure
├── Dark Image Acquisition Failure
├── Offset Calculation Failure
├── Offset Data Save Failure
├── Offset Table Load Failure
├── Offset Drift
└── Offset Verification Failure
```

---

# 5. Typical Symptoms

## 5.1 Calibration Cannot Start

特点：

- 无法进入 Offset Calibration
- 软件提示启动失败

可能原因：

- Detector Offline
- Firmware Failure
- Configuration Error

---

## 5.2 Dark Image Acquisition Failure

特点：

- Dark Image 无法采集
- Calibration 中断

可能原因：

- Trigger Failure
- Communication Failure
- Detector Busy

---

## 5.3 Offset Calculation Failure

特点：

- Offset Table 无法生成
- Calculation Error

可能原因：

- Firmware Algorithm Error
- Invalid Raw Data

---

## 5.4 Offset Save Failure

特点：

- Offset Calibration 完成
- 数据无法保存

可能原因：

- Storage Failure
- File Permission Error
- Flash Memory Failure

---

## 5.5 Offset Load Failure

特点：

- Offset Table 无法加载
- 系统使用默认参数

可能原因：

- Calibration File Missing
- Version Mismatch
- CRC Error

---

## 5.6 Offset Drift

特点：

- Offset 随时间变化
- 冷启动与热稳定差异明显

可能原因：

- Temperature Drift
- ADC Offset Drift
- Power Instability

---

## 5.7 Offset Verification Failure

特点：

- 校准完成
- 图像仍存在背景异常

可能原因：

- Offset Table Invalid
- Hardware Failure
- Calibration Executed Under Incorrect Conditions

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Calibration Cannot Start | Firmware / Configuration |
| Acquisition Failure | Communication / Trigger |
| Calculation Failure | Firmware Algorithm |
| Save Failure | Storage Device |
| Load Failure | Calibration File |
| Offset Drift | Temperature / ADC |
| Verification Failure | Hardware Failure |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| ADC | Offset Drift |
| Readout ASIC | Channel Offset |
| FPGA | Offset Processing Failure |
| Power Module | Background Drift |
| Main Board | Data Storage Failure |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Offset Calculation Error |
| Configuration | Wrong Calibration Parameter |
| Driver | Calibration Communication Failure |
| SDK | Offset Loading Failure |

---

# 9. Relationship with Image Failure

Offset Calibration Failure 可能导致：

- Offset Artifact
- Uniformity Failure
- Noise Artifact
- Ghost Artifact
- Background Gray Shift

---

# 10. Diagnostic Workflow

```text
Offset Calibration Failed

↓

Calibration Started？

↓

NO

↓

Firmware / Configuration

↓

YES

↓

Dark Image Acquired？

↓

NO

↓

Trigger / Communication

↓

YES

↓

Offset Calculated？

↓

NO

↓

Firmware

↓

YES

↓

Offset Saved？

↓

NO

↓

Storage

↓

YES

↓

Image Normal？

↓

NO

↓

ADC / Power / Hardware

↓

Calibration Passed
```

---

# 11. Detection Methods

## Dark Image Verification

检查：

- Dark Image 是否正常采集
- 灰度是否稳定

---

## Offset Table Verification

检查：

- Offset Table 是否生成
- 数据是否完整
- CRC 是否正确

---

## Image Verification

校准完成后采集：

- Dark Image
- Flat Field Image

确认背景是否恢复正常。

---

## Temperature Stability Test

分别在：

- 冷启动
- 热稳定

状态下执行 Offset Calibration，比较 Offset 是否漂移。

---

## Log Analysis

检查：

- Calibration Log
- Firmware Log
- Error Code
- Communication Log

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Offset Calibration Timeout | Communication Failure |
| Offset File Missing | Storage Failure |
| Offset Table Invalid | Data Corruption |
| Background Still Bright | Offset Verification Failure |
| Offset Changes with Temperature | ADC Drift |
| Calibration Successful but Image Abnormal | Hardware Failure |

---

# 13. Engineering Recommendations

建议：

- 确保 Detector 已完成预热并达到稳定工作温度。
- Offset Calibration 应在无 X-ray 曝光环境下执行。
- 校准完成后立即验证 Dark Image。
- 检查 Offset Table 是否正确保存及加载。
- 若重复校准无改善，应重点检查 ADC、Power Module、Readout ASIC 及 Firmware。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## OffsetCalibration

说明 Offset Calibration 的标准流程。

---

## OffsetArtifact

说明 Offset Calibration 异常导致的图像表现。

---

## ADCFailure

分析 ADC Offset 漂移问题。

---

## CalibrationDataFailure

分析 Offset 数据文件异常。

---

## DecisionTree

Offset Calibration Failure 是 Calibration 故障诊断的重要入口。

---

# 15. Knowledge Graph

```text
Offset Calibration Failure

├── Start Failure
├── Acquisition Failure
├── Calculation Failure
├── Save Failure
├── Load Failure
├── Offset Drift
└── Verification Failure

↓

Offset Calibration Workflow

↓

Image Verification

↓

Hardware Analysis

├── ADC
├── ASIC
├── FPGA
├── Power
└── Storage

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Offset Calibration Failure 是 Flat Panel Detector 校准过程中最基础、最关键的故障类型之一，涵盖校准启动、Dark Image 采集、Offset 计算、数据保存、数据加载及结果验证等多个环节。其根因通常涉及 Firmware、ADC、Power Module、Readout ASIC、存储设备及通信系统。通过 Dark Image 验证、Offset Table 检查、温度稳定性测试及日志分析，可快速定位 Offset 校准异常，并结合 Image Failure、Hardware Failure、Calibration Data 与 DecisionTree 建立完整的校准故障分析体系。