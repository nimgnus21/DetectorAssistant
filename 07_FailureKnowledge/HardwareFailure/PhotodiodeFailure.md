# PhotodiodeFailure

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
- ScintillatorFailure.md
- TFTFailure.md
- ../../03_Hardware/Photodiode.md
- ../../06_Workflow/AcquisitionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Photodiode Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Photodiode（光电二极管）的典型故障模式、形成机理、图像表现、检测方法及影响范围。

Photodiode 是 Detector 信号转换链中的核心器件，其主要功能是将 Scintillator 输出的可见光转换为电荷信号。当 Photodiode 发生异常时，将直接影响像素信号质量，并导致后续 TFT、Readout ASIC 及图像处理流程产生异常。

本文件回答的问题是：

> **Photodiode 为什么会失效？失效后会产生哪些图像异常？**

---

# 2. Scope

适用于：

- a-Si Flat Panel Detector
- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于所有 Photodiode 相关故障分析。

---

# 3. Photodiode Overview

Photodiode 的主要功能：

- 接收 Scintillator 发出的可见光
- 将光能转换为电荷
- 将电荷存储于 Pixel 电容
- 等待 TFT 导通后完成读出

工作位置：

```text
X-ray

↓

Scintillator

↓

Photodiode

↓

Pixel Charge

↓

TFT

↓

Readout ASIC
```

Photodiode 是 Detector 信号产生的起点。

---

# 4. Failure Modes

Photodiode 常见故障模式如下：

| Failure Mode | Description |
|--------------|-------------|
| Open Circuit | 光电二极管开路 |
| Short Circuit | 光电二极管短路 |
| Leakage Current Increase | 漏电流增大 |
| Low Photoelectric Conversion Efficiency | 光电转换效率下降 |
| Aging | 老化 |
| Radiation Damage | 辐射损伤 |
| Manufacturing Defect | 制造缺陷 |
| Pixel Response Drift | 像素响应漂移 |

---

# 5. Failure Mechanisms

## 5.1 Open Circuit

Photodiode 与像素节点连接断开。

影响：

- 无法产生有效电荷
- Pixel 无响应

典型表现：

- Dead Pixel
- Dark Pixel

---

## 5.2 Short Circuit

Photodiode PN 结短路。

影响：

- 电荷无法正常积累
- Pixel 输出异常

典型表现：

- Bright Pixel
- Fixed Pixel

---

## 5.3 Leakage Current

暗电流增加。

影响：

- Charge Loss
- Offset 增加
- SNR 降低

典型表现：

- 图像噪声增加
- Uniformity 下降

---

## 5.4 Photoelectric Conversion Degradation

光电转换效率降低。

原因包括：

- Aging
- Radiation Damage
- 材料退化

影响：

- Detector Sensitivity 降低
- DQE 降低

典型表现：

- 图像整体偏暗
- 对比度下降

---

## 5.5 Radiation Damage

长期 X-ray 辐照导致 Photodiode 特性变化。

可能出现：

- 暗电流增加
- 响应下降
- 像素漂移

通常属于渐进式故障。

---

# 6. Failure Symptoms

Photodiode 故障可能产生以下图像表现：

| Symptom | Possible Cause |
|----------|----------------|
| Dead Pixel | Open Circuit |
| Bright Pixel | Short Circuit |
| Dark Area | Response Loss |
| Bright Area | Leakage |
| Increased Noise | Dark Current |
| Low Sensitivity | Aging |
| Uniformity Degradation | Response Drift |

说明：

上述现象也可能由 TFT、Calibration 或 Readout ASIC 导致，应结合其他证据分析。

---

# 7. Impact Analysis

Photodiode Failure 对系统的影响：

| Affected Module | Impact |
|-----------------|--------|
| Acquisition | 电荷生成异常 |
| Readout | 信号幅值异常 |
| Calibration | Offset/Gain 偏移 |
| Image Generation | 图像质量下降 |
| Clinical Imaging | 诊断质量降低 |

严重故障可能导致局部区域无法正常成像。

---

# 8. Detection Methods

推荐检测方法：

## Image Analysis

检查：

- Dead Pixel
- Bright Pixel
- Uniformity
- Noise

---

## Offset Image

观察：

- 固定异常点
- 暗电流分布

---

## Gain Image

观察：

- 像素响应一致性
- 光电转换效率

---

## Long Exposure Test

用于观察：

- Leakage
- Dark Current
- Response Drift

---

## Historical Comparison

比较：

- 新旧 Calibration
- 长期图像变化
- 同型号 Detector

---

# 9. Root Cause Analysis

建议分析流程：

```text
Image Abnormal

↓

Dead / Bright Pixel

↓

Offset Check

↓

Gain Check

↓

Photodiode Response

↓

Exclude TFT Failure

↓

Exclude ASIC Failure

↓

Confirm Photodiode Failure
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Manufacturing Defect | 出厂缺陷 |
| Long-term Aging | 长期老化 |
| High Dose Exposure | 长时间高剂量照射 |
| Material Degradation | 材料退化 |
| Pixel Characteristic Drift | 像素参数漂移 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单个像素异常 |
| Moderate | 局部区域响应下降 |
| Major | 大面积响应异常 |
| Critical | Detector 无法正常成像 |

---

# 12. Engineering Recommendations

建议：

- 定期执行 Offset 与 Gain Calibration。
- 持续监控 Dead Pixel 与 Bright Pixel 数量变化。
- 对长期使用设备建立响应趋势记录。
- 若异常持续扩大，应结合 Detector 历史数据判断是否存在 Photodiode 老化。
- 在确认 Photodiode 故障前，应排除 TFT、Readout ASIC、Calibration 等相关因素。

---

# 13. Relationship with Other Modules

## ScintillatorFailure

Scintillator 决定入射光质量。

Photodiode 决定光电转换效率。

---

## TFTFailure

Photodiode 负责产生电荷。

TFT 负责释放电荷。

---

## Calibration

Photodiode 漂移会影响：

- Offset
- Gain
- Defect

---

## DecisionTree

Photodiode Failure 是以下故障诊断的重要分支：

- Dead Pixel
- Bright Pixel
- Uniformity
- Noise

---

# 14. Knowledge Graph

```text
Scintillator

↓

Photodiode

├── Open Circuit
├── Short Circuit
├── Leakage
├── Aging
├── Radiation Damage
└── Response Drift

↓

Pixel Charge

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

Photodiode Failure 是 Detector 信号链中的关键硬件故障之一，其主要表现为光电转换效率下降、暗电流增加、开路、短路及响应漂移等异常。该类故障通常导致 Dead Pixel、Bright Pixel、Noise、Uniformity 下降及整体灵敏度降低。分析时应结合 Offset、Gain、图像表现及 Workflow，排除 TFT、Readout ASIC 和 Calibration 等相关因素后，再确认 Photodiode 为根本原因，为后续 DecisionTree 和 Service 提供可靠依据。