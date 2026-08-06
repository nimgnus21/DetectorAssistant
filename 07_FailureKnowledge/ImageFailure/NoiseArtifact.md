# NoiseArtifact

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
- ../HardwareFailure/ADCFailure.md
- ../HardwareFailure/PowerFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Noise Artifact 描述数字平板探测器（Flat Panel Detector，FPD）图像噪声（Noise Artifact）的分类、形成机理、图像表现、检测方法及根因分析。

Noise Artifact 是评价 Detector 图像质量的重要指标之一。图像噪声不仅降低图像信噪比（Signal-to-Noise Ratio，SNR），还可能掩盖细微病灶，影响临床诊断。

本文件回答的问题：

> **为什么图像会出现噪点、雪花、颗粒感或随机亮暗点？如何快速定位噪声来源？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Random Noise
- Fixed Pattern Noise
- Salt-and-Pepper Noise
- Stripe Noise
- Periodic Noise
- EMI Noise

---

# 3. What is Noise Artifact

Noise Artifact 指：

**Detector 在没有真实图像信息变化的情况下，输出随机或规律性的灰度波动。**

主要特点：

- 图像颗粒感增强
- 灰度随机波动
- 图像清晰度下降
- 信噪比降低
- 对比度下降

---

# 4. Classification

```text
Noise Artifact

├── Random Noise
├── Fixed Pattern Noise
├── Salt-and-Pepper Noise
├── Stripe Noise
├── Periodic Noise
├── Thermal Noise
├── EMI Noise
└── Shot Noise
```

---

# 5. Image Characteristics

## 5.1 Random Noise

特点：

- 随机分布
- 每幅图不同

可能原因：

- ADC Noise
- Power Noise
- High ISO / Low Dose

---

## 5.2 Fixed Pattern Noise

特点：

- 固定位置
- 每幅图一致

可能原因：

- Offset Error
- Gain Error
- ADC Offset

---

## 5.3 Salt-and-Pepper Noise

特点：

- 随机黑白点
- 数量较少

可能原因：

- Communication Error
- Memory Bit Error
- FPGA Error

---

## 5.4 Stripe Noise

特点：

- 行或列方向条纹
- 周期性明显

可能原因：

- ADC Channel Noise
- Power Ripple

---

## 5.5 Periodic Noise

特点：

- 固定周期重复

可能原因：

- Clock Noise
- FPGA Timing
- Switching Power Supply

---

## 5.6 Thermal Noise

特点：

- 温度升高时增加

可能原因：

- ADC
- Analog Front End
- Sensor Temperature

---

## 5.7 EMI Noise

特点：

- 环境变化时出现
- 随设备启停变化

可能原因：

- Electromagnetic Interference
- Poor Grounding
- Shield Failure

---

## 5.8 Shot Noise

特点：

- 剂量越低越明显

可能原因：

- X-ray Quantum Statistics
- Low Exposure

---

# 6. Typical Root Causes

| Noise Type | Possible Root Cause |
|------------|---------------------|
| Random Noise | ADC / Power |
| Fixed Pattern Noise | Offset / Gain |
| Stripe Noise | ADC Channel |
| Salt-and-Pepper Noise | Communication |
| Periodic Noise | Clock |
| Thermal Noise | Temperature |
| EMI Noise | Shielding |
| Shot Noise | Low Dose |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| ADC | Random Noise |
| Power Module | Ripple Noise |
| Main Board | Clock Noise |
| FPGA | Digital Noise |
| Communication Board | Data Noise |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Image Noise Increase |
| Calibration | Fixed Pattern Noise |
| SDK | Incorrect Image Processing |
| Driver | Data Corruption |

---

# 9. Relationship with Calibration

Noise Artifact 与 Calibration 密切相关。

主要关联：

- Offset Calibration
- Gain Calibration

Calibration 异常可能导致：

- Fixed Pattern Noise
- Stripe Noise
- Uniformity Degradation

---

# 10. Diagnostic Workflow

```text
Noise Observed

↓

Random？

↓

YES

↓

ADC / Power

↓

Fixed？

↓

Offset / Gain

↓

Stripe？

↓

ADC Channel

↓

Periodic？

↓

Clock / FPGA

↓

Temperature Related？

↓

Thermal Noise

↓

Environment Related？

↓

EMI
```

---

# 11. Detection Methods

## Dark Image Test

检查：

- Background Noise
- Random Noise

---

## Flat Field Test

检查：

- Fixed Pattern Noise
- Stripe Noise

---

## Noise Measurement

测量：

- SNR
- RMS Noise
- Standard Deviation

---

## Temperature Test

比较：

- 冷启动
- 热稳定

观察噪声变化。

---

## EMI Verification

关闭附近设备：

观察：

- Noise 是否消失

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Grainy Image | Random Noise |
| Stripe Noise | ADC Channel Failure |
| Snow-like Image | EMI Noise |
| Fixed Texture | Offset Calibration Failure |
| Noise After Warm-up | Thermal Noise |
| Noise During Exposure | Power Ripple |

---

# 13. Engineering Recommendations

建议：

- 首先确认噪声属于随机还是固定模式。
- 检查曝光剂量是否过低。
- 重新执行 Offset 与 Gain Calibration。
- 排查供电质量及接地情况。
- 检查 ADC、FPGA 及时钟信号稳定性。
- 使用 DecisionTree 完成根因分析。

---

# 14. Relationship with Other Modules

## ADCFailure

Noise Artifact 最常见硬件来源。

---

## PowerFailure

供电纹波会导致随机噪声及条纹噪声。

---

## CalibrationFailure

Offset/Gain 校准异常会产生固定模式噪声。

---

## DecisionTree

Noise Artifact 是图像质量分析的重要入口。

---

# 15. Knowledge Graph

```text
Noise Artifact

├── Random Noise
├── Fixed Pattern Noise
├── Salt-and-Pepper Noise
├── Stripe Noise
├── Periodic Noise
├── Thermal Noise
├── EMI Noise
└── Shot Noise

↓

Noise Classification

↓

Hardware Analysis

├── ADC
├── Power
├── FPGA
├── Clock
└── Communication

↓

Calibration Analysis

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Noise Artifact 是 Flat Panel Detector 最常见的图像质量异常之一，主要表现为随机噪声、固定模式噪声、条纹噪声、周期噪声、热噪声及电磁干扰噪声等。其根因通常涉及 ADC、Power Module、Clock、FPGA、Communication、Offset/Gain Calibration 以及曝光剂量等多个因素。通过 Dark Image、Flat Field、SNR 测试、温度测试及 EMI 排查，可快速定位噪声来源，并结合 HardwareFailure、CalibrationFailure 与 DecisionTree 建立标准化噪声分析流程。