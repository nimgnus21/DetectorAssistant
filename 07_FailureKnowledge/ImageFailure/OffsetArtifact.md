# OffsetArtifact

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
- GainArtifact.md
- GhostArtifact.md
- ../SoftwareFailure/CalibrationFailure.md
- ../HardwareFailure/ADCFailure.md
- ../HardwareFailure/PowerFailure.md
- ../../05_Calibration/OffsetCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Offset Artifact 描述数字平板探测器（Flat Panel Detector，FPD）由于 Offset Correction（零点校正）异常所导致的图像伪影，包括形成机理、图像表现、影响因素、检测方法及根因分析。

Offset Calibration 是 Detector 图像处理流程中的第一步，其作用是在无 X-ray 曝光条件下测量每个 Pixel 的 Dark Signal，并将其从后续图像中扣除。

若 Offset 数据异常或补偿失败，将直接影响整个图像的灰度基准，导致背景异常及均匀性下降。

本文件回答的问题：

> **为什么没有曝光时图像仍然存在灰度？为什么背景会出现明暗不一致？**

---

# 2. Scope

适用于：

- Offset Calibration
- Dark Image
- Flat Field Test
- Factory Test
- Engineering Debug
- Technical Support
- Field Service

---

# 3. What is Offset Artifact

Offset Artifact 指：

**由于 Offset 数据错误、Offset Calibration 失败或 Offset Drift 导致图像背景灰度异常的现象。**

主要特点：

- 无曝光时仍存在图像信号
- 背景灰度偏高或偏低
- 图像整体偏亮或偏暗
- 局部区域灰度异常
- 多次曝光后仍持续存在

---

# 4. Classification

```text
Offset Artifact

├── Global Offset Shift
├── Local Offset Error
├── Offset Drift
├── Background Artifact
├── Offset Stripe
└── Offset Saturation
```

---

# 5. Image Characteristics

## 5.1 Global Offset Shift

特点：

- 整幅图像整体变亮或变暗
- 灰度基线整体偏移

可能原因：

- Offset Calibration Failure
- Wrong Offset Table

---

## 5.2 Local Offset Error

特点：

- 局部区域背景异常
- 固定位置重复出现

可能原因：

- Offset Table Corruption
- Readout Channel Offset

---

## 5.3 Offset Drift

特点：

- 随时间缓慢变化
- 开机初期更加明显

可能原因：

- Temperature Drift
- ADC Offset Drift
- Power Drift

---

## 5.4 Background Artifact

特点：

- 背景不干净
- 空曝光仍有纹理

可能原因：

- Dark Current
- Offset Correction Failure

---

## 5.5 Offset Stripe

特点：

- 背景出现规则条纹
- 行或列方向明显

可能原因：

- ADC Offset
- ASIC Channel Offset

---

## 5.6 Offset Saturation

特点：

- 局部背景灰度达到上限
- 图像无法恢复正常

可能原因：

- Offset Overflow
- Firmware Calculation Error

---

# 6. Typical Root Causes

| Artifact | Possible Root Cause |
|----------|---------------------|
| Whole Image Bright | Offset Calibration Failure |
| Whole Image Dark | Wrong Offset Table |
| Background Texture | Dark Current |
| Stripe Background | ADC Offset |
| Gray Drift | Temperature Drift |
| Local Background Difference | ASIC Channel Offset |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| ADC | Offset Shift |
| Readout ASIC | Channel Offset |
| Power Module | Offset Drift |
| Photodiode | Dark Current Increase |
| FPGA | Offset Calculation Error |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Calibration | Offset Failure |
| Firmware | Offset Calculation Error |
| Configuration | Wrong Offset Parameter |
| SDK | Offset Table Loading Failure |

---

# 9. Relationship with Calibration

Offset Artifact 与 Offset Calibration 完全对应。

主要流程：

```text
Dark Image

↓

Calculate Offset

↓

Generate Offset Table

↓

Offset Correction

↓

Corrected Image
```

任一环节异常均可能导致 Offset Artifact。

---

# 10. Diagnostic Workflow

```text
Background Abnormal

↓

Dark Image Test

↓

Background Uniform？

↓

NO

↓

Whole Image？

↓

YES

↓

Offset Calibration

↓

NO

↓

Local Area？

↓

YES

↓

ADC / ASIC

↓

Gray Drift？

↓

Temperature / Power

↓

Firmware Verification
```

---

# 11. Detection Methods

## Dark Image Test

采集：

- Dark Image

观察：

- Background Gray Level
- Fixed Pattern

---

## Offset Calibration

重新执行：

- Offset Calibration

验证异常是否消除。

---

## Temperature Test

观察：

- 冷启动
- 热稳定后

比较 Offset 是否漂移。

---

## Histogram Analysis

分析：

- Mean Gray Value
- Standard Deviation
- Gray Distribution

---

## Hardware Inspection

检查：

- ADC
- ASIC
- Power Module
- FPGA

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Whole Image Bright | Offset Calibration Failure |
| Whole Image Dark | Wrong Offset Data |
| Background Stripe | ADC Offset |
| Background Drift | Temperature Drift |
| Local Background Difference | ASIC Offset |
| Offset Lost After Upgrade | Calibration File Missing |

---

# 13. Engineering Recommendations

建议：

- 优先采集 Dark Image 判断 Offset 是否正常。
- 重新执行 Offset Calibration。
- 比较不同温度下 Offset 稳定性。
- 检查 Offset Table 是否正确加载。
- 若重新校准无改善，应检查 ADC、ASIC、Power 及 Firmware。
- 使用 DecisionTree 完成最终故障定位。

---

# 14. Relationship with Other Modules

## CalibrationFailure

Offset 校准失败是 Offset Artifact 的主要原因。

---

## UniformityFailure

Offset 异常直接影响图像均匀性。

---

## GhostArtifact

Offset 更新异常可能导致残影。

---

## ADCFailure

ADC Offset 是背景异常的重要硬件来源。

---

## DecisionTree

Offset Artifact 是背景异常分析的重要诊断节点。

---

# 15. Knowledge Graph

```text
Offset Artifact

├── Global Offset Shift
├── Local Offset Error
├── Offset Drift
├── Background Artifact
├── Offset Stripe
└── Offset Saturation

↓

Offset Calibration

↓

Hardware Analysis

├── ADC
├── ASIC
├── Power
├── FPGA
└── Photodiode

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Offset Artifact 是 Flat Panel Detector 图像处理中最基础的图像异常之一，主要表现为背景灰度异常、整体亮度偏移、局部背景差异、灰度漂移及背景条纹等。其根因通常包括 Offset Calibration 失败、ADC Offset 漂移、Readout ASIC 通道偏置、Power 稳定性不足及 Firmware 计算错误等。通过 Dark Image 测试、Offset Calibration 验证、温度稳定性测试及硬件检查，可快速完成 Offset 异常定位，并结合 Calibration、HardwareFailure 与 DecisionTree 建立标准化故障分析流程。