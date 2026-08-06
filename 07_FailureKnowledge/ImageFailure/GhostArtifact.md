# GhostArtifact

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
- ../HardwareFailure/ScintillatorFailure.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/OffsetCalibration.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Ghost Artifact 描述数字平板探测器（Flat Panel Detector，FPD）图像残影（Ghost Artifact）的典型表现、形成机理、故障来源、检测方法及根因分析。

Ghost Artifact 是指上一幅曝光图像的信息残留在后续图像中，即使当前曝光对象已经改变，图像中仍然可以观察到前一次曝光留下的轮廓或灰度信息。

Ghost Artifact 会降低图像真实性，影响临床诊断，是图像质量评价的重要项目之一。

本文件回答的问题：

> **为什么上一张图像会残留到下一张图像？如何判断残影的真正来源？**

---

# 2. Scope

适用于：

- Dynamic Imaging
- Continuous Exposure
- Clinical Imaging
- Factory Test
- Engineering Debug
- Technical Support

适用于：

- Ghost Artifact
- Image Lag
- Residual Image
- Afterimage

---

# 3. What is Ghost Artifact

Ghost Artifact 指：

**前一次曝光形成的图像信息，在后续曝光过程中仍然部分保留，并叠加到新的图像中。**

主要特点：

- 前一幅图像轮廓仍可见
- 高曝光区域最明显
- 多次曝光后逐渐减弱
- 固定曝光条件下可重复出现

---

# 4. Classification

```text
Ghost Artifact

├── Temporary Ghost
├── Persistent Ghost
├── Local Ghost
├── Global Ghost
├── Motion Ghost
└── Image Lag
```

---

# 5. Image Characteristics

## 5.1 Temporary Ghost

特点：

- 残影持续 1～3 帧
- 随连续曝光逐渐消失

可能原因：

- Photodiode Charge Residual
- Offset Recovery Delay

---

## 5.2 Persistent Ghost

特点：

- 长时间存在
- 多次曝光后仍明显

可能原因：

- Scintillator Aging
- Photodiode Defect

---

## 5.3 Local Ghost

特点：

- 局部区域存在残影
- 多发生于高剂量曝光区域

可能原因：

- Local Photodiode Saturation
- Local Scintillator Damage

---

## 5.4 Global Ghost

特点：

- 整幅图像均存在残影

可能原因：

- Offset Correction Failure
- Firmware Correction Failure

---

## 5.5 Motion Ghost

特点：

- 连续动态图像中出现拖影

可能原因：

- Long Image Lag
- Readout Delay

---

## 5.6 Image Lag

特点：

- 图像逐帧衰减
- 灰度缓慢恢复

可能原因：

- Charge Release Delay
- Detector Recovery Delay

---

# 6. Typical Root Causes

| Ghost Artifact | Possible Root Cause |
|----------------|---------------------|
| Whole Image Ghost | Offset Calibration Failure |
| Local Ghost | Photodiode Failure |
| Persistent Ghost | Scintillator Aging |
| Motion Ghost | Firmware Timing Error |
| Residual Image | Charge Residual |
| Long Recovery | Detector Recovery Delay |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Scintillator | Persistent Ghost |
| Photodiode | Local Ghost |
| TFT | Charge Release Delay |
| Readout ASIC | Slow Readout |
| FPGA | Timing Delay |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Calibration | Ghost Enhancement |
| Firmware | Incorrect Offset Update |
| Configuration | Wrong Recovery Parameter |
| SDK | Incorrect Image Processing |

---

# 9. Relationship with Calibration

Ghost Artifact 与 Offset Calibration 密切相关。

若 Offset 未及时更新：

可能导致：

- Residual Image
- Background Ghost
- Gray Level Shift

Gain Calibration 一般不会直接产生 Ghost，但可能放大 Ghost 的可见程度。

---

# 10. Diagnostic Workflow

```text
Ghost Image

↓

Previous Image Visible？

↓

YES

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

Photodiode

↓

Persistent？

↓

YES

↓

Scintillator

↓

Motion Only？

↓

YES

↓

Firmware Timing
```

---

# 11. Detection Methods

## Ghost Test

使用标准 Ghost Test Pattern：

- 高剂量曝光
- 空曝光
- 连续采集

观察残影变化。

---

## Continuous Exposure Test

连续采集多帧：

观察：

- Ghost 衰减速度
- 恢复时间

---

## Offset Calibration Verification

重新执行：

- Offset Calibration

验证 Ghost 是否改善。

---

## Temperature Test

不同温度下测试：

观察：

- Ghost 强度
- 恢复时间

---

## Hardware Inspection

检查：

- Scintillator
- Photodiode
- ASIC
- FPGA

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Previous Bone Image Visible | Ghost Artifact |
| High Dose Residual Image | Charge Residual |
| Ghost After Long Exposure | Photodiode Saturation |
| Ghost After Calibration Failure | Offset Failure |
| Motion Imaging Ghost | Firmware Timing Error |
| Persistent Local Ghost | Scintillator Damage |

---

# 13. Engineering Recommendations

建议：

- 优先确认 Ghost 是否能够自然衰减。
- 重新执行 Offset Calibration。
- 比较不同曝光剂量下 Ghost 变化。
- 确认是否仅发生于局部区域。
- 检查 Scintillator 与 Photodiode 是否存在老化或损伤。
- 使用 DecisionTree 完成根因分析。

---

# 14. Relationship with Other Modules

## OffsetArtifact

Offset 校正异常是 Ghost 的主要软件原因。

---

## CalibrationFailure

Calibration Failure 会导致 Ghost 无法有效消除。

---

## PhotodiodeFailure

解释局部 Ghost 的硬件来源。

---

## ScintillatorFailure

解释长期 Persistent Ghost 的形成机理。

---

## DecisionTree

Ghost Artifact 是动态成像质量分析的重要节点。

---

# 15. Knowledge Graph

```text
Ghost Artifact

├── Temporary Ghost
├── Persistent Ghost
├── Local Ghost
├── Global Ghost
├── Motion Ghost
└── Image Lag

↓

Calibration Analysis

↓

Hardware Analysis

├── Photodiode
├── Scintillator
├── TFT
├── ASIC
└── FPGA

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Ghost Artifact 是 Flat Panel Detector 中典型的动态图像异常，主要表现为上一幅图像信息残留于后续图像中。其根因通常包括 Photodiode 电荷残留、Scintillator 老化、Offset Calibration 异常、Firmware 时序错误及 Detector 恢复延迟等。通过 Ghost Test、连续曝光测试、Offset 校准验证及硬件检查，可快速判断残影来源，并结合 DecisionTree 完成标准化故障定位，为研发、生产及现场技术支持提供统一的分析依据。