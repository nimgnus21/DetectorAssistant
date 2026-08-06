# UniformityFailure

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
- ImageArtifact.md
- OffsetArtifact.md
- GainArtifact.md
- NoiseArtifact.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../HardwareFailure/ScintillatorFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/GainCalibration.md
- ../../05_Calibration/OffsetCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Uniformity Failure 描述数字平板探测器（Flat Panel Detector，FPD）图像均匀性异常（Uniformity Failure）的典型表现、形成机理、故障来源、检测方法及根因分析。

均匀性（Uniformity）是评价探测器图像质量的重要指标。在理想情况下，Detector 对均匀 X-ray 照射应输出灰度一致的图像。若图像出现局部亮暗不一致、渐变、块状阴影或条带，则说明图像均匀性发生异常。

本文件回答的问题：

> **为什么均匀曝光下图像仍然不均匀？如何快速定位均匀性异常的根因？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Offset Uniformity
- Gain Uniformity
- Flat Field Test
- Uniform Exposure Test
- Clinical Image Verification

---

# 3. What is Uniformity Failure

Uniformity Failure 指：

**在均匀曝光条件下，Detector 输出图像出现非真实的灰度差异或亮度分布异常。**

典型特点：

- 明暗不一致
- 局部阴影
- 大面积渐变
- 块状区域
- 条带区域

---

# 4. Classification

```text
Uniformity Failure

├── Global Non-uniformity
├── Local Non-uniformity
├── Gradient Artifact
├── Block Artifact
├── Stripe Uniformity Failure
├── Corner Brightness Difference
└── Regional Brightness Difference
```

---

# 5. Image Characteristics

## 5.1 Global Non-uniformity

特点：

- 整幅图像灰度分布不一致
- 左右或上下亮度不同

可能原因：

- Gain Calibration Failure
- X-ray Beam Non-uniformity
- Scintillator Aging

---

## 5.2 Local Non-uniformity

特点：

- 局部区域偏亮或偏暗
- 固定位置

可能原因：

- Photodiode Failure
- Scintillator Damage
- Local Gain Error

---

## 5.3 Gradient Artifact

特点：

- 灰度逐渐变化
- 无明显边界

可能原因：

- Offset Drift
- Temperature Drift
- Power Drift

---

## 5.4 Block Artifact

特点：

- 方块状区域
- 边界清晰

可能原因：

- Readout ASIC
- FPGA Data Block Error
- Gain Table Corruption

---

## 5.5 Stripe Uniformity Failure

特点：

- 宽条带亮暗变化

可能原因：

- Gain Calibration Error
- ADC Channel Offset
- Power Ripple

---

## 5.6 Corner Brightness Difference

特点：

- 四角亮度明显不同

可能原因：

- Scintillator Thickness Difference
- X-ray Irradiation Difference
- Mechanical Assembly Error

---

# 6. Typical Root Causes

| Uniformity Failure | Possible Root Cause |
|--------------------|---------------------|
| Overall Brightness Difference | Gain Calibration |
| Local Dark Area | Photodiode Failure |
| Local Bright Area | Gain Table Error |
| Block Difference | FPGA / ASIC |
| Gradient | Offset Drift |
| Stripe | ADC / Gain |
| Corner Difference | Scintillator |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Scintillator | Brightness Difference |
| Photodiode | Local Non-uniformity |
| Readout ASIC | Block Artifact |
| ADC | Stripe Artifact |
| FPGA | Regional Difference |
| Power Module | Gradient |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Calibration | Uniformity Failure |
| Configuration | Brightness Difference |
| Firmware | Wrong Correction |
| SDK | Incorrect Calibration Loading |

---

# 9. Relationship with Calibration

Uniformity Failure 与 Calibration 关系最为密切。

主要关联：

- Offset Calibration
- Gain Calibration
- Bad Pixel Calibration

任何校准异常均可能导致均匀性下降。

---

# 10. Diagnostic Workflow

```text
Uniform Image

↓

Brightness Uniform？

↓

NO

↓

Global？

↓

YES

↓

Gain Calibration

↓

NO

↓

Local？

↓

YES

↓

Photodiode

↓

Block？

↓

ASIC / FPGA

↓

Gradient？

↓

Offset / Temperature

↓

Stripe？

↓

ADC / Gain

↓

Corner Difference？

↓

Scintillator
```

---

# 11. Detection Methods

## Flat Field Test

采集：

- Uniform Exposure Image

观察：

- 灰度一致性
- 区域亮度变化

---

## Uniformity Measurement

测量：

- Mean Gray Value
- Standard Deviation
- Uniformity Percentage

---

## Calibration Verification

重新执行：

- Offset Calibration
- Gain Calibration

验证异常是否改善。

---

## Temperature Verification

检查：

- Detector Temperature
- Warm-up Time

确认是否存在温漂。

---

## Hardware Inspection

检查：

- Scintillator
- Photodiode
- ASIC
- ADC
- Power Module

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Whole Image Uneven | Gain Calibration Failure |
| Local Dark Region | Photodiode Failure |
| Local Bright Region | Gain Table Error |
| Stripe Uniformity | ADC Offset |
| Corner Dark | Scintillator Aging |
| Gradient Image | Offset Drift |

---

# 13. Engineering Recommendations

建议：

- 首先使用标准 Flat Field 图像进行分析。
- 优先重新执行 Offset 与 Gain Calibration。
- 确认异常是否固定位置。
- 排除 X-ray Source 不均匀照射影响。
- 若重新校准无改善，再检查 Photodiode、Scintillator、ASIC 及 ADC。
- 使用 DecisionTree 完成最终根因定位。

---

# 14. Relationship with Other Modules

## OffsetArtifact

分析 Offset 引起的均匀性异常。

---

## GainArtifact

分析 Gain 校正导致的均匀性异常。

---

## CalibrationFailure

解释校准失败造成的图像均匀性问题。

---

## PhotodiodeFailure

解释局部灰度异常的硬件原因。

---

## DecisionTree

Uniformity Failure 是图像质量分析的重要入口之一。

---

# 15. Knowledge Graph

```text
Uniformity Failure

├── Global Difference
├── Local Difference
├── Gradient
├── Block Artifact
├── Stripe Artifact
└── Corner Difference

↓

Calibration Analysis

↓

Hardware Analysis

├── Photodiode
├── Scintillator
├── ASIC
├── ADC
└── Power

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Uniformity Failure 是 Flat Panel Detector 图像质量评价中的核心异常类型，主要表现为整体或局部亮度不一致、渐变、条带、块状区域及四角亮度差异等。其根因通常涉及 Gain/Offset Calibration、Photodiode、Scintillator、Readout ASIC、ADC、FPGA 及供电系统。通过 Flat Field 测试、校准验证、硬件检查及 DecisionTree 分析，可快速定位均匀性异常来源，为现场维修、生产测试及研发分析提供标准化诊断依据。