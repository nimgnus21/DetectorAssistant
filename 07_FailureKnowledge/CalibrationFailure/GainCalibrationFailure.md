# GainCalibrationFailure

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
- BadPixelCalibrationFailure.md
- CalibrationDataFailure.md
- ../ImageFailure/GainArtifact.md
- ../ImageFailure/UniformityFailure.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../HardwareFailure/ScintillatorFailure.md
- ../HardwareFailure/ADCFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/GainCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Gain Calibration Failure 描述数字平板探测器（Flat Panel Detector，FPD）在 Gain Calibration（增益校准）过程中发生的各种异常，包括 Gain 数据计算失败、Gain Table 生成失败、Gain 校准结果异常以及校准后图像质量下降等问题。

Gain Calibration 的目标是消除 Detector 各 Pixel 对相同 X-ray 剂量响应不一致的问题，使整幅图像具有一致的亮度和灰度响应。

本文件回答的问题：

> **为什么 Gain Calibration 会失败？为什么完成 Gain Calibration 后图像仍然存在亮暗不均？**

---

# 2. Scope

适用于：

- Factory Calibration
- Acceptance Test
- Preventive Maintenance
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Gain Calibration
- Flat Field Calibration
- Gain Table Generation
- Gain Verification

---

# 3. What is Gain Calibration Failure

Gain Calibration Failure 指：

**Detector 无法正确计算、保存、加载或应用 Gain 数据，导致 Pixel 响应补偿失败。**

主要表现：

- Gain Calibration Failed
- Gain Table Invalid
- Uniformity Poor
- Brightness Difference
- Gain Drift
- Calibration Passed but Uniformity Failed

---

# 4. Failure Classification

```text
Gain Calibration Failure

├── Calibration Start Failure
├── Flat Field Acquisition Failure
├── Gain Calculation Failure
├── Gain Table Save Failure
├── Gain Table Load Failure
├── Gain Drift
└── Gain Verification Failure
```

---

# 5. Typical Symptoms

## 5.1 Calibration Cannot Start

特点：

- 无法启动 Gain Calibration
- 软件提示 Calibration Failed

可能原因：

- Detector Offline
- Configuration Error
- Firmware Failure

---

## 5.2 Flat Field Acquisition Failure

特点：

- Flat Field Image 无法采集
- Calibration 中断

可能原因：

- X-ray Generator Failure
- Exposure Failure
- Communication Failure

---

## 5.3 Gain Calculation Failure

特点：

- 无法生成 Gain Table
- 软件提示 Calculation Error

可能原因：

- Invalid Flat Field Image
- Firmware Algorithm Error

---

## 5.4 Gain Table Save Failure

特点：

- Gain Calibration 完成
- Gain 数据未保存

可能原因：

- Flash Failure
- Storage Error

---

## 5.5 Gain Table Load Failure

特点：

- 系统无法加载 Gain 数据
- 使用默认参数运行

可能原因：

- File Missing
- CRC Error
- Version Mismatch

---

## 5.6 Gain Drift

特点：

- Gain 随时间变化
- 图像亮度逐渐变化

可能原因：

- Temperature Drift
- Analog Circuit Drift
- Detector Aging

---

## 5.7 Gain Verification Failure

特点：

- Calibration 成功
- Flat Field 仍然不均匀

可能原因：

- Photodiode Response Difference
- Scintillator Non-uniformity
- ADC Gain Difference

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Calibration Cannot Start | Firmware / Configuration |
| Flat Field Acquisition Failure | Exposure / Communication |
| Gain Calculation Failure | Firmware Algorithm |
| Save Failure | Storage Failure |
| Load Failure | Calibration File |
| Gain Drift | Temperature / Aging |
| Verification Failure | Hardware Difference |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Photodiode | Sensitivity Difference |
| Scintillator | Light Output Difference |
| ADC | Gain Difference |
| Readout ASIC | Channel Gain Difference |
| FPGA | Gain Processing Failure |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Gain Calculation Failure |
| Configuration | Wrong Calibration Parameters |
| Driver | Calibration Communication Failure |
| SDK | Gain Table Loading Failure |

---

# 9. Relationship with Image Failure

Gain Calibration Failure 可能导致：

- Gain Artifact
- Uniformity Failure
- Brightness Difference
- Stripe Artifact
- Local Bright/Dark Region

---

# 10. Diagnostic Workflow

```text
Gain Calibration Failed

↓

Calibration Started？

↓

NO

↓

Firmware / Configuration

↓

YES

↓

Flat Field Acquired？

↓

NO

↓

Exposure / Communication

↓

YES

↓

Gain Calculated？

↓

NO

↓

Firmware

↓

YES

↓

Gain Saved？

↓

NO

↓

Storage

↓

YES

↓

Uniformity Passed？

↓

NO

↓

Photodiode / Scintillator / ADC

↓

Calibration Passed
```

---

# 11. Detection Methods

## Flat Field Verification

检查：

- Flat Field 是否均匀
- 曝光是否稳定
- 灰度是否正常

---

## Gain Table Verification

检查：

- Gain Table 是否生成
- 文件是否完整
- CRC 是否正确

---

## Uniformity Test

采集 Uniform Image：

分析：

- Mean Gray Value
- Standard Deviation
- Uniformity

---

## Temperature Stability Test

比较：

- 冷启动
- 热稳定

观察 Gain 是否漂移。

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
| Gain Calibration Timeout | Communication Failure |
| Gain Table Missing | Storage Failure |
| Uniformity Failed After Calibration | Photodiode Difference |
| Bright Corner | Scintillator Difference |
| Gain Changes After Warm-up | Temperature Drift |
| Calibration Passed but Image Uneven | Hardware Difference |

---

# 13. Engineering Recommendations

建议：

- 使用稳定的 X-ray 输出完成 Gain Calibration。
- 确保 Flat Field 图像无遮挡、曝光均匀。
- 校准完成后立即执行 Uniformity Test。
- 检查 Gain Table 是否成功保存及加载。
- 若重复校准无改善，应检查 Photodiode、Scintillator、ADC 及 Firmware。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## GainCalibration

说明 Gain Calibration 标准流程。

---

## GainArtifact

说明 Gain Calibration 异常导致的图像表现。

---

## UniformityFailure

分析 Gain Calibration 对均匀性的影响。

---

## PhotodiodeFailure

分析 Pixel 响应差异。

---

## DecisionTree

Gain Calibration Failure 是 Gain 异常诊断的重要入口。

---

# 15. Knowledge Graph

```text
Gain Calibration Failure

├── Start Failure
├── Flat Field Acquisition Failure
├── Gain Calculation Failure
├── Save Failure
├── Load Failure
├── Gain Drift
└── Verification Failure

↓

Gain Calibration Workflow

↓

Uniformity Verification

↓

Hardware Analysis

├── Photodiode
├── Scintillator
├── ADC
├── ASIC
└── FPGA

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Gain Calibration Failure 是 Flat Panel Detector 增益校准过程中最重要的故障类型之一，涉及 Flat Field 图像采集、Gain 计算、Gain Table 管理及校准结果验证等多个环节。其根因通常包括曝光异常、Photodiode 响应差异、Scintillator 光输出不均、ADC 增益偏差、Firmware 算法异常及存储故障。通过 Flat Field 验证、Gain Table 检查、Uniformity 测试及日志分析，可快速定位 Gain 校准异常，并结合 Image Failure、Hardware Failure 与 DecisionTree 建立完整的 Gain 故障分析体系。