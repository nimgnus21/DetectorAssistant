# LineArtifact

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
- NoiseArtifact.md
- ../HardwareFailure/TFTFailure.md
- ../HardwareFailure/GateDriverFailure.md
- ../HardwareFailure/ReadoutASICFailure.md
- ../HardwareFailure/ADCFailure.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Line Artifact 描述数字平板探测器（Flat Panel Detector，FPD）中所有线状图像异常（Line Artifact）的典型表现、形成机理、故障来源、检测方法及根因分析。

Line Artifact 是 Detector 最具代表性的图像异常之一，其特征通常表现为横线、竖线或规则条纹。

由于 TFT、Gate Driver、Readout ASIC、ADC、FPGA 等模块均可能产生线状异常，因此 Line Artifact 是现场维修中最重要的图像分析内容之一。

本文件回答的问题：

> **图像出现横线、竖线或条纹时，应如何快速定位故障来源？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Vertical Line
- Horizontal Line
- Multiple Line
- Stripe Artifact
- Periodic Line

---

# 3. What is Line Artifact

Line Artifact 指：

**图像中沿行方向或列方向连续出现的异常亮线、暗线或条纹。**

主要特点：

- 连续出现
- 位置固定或重复
- 通常贯穿整幅图像
- 多数情况下具有硬件对应关系

---

# 4. Classification

```text
Line Artifact

├── Vertical Line
├── Horizontal Line
├── Multiple Vertical Lines
├── Multiple Horizontal Lines
├── Stripe Artifact
├── Periodic Line
└── Intermittent Line
```

---

# 5. Image Characteristics

## 5.1 Vertical Line

特点：

- 从图像顶部贯穿到底部
- 宽度通常为 1~数个 Pixel
- 固定位置重复出现

可能原因：

- TFT Failure
- Column Readout Failure
- ADC Channel Failure

---

## 5.2 Horizontal Line

特点：

- 从左至右贯穿整幅图像
- 固定位置

可能原因：

- Gate Driver Failure
- Readout ASIC Failure
- Timing Failure

---

## 5.3 Multiple Vertical Lines

特点：

- 多条等间距竖线
- 周期性明显

可能原因：

- ADC Channel Failure
- FPGA Data Mapping Error
- Readout ASIC Failure

---

## 5.4 Multiple Horizontal Lines

特点：

- 多条横线
- 连续出现

可能原因：

- Gate Driver Output Failure
- Clock Distribution Failure

---

## 5.5 Stripe Artifact

特点：

- 明暗相间
- 宽条纹
- 周期重复

可能原因：

- Gain Calibration Error
- ADC Offset Error
- Power Ripple

---

## 5.6 Intermittent Line

特点：

- 随机出现
- 重启后可能消失

可能原因：

- Connector Failure
- EMI
- Communication Error
- Power Instability

---

# 6. Typical Root Causes

| Artifact | Possible Root Cause |
|----------|---------------------|
| Single Vertical Line | TFT Failure |
| Multiple Vertical Lines | ADC / FPGA |
| Single Horizontal Line | Gate Driver |
| Multiple Horizontal Lines | Readout ASIC |
| Stripe Pattern | Gain / ADC |
| Random Line | Communication / Power |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Image Symptom |
|-----------------|----------------------|
| TFT | Vertical Line |
| Gate Driver | Horizontal Line |
| Readout ASIC | Multiple Horizontal Lines |
| ADC | Periodic Vertical Line |
| FPGA | Data Mapping Line |
| Main Board | Mixed Line Artifact |
| Power | Random Stripe |

---

# 8. Relationship with Workflow

Line Artifact 可能发生于以下流程：

| Workflow | Failure Stage |
|----------|---------------|
| AcquisitionWorkflow | Sensor Readout |
| ReadoutWorkflow | Row / Column Readout |
| ImageGenerationWorkflow | Data Reconstruction |
| ImageTransmissionWorkflow | Data Corruption |

---

# 9. Diagnostic Workflow

```text
Line Artifact

↓

Vertical？

↓

YES

↓

Single？

↓

YES

↓

TFT

↓

NO

↓

ADC / FPGA

↓

Horizontal？

↓

YES

↓

Gate Driver

↓

Multiple？

↓

Readout ASIC

↓

Stripe？

↓

Gain / Power

↓

Random？

↓

Communication / Connector
```

---

# 10. Detection Methods

## Image Analysis

观察：

- 行或列方向
- 宽度
- 长度
- 是否贯穿整幅图像

---

## Repeatability Test

检查：

- 每张图是否相同
- 是否固定位置

---

## Exposure Test

改变曝光条件：

观察：

- 是否随曝光变化

---

## Calibration Test

重新执行：

- Offset Calibration
- Gain Calibration

观察条纹是否消失。

---

## Hardware Verification

检查：

- TFT
- Gate Driver
- Readout ASIC
- ADC
- FPGA

---

# 11. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Single Bright Vertical Line | TFT 开路 |
| Single Dark Vertical Line | TFT 短路 |
| Horizontal Black Line | Gate Driver Failure |
| Multiple Bright Lines | ADC Channel Failure |
| Periodic Stripe | Gain Calibration Error |
| Random Horizontal Line | Power Instability |

---

# 12. Engineering Recommendations

建议：

- 首先确认异常方向（横向或纵向）。
- 判断异常是否固定位置。
- 判断是否与曝光条件有关。
- 结合 Calibration 排除 Offset/Gain 问题。
- 根据图像方向快速定位对应硬件模块。
- 使用 DecisionTree 进一步确认根因。

---

# 13. Relationship with Other Modules

## TFTFailure

重点分析纵向线状异常。

---

## GateDriverFailure

重点分析横向线状异常。

---

## ReadoutASICFailure

重点分析多行读出异常。

---

## ADCFailure

重点分析周期性条纹及通道异常。

---

## DecisionTree

Line Artifact 是图像诊断的重要入口，可快速缩小故障范围。

---

# 14. Knowledge Graph

```text
Line Artifact

├── Vertical Line
├── Horizontal Line
├── Multiple Line
├── Stripe
└── Intermittent Line

↓

Direction Analysis

↓

Hardware Mapping

├── TFT
├── Gate Driver
├── Readout ASIC
├── ADC
├── FPGA
└── Power

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 15. Summary

Line Artifact 是 Flat Panel Detector 最典型、最容易识别的图像异常之一，主要表现为纵向线、横向线、周期性条纹及随机线状伪影。由于 Detector 的读出架构具有明确的行列对应关系，因此线状异常通常能够直接映射到特定硬件模块，例如 TFT、Gate Driver、Readout ASIC、ADC 或 FPGA。通过分析线条方向、数量、位置、重复性及与曝光条件的关系，可快速完成故障定位，并结合 Calibration、Workflow 及 DecisionTree 进行进一步验证，为现场维修和研发分析提供标准化诊断依据。