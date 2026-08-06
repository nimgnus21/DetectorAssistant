# GainArtifact

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
- UniformityFailure.md
- OffsetArtifact.md
- BadPixelArtifact.md
- ../SoftwareFailure/CalibrationFailure.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../HardwareFailure/ScintillatorFailure.md
- ../HardwareFailure/ADCFailure.md
- ../../05_Calibration/GainCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Gain Artifact 描述数字平板探测器（Flat Panel Detector，FPD）由于 Gain Calibration（增益校正）异常所导致的图像伪影，包括形成机理、图像表现、影响因素、检测方法及根因分析。

Gain Calibration 用于补偿不同 Pixel 对相同 X-ray 剂量响应不一致的问题，使整个 Detector 输出具有一致的灰度响应。

若 Gain 数据错误、Gain Table 损坏或 Gain Calibration 失败，则会导致图像整体或局部亮度不一致，从而产生 Gain Artifact。

本文件回答的问题：

> **为什么均匀曝光下图像仍然出现亮暗不一致？Gain 校正异常会导致哪些图像问题？**

---

# 2. Scope

适用于：

- Gain Calibration
- Flat Field Test
- Uniform Exposure Test
- Factory Test
- Engineering Debug
- Technical Support
- Field Service

---

# 3. What is Gain Artifact

Gain Artifact 指：

**由于 Gain Calibration 数据异常或 Gain Correction 失败，使不同 Pixel 对相同 X-ray 输入产生不同灰度输出，从而导致图像亮度分布异常。**

主要特点：

- 图像亮度不均匀
- 局部区域偏亮或偏暗
- 条带状亮度变化
- 大面积灰度差异
- 图像重复性较高

---

# 4. Classification

```text
Gain Artifact

├── Global Gain Error
├── Local Gain Error
├── Stripe Gain Artifact
├── Block Gain Artifact
├── Gain Drift
└── Gain Saturation
```

---

# 5. Image Characteristics

## 5.1 Global Gain Error

特点：

- 整体亮度异常
- 图像灰度整体偏高或偏低

可能原因：

- Wrong Gain Table
- Gain Calibration Failure

---

## 5.2 Local Gain Error

特点：

- 局部区域明显偏亮或偏暗
- 固定位置重复出现

可能原因：

- Local Gain Table Error
- Photodiode Sensitivity Difference

---

## 5.3 Stripe Gain Artifact

特点：

- 行或列方向亮暗条纹
- 周期性明显

可能原因：

- ADC Gain Difference
- ASIC Channel Gain Difference

---

## 5.4 Block Gain Artifact

特点：

- 方块状亮度差异
- 边界清晰

可能原因：

- FPGA Data Block Error
- Readout ASIC Gain Error

---

## 5.5 Gain Drift

特点：

- 图像亮度随时间变化
- 热稳定后逐渐恢复

可能原因：

- Temperature Drift
- Analog Circuit Drift

---

## 5.6 Gain Saturation

特点：

- 局部区域亮度达到最大值
- 无法正常补偿

可能原因：

- Gain Overflow
- Firmware Calculation Error

---

# 6. Typical Root Causes

| Artifact | Possible Root Cause |
|----------|---------------------|
| Whole Image Brightness Difference | Gain Calibration Failure |
| Local Bright Area | Gain Table Error |
| Stripe Brightness Difference | ADC Gain Difference |
| Block Difference | ASIC / FPGA |
| Gain Drift | Temperature Drift |
| Saturation | Gain Calculation Error |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Photodiode | Pixel Sensitivity Difference |
| Scintillator | Light Output Difference |
| ADC | Gain Difference |
| Readout ASIC | Channel Gain Difference |
| FPGA | Gain Correction Error |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Calibration | Gain Calibration Failure |
| Firmware | Gain Table Processing Error |
| Configuration | Wrong Gain Parameter |
| SDK | Gain Table Loading Failure |

---

# 9. Relationship with Calibration

Gain Artifact 与 Gain Calibration 直接对应。

标准流程：

```text
Flat Field Image

↓

Calculate Pixel Gain

↓

Generate Gain Table

↓

Gain Correction

↓

Corrected Image
```

任何环节异常均可能导致 Gain Artifact。

---

# 10. Diagnostic Workflow

```text
Uniform Exposure

↓

Brightness Uniform？

↓

NO

↓

Whole Image？

↓

YES

↓

Gain Calibration

↓

NO

↓

Local Area？

↓

YES

↓

Photodiode

↓

Stripe？

↓

ADC / ASIC

↓

Block？

↓

FPGA

↓

Temperature Related？

↓

Gain Drift
```

---

# 11. Detection Methods

## Flat Field Test

采集：

- Uniform Exposure Image

观察：

- Brightness Uniformity
- Gray Distribution

---

## Gain Calibration

重新执行：

- Gain Calibration

确认异常是否消失。

---

## Histogram Analysis

分析：

- Mean Gray Value
- Gray Distribution
- Uniformity

---

## Temperature Stability Test

观察：

- 冷启动
- 热稳定

比较 Gain 是否漂移。

---

## Hardware Inspection

检查：

- Photodiode
- Scintillator
- ADC
- ASIC
- FPGA

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Whole Image Uneven | Gain Calibration Failure |
| Bright Block | FPGA Gain Table Error |
| Stripe Brightness | ADC Gain Difference |
| Corner Brightness Difference | Scintillator Difference |
| Local Bright Area | Photodiode Sensitivity Difference |
| Gain Lost After Upgrade | Gain Table Missing |

---

# 13. Engineering Recommendations

建议：

- 优先使用标准 Flat Field 图像分析 Gain。
- 重新执行 Gain Calibration。
- 确认 Gain Table 是否正确加载。
- 判断异常是否固定位置。
- 检查 Photodiode、Scintillator、ADC、ASIC 是否存在响应差异。
- 使用 DecisionTree 完成最终故障定位。

---

# 14. Relationship with Other Modules

## GainCalibration

Gain Artifact 的直接来源。

---

## UniformityFailure

Gain 异常是均匀性异常最常见原因。

---

## PhotodiodeFailure

解释局部响应差异。

---

## ScintillatorFailure

解释局部光输出差异。

---

## DecisionTree

Gain Artifact 是 Flat Field 图像分析的重要诊断节点。

---

# 15. Knowledge Graph

```text
Gain Artifact

├── Global Gain Error
├── Local Gain Error
├── Stripe Gain Artifact
├── Block Gain Artifact
├── Gain Drift
└── Gain Saturation

↓

Gain Calibration

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

Gain Artifact 是 Flat Panel Detector 图像校正过程中最重要的图像异常之一，主要表现为整体或局部亮度不一致、条带、块状区域及增益漂移等。其根因通常包括 Gain Calibration 失败、Gain Table 错误、Photodiode 响应差异、Scintillator 光输出不均、ADC/Readout ASIC 增益偏差以及 FPGA 校正异常等。通过 Flat Field 测试、Gain Calibration 验证、灰度统计分析及硬件检查，可快速定位 Gain 异常来源，并结合 Calibration、HardwareFailure 及 DecisionTree 建立标准化故障分析流程。