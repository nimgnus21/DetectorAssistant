# ImageArtifact

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
- LineArtifact.md
- NoiseArtifact.md
- UniformityFailure.md
- GhostArtifact.md
- BadPixelArtifact.md
- OffsetArtifact.md
- GainArtifact.md
- ImageDistortion.md
- ImageLoss.md
- ../HardwareFailure/
- ../SoftwareFailure/
- ../../05_Calibration/
- ../../06_Workflow/
- ../../09_DecisionTree/

---

# 1. Purpose

Image Artifact 描述数字平板探测器（Flat Panel Detector，FPD）中所有图像异常（Image Artifact）的分类、形成机理、表现形式、诊断方法及故障定位思路。

Image Artifact 是现场维修、质量分析及研发调试中最常见的问题，也是整个故障分析流程的起点。

Image Artifact 本身并不是故障原因，而是系统异常在最终 X-ray 图像中的表现。

本文件回答的问题：

> **图像出现异常时，应如何根据图像特征快速判断故障方向？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- 静态图像
- 动态图像
- 连续曝光
- 单次曝光
- 校准图像
- 临床图像

---

# 3. What is Image Artifact

Image Artifact 是指：

**由于 Detector 硬件、软件、校准、通信、环境或操作异常导致的非真实影像信息。**

Artifact 不代表被检测物体，而是系统自身产生的异常表现。

Artifact 可分为：

- 固定存在
- 随机出现
- 周期性出现
- 曝光相关
- 环境相关

---

# 4. Image Artifact Classification

按照图像表现分类：

```text
Image Artifact

├── Line Artifact
├── Noise Artifact
├── Uniformity Failure
├── Ghost Artifact
├── Bad Pixel Artifact
├── Offset Artifact
├── Gain Artifact
├── Image Distortion
├── Image Loss
└── Brightness / Contrast Abnormality
```

---

# 5. Classification by Image Characteristics

## 5.1 Geometry Artifact

特点：

- 行
- 列
- 条纹
- 网格
- 几何变形

典型原因：

- TFT
- Gate Driver
- Readout ASIC
- FPGA

---

## 5.2 Brightness Artifact

特点：

- 亮度异常
- 灰度异常
- 黑白反转
- 对比度异常

典型原因：

- ADC
- Calibration
- Configuration

---

## 5.3 Uniformity Artifact

特点：

- 整体亮度不一致
- 局部明暗

典型原因：

- Gain
- Offset
- Scintillator
- Photodiode

---

## 5.4 Noise Artifact

特点：

- 随机噪声
- 固定噪声
- 椒盐噪声

典型原因：

- ADC
- Power
- EMI
- Communication

---

## 5.5 Missing Data Artifact

特点：

- 图像缺失
- 图像截断
- 图像冻结

典型原因：

- FPGA
- Memory
- Communication

---

## 5.6 Defect Artifact

特点：

- Dead Pixel
- Bright Pixel
- Pixel Cluster

典型原因：

- TFT
- Photodiode
- Calibration

---

# 6. Classification by Failure Source

| Failure Source | Typical Artifact |
|----------------|------------------|
| TFT | Vertical Line |
| Gate Driver | Row Failure |
| Readout ASIC | Horizontal Line |
| ADC | Noise |
| FPGA | Image Corruption |
| Memory | Image Repeat |
| Power | Random Noise |
| Calibration | Uniformity Failure |
| Communication | Image Loss |
| Firmware | Image Freeze |

---

# 7. Classification by Stability

## Fixed Artifact

特点：

- 每张图都存在
- 位置固定

通常原因：

- Hardware
- Calibration

---

## Random Artifact

特点：

- 随机出现

通常原因：

- Power
- Communication
- EMI

---

## Periodic Artifact

特点：

- 周期性重复

通常原因：

- Clock
- Timing
- FPGA

---

## Environment Related Artifact

特点：

- 环境变化后出现

通常原因：

- Temperature
- Humidity
- Vibration
- EMI

---

# 8. Diagnostic Workflow

标准分析流程：

```text
Image Abnormal

↓

Determine Artifact Type

↓

Determine Distribution

↓

Determine Stability

↓

Determine Workflow Stage

↓

Determine Related Hardware

↓

Root Cause Analysis

↓

Solution Verification
```

---

# 9. Image Feature Analysis

分析图像时建议观察以下特征：

| Feature | Analysis Target |
|----------|-----------------|
| Position | 固定位置或随机位置 |
| Direction | 横向、纵向或斜向 |
| Shape | 点、线、块、带 |
| Brightness | 偏亮或偏暗 |
| Frequency | 连续、间隔或随机 |
| Repeatability | 是否重复出现 |
| Exposure Dependency | 是否与曝光有关 |
| Temperature Dependency | 是否与温度有关 |

---

# 10. Common Root Causes

| Artifact | Possible Root Cause |
|----------|---------------------|
| Vertical Line | TFT / Gate Driver |
| Horizontal Line | Readout ASIC |
| Noise | ADC / Power |
| Ghost | Scintillator / Offset |
| Bright Spot | Photodiode |
| Image Missing | FPGA / Communication |
| Uniformity Failure | Gain / Offset |
| Image Distortion | FPGA / Main Board |

---

# 11. Engineering Recommendations

建议按照以下顺序进行分析：

1. 确认图像异常类型。
2. 判断异常是否固定出现。
3. 判断异常是否随曝光变化。
4. 判断异常是否与温度、时间或环境相关。
5. 对照 Workflow 确定异常发生阶段。
6. 结合 Hardware、Software 与 Calibration 模块分析根因。
7. 使用 DecisionTree 完成最终定位。

---

# 12. Relationship with Other Modules

## HardwareFailure

解释图像异常对应的硬件根因。

---

## SoftwareFailure

解释软件导致的图像异常。

---

## Calibration

解释 Offset、Gain、Bad Pixel 等校准异常。

---

## Workflow

确定异常发生的流程阶段。

---

## DecisionTree

根据图像特征快速定位故障模块。

---

# 13. Knowledge Graph

```text
Image Artifact

├── Line Artifact
├── Noise Artifact
├── Uniformity Failure
├── Ghost Artifact
├── Bad Pixel Artifact
├── Offset Artifact
├── Gain Artifact
├── Image Distortion
└── Image Loss

↓

Image Feature Analysis

↓

Workflow Analysis

↓

Hardware / Software Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 14. Summary

Image Artifact 是 Flat Panel Detector 故障分析的入口，也是现场诊断最重要的依据。通过对图像异常的类型、分布、稳定性、亮度变化及出现规律进行系统分析，可快速判断异常属于硬件、软件、校准、通信还是环境因素导致，并结合 Workflow、HardwareFailure、SoftwareFailure 及 DecisionTree 完成标准化故障定位，提高现场诊断效率和准确性。