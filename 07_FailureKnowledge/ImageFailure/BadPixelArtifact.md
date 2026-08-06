# BadPixelArtifact

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
- GainArtifact.md
- ../HardwareFailure/TFTFailure.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/BadPixelCalibration.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Bad Pixel Artifact 描述数字平板探测器（Flat Panel Detector，FPD）中坏点（Bad Pixel）的类型、形成机理、图像表现、检测方法及根因分析。

Bad Pixel 是 Detector 生命周期中最常见、最稳定的图像缺陷之一。少量坏点通常可以通过 Bad Pixel Calibration 进行补偿，而大量坏点或坏点持续增加，则可能意味着 Detector 硬件开始老化或损坏。

本文件回答的问题：

> **为什么图像会出现亮点、黑点或坏点簇？什么时候需要怀疑硬件故障？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Dead Pixel
- Bright Pixel
- Hot Pixel
- Cold Pixel
- Pixel Cluster
- Bad Pixel Compensation

---

# 3. What is Bad Pixel Artifact

Bad Pixel Artifact 指：

**一个或多个像素不能按照正常方式响应 X-ray 或读出信号，从而形成固定位置的异常像素。**

特点：

- 固定位置
- 每次曝光均出现
- 不随被检物移动
- 长时间保持一致

---

# 4. Classification

```text
Bad Pixel Artifact

├── Dead Pixel
├── Bright Pixel
├── Hot Pixel
├── Cold Pixel
├── Pixel Cluster
├── Defective Line Pixel
└── Progressive Bad Pixel
```

---

# 5. Image Characteristics

## 5.1 Dead Pixel

特点：

- 始终为黑色
- 无灰度变化

可能原因：

- TFT Open
- Photodiode Failure

---

## 5.2 Bright Pixel

特点：

- 始终为白色
- 灰度异常偏高

可能原因：

- Leakage Current
- ADC Saturation

---

## 5.3 Hot Pixel

特点：

- 高曝光时更明显
- 温度升高后增加

可能原因：

- Dark Current Increase
- Sensor Aging

---

## 5.4 Cold Pixel

特点：

- 响应明显偏低
- 曝光不足区域更加明显

可能原因：

- Photodiode Sensitivity Loss

---

## 5.5 Pixel Cluster

特点：

- 多个相邻坏点
- 面积较大

可能原因：

- Local TFT Damage
- Sensor Defect

---

## 5.6 Progressive Bad Pixel

特点：

- 坏点数量逐渐增加
- 老化明显

可能原因：

- Detector Aging
- Radiation Damage

---

# 6. Typical Root Causes

| Artifact | Possible Root Cause |
|----------|---------------------|
| Dead Pixel | TFT Open |
| Bright Pixel | Leakage Current |
| Hot Pixel | Dark Current |
| Cold Pixel | Photodiode Failure |
| Pixel Cluster | Local Hardware Damage |
| Increasing Bad Pixels | Detector Aging |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| TFT | Dead Pixel |
| Photodiode | Bright / Dark Pixel |
| Readout ASIC | Pixel Block Error |
| ADC | Pixel Gray Error |
| Sensor Array | Pixel Cluster |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Bad Pixel Calibration | 补偿失败 |
| Calibration | 坏点数量增加 |
| Firmware | 补偿表加载失败 |
| SDK | 坏点补偿异常 |

---

# 9. Relationship with Calibration

Bad Pixel Calibration 用于：

- 自动识别坏点
- 建立 Bad Pixel Map
- 邻域插值补偿

若 Calibration 失败：

可能出现：

- 坏点重新出现
- 新坏点无法补偿
- 坏点数量异常增加

---

# 10. Diagnostic Workflow

```text
Bad Pixel

↓

Fixed Position？

↓

YES

↓

Single？

↓

YES

↓

TFT / Photodiode

↓

Multiple？

↓

Pixel Cluster

↓

Increasing？

↓

Detector Aging

↓

Calibration Valid？

↓

NO

↓

Bad Pixel Calibration

↓

Hardware Verification
```

---

# 11. Detection Methods

## Dark Image Test

采集暗场图像：

观察：

- Bright Pixel
- Hot Pixel

---

## Flat Field Test

采集均匀曝光图像：

观察：

- Dead Pixel
- Cold Pixel

---

## Bad Pixel Calibration

重新执行：

- Bad Pixel Detection
- Bad Pixel Compensation

---

## Temperature Test

比较：

- 常温
- 高温

观察坏点变化。

---

## Trend Analysis

统计：

- Bad Pixel Count
- Growth Rate

判断是否存在老化趋势。

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Single Black Pixel | TFT Failure |
| Single Bright Pixel | Leakage Current |
| Multiple Bright Pixels | Dark Current Increase |
| Pixel Cluster | Local Sensor Damage |
| Bad Pixel After Upgrade | Calibration Table Lost |
| Increasing Bad Pixels | Detector Aging |

---

# 13. Engineering Recommendations

建议：

- 首先确认坏点是否固定位置。
- 重新执行 Bad Pixel Calibration。
- 统计坏点数量及增长趋势。
- 判断坏点是否集中于局部区域。
- 若坏点持续增加，应重点检查 Photodiode、TFT 或 Sensor 老化。
- 超出产品规格时，应建议返厂维修或更换 Detector。

---

# 14. Relationship with Other Modules

## TFTFailure

Dead Pixel 最常见硬件来源。

---

## PhotodiodeFailure

Bright Pixel、Cold Pixel 主要来源。

---

## CalibrationFailure

解释坏点补偿失败原因。

---

## UniformityFailure

大量坏点会降低图像均匀性。

---

## DecisionTree

Bad Pixel Artifact 是硬件健康状态的重要判断依据。

---

# 15. Knowledge Graph

```text
Bad Pixel Artifact

├── Dead Pixel
├── Bright Pixel
├── Hot Pixel
├── Cold Pixel
├── Pixel Cluster
└── Progressive Bad Pixel

↓

Bad Pixel Calibration

↓

Hardware Analysis

├── TFT
├── Photodiode
├── ASIC
└── Sensor Array

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Bad Pixel Artifact 是 Flat Panel Detector 最常见且最稳定的图像异常之一，主要表现为 Dead Pixel、Bright Pixel、Hot Pixel、Cold Pixel 及 Pixel Cluster。其根因通常涉及 TFT 开路、Photodiode 损坏、暗电流增加、局部硬件损伤及探测器老化等。通过暗场测试、Flat Field 测试、Bad Pixel Calibration 及趋势分析，可快速判断坏点来源及严重程度，并结合 HardwareFailure、CalibrationFailure 与 DecisionTree 完成标准化故障定位，为产品质量评估和现场维修提供可靠依据。