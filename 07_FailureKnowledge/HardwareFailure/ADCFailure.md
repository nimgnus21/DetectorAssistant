# ADCFailure

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
- ReadoutASICFailure.md
- FPGAFailure.md
- ../../03_Hardware/ADC.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

ADC Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Analog-to-Digital Converter（ADC）的典型故障模式、形成机理、图像表现、检测方法及根因分析。

ADC 位于 Detector 模拟信号链与数字信号链之间，其负责将 Readout ASIC 输出的模拟电压转换为数字灰度数据，是图像数字化的关键环节。

ADC 工作异常不会改变 X-ray 信号本身，而会导致灰度值计算错误，从而影响图像质量、动态范围及后续数字图像处理。

本文件回答的问题：

> **ADC 为什么会发生故障？故障后会导致哪些图像异常？**

---

# 2. Scope

适用于：

- a-Si Flat Panel Detector
- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于所有 ADC 相关故障分析。

---

# 3. ADC Overview

ADC（Analog-to-Digital Converter）负责将模拟电压转换为数字灰度值。

主要职责：

- Analog Signal Sampling
- Analog-to-Digital Conversion
- Gray Level Quantization
- Digital Data Output

信号流程：

```text
Photodiode

↓

TFT

↓

Readout ASIC

↓

Analog Signal

↓

ADC

↓

Digital Image Data

↓

FPGA
```

正常情况下：

- 输入模拟信号连续变化
- ADC 按采样时钟完成采样
- 输出固定 Bit Depth 数字数据
- 灰度值与输入电压保持线性关系

---

# 4. Failure Modes

ADC 常见故障模式如下：

| Failure Mode | Description |
|--------------|-------------|
| Reference Voltage Failure | 基准电压异常 |
| Sampling Clock Failure | 采样时钟异常 |
| Gain Error | 增益误差 |
| Offset Error | 偏置误差 |
| Quantization Error | 量化误差 |
| Bit Error | 数据位错误 |
| Channel Failure | 通道失效 |
| Saturation Failure | 饱和异常 |
| Thermal Drift | 温度漂移 |
| ADC IC Failure | ADC 芯片故障 |

---

# 5. Failure Mechanisms

## 5.1 Reference Voltage Failure

ADC 基准电压异常。

影响：

- 全局灰度计算错误
- Dynamic Range 改变

典型表现：

- 图像整体偏亮
- 图像整体偏暗
- 灰阶压缩

---

## 5.2 Sampling Clock Failure

采样时钟频率异常。

影响：

- 数据采样错误
- Sampling Miss

典型表现：

- 图像随机噪声
- 灰度跳变

---

## 5.3 Gain Error

ADC 增益发生偏移。

影响：

- Gray Scale Stretch
- Gray Scale Compression

典型表现：

- 对比度异常
- Gain Calibration 无法完全修正

---

## 5.4 Offset Error

ADC Offset 偏移。

影响：

- Gray Baseline Shift

典型表现：

- 图像整体偏亮
- 图像整体偏暗
- Offset Image 异常

---

## 5.5 Quantization Error

ADC 分辨率不足或量化异常。

影响：

- Gray Step 增加
- Dynamic Range 降低

典型表现：

- 灰阶断层
- 图像层次减少

---

## 5.6 Bit Error

ADC 输出 Bit 数据错误。

影响：

- Gray Value 错误
- 数字数据异常

典型表现：

- 固定灰阶错误
- 条纹
- 周期性噪声

---

## 5.7 Channel Failure

多通道 ADC 某一路失效。

影响：

- 对应输入无法转换

典型表现：

- 固定列异常
- 多列灰度错误

---

## 5.8 Saturation Failure

ADC 提前进入饱和状态。

影响：

- 高灰度信息丢失

典型表现：

- 图像过曝
- 白色区域无细节

---

## 5.9 Thermal Drift

ADC 温度变化导致参数漂移。

影响：

- Gain Drift
- Offset Drift

典型表现：

- 图像质量随温度变化
- 长时间工作后灰度漂移

---

# 6. Typical Image Symptoms

| Image Symptom | Possible Cause |
|---------------|----------------|
| Gray Shift | Offset Error |
| Low Contrast | Gain Error |
| Image Saturation | Saturation Failure |
| Band Noise | Sampling Failure |
| Random Noise | Clock Failure |
| Gray Level Jump | Quantization Error |
| Column Gray Difference | Channel Failure |
| Dynamic Range Reduction | Reference Voltage Failure |

说明：

ADC 故障通常影响灰度计算，不会直接产生 Dead Pixel 或 Bright Pixel。

---

# 7. Failure Impact

ADC Failure 对系统的影响：

| Module | Impact |
|---------|--------|
| Readout | 数字转换异常 |
| FPGA | 接收错误数据 |
| Calibration | Gain / Offset 校正异常 |
| Image Generation | 灰度计算异常 |
| Clinical Diagnosis | 图像质量下降 |

---

# 8. Detection Methods

推荐检测方法：

## Offset Image

检查：

- 灰度基线
- Offset 漂移

---

## Gain Image

检查：

- 灰度响应
- Gain 一致性

---

## Raw Image

检查：

- Gray Step
- Saturation
- Bit Error

---

## Oscilloscope Measurement

测量：

- Sampling Clock
- Reference Voltage
- Analog Input

---

## ADC Register Verification

检查：

- Gain Configuration
- Offset Configuration
- Sampling Mode

---

## Temperature Test

观察：

- 温升后的 Gray Drift
- 长时间运行稳定性

---

# 9. Root Cause Analysis

推荐分析流程：

```text
Gray Level Abnormal

↓

Raw Image Normal ?

↓

NO

↓

Analog Signal Normal ?

↓

YES

↓

Check ADC

├── Reference Voltage
├── Clock
├── Gain
├── Offset
├── Bit Output
└── Channel Status

↓

Confirm ADC Failure
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Reference Voltage Instability | 基准源异常 |
| ADC IC Aging | 芯片老化 |
| Sampling Clock Failure | 时钟异常 |
| Thermal Drift | 温度漂移 |
| Power Noise | 电源噪声 |
| Configuration Error | 参数配置错误 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 灰度轻微偏移 |
| Moderate | 对比度下降 |
| Major | 大面积灰度异常 |
| Critical | 图像无法正确数字化 |

---

# 12. Engineering Recommendations

建议：

- 定期验证 ADC Reference Voltage。
- 使用示波器检查 Sampling Clock。
- 检查 ADC Gain、Offset 配置。
- 对比 Analog Signal 与 Digital Output。
- 排除 Readout ASIC、FPGA 和电源因素后，再确认 ADC 故障。

---

# 13. Relationship with Other Modules

## ReadoutASICFailure

Readout ASIC 输出模拟信号。

ADC 将模拟信号转换为数字数据。

---

## FPGAFailure

ADC 输出数字数据。

FPGA 负责数字数据接收、缓存和处理。

---

## ReadoutWorkflow

ADC 是 Readout Workflow 中模拟信号数字化的核心节点。

---

## DecisionTree

ADC Failure 是以下诊断的重要节点：

- Gray Shift
- Low Contrast
- Band Noise
- Dynamic Range Reduction
- Saturation
- Bit Error

---

# 14. Knowledge Graph

```text
Readout ASIC

↓

Analog Signal

↓

ADC

├── Reference Voltage Failure
├── Sampling Clock Failure
├── Gain Error
├── Offset Error
├── Quantization Error
├── Bit Error
├── Channel Failure
├── Saturation Failure
└── Thermal Drift

↓

Digital Image Data

↓

FPGA

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

ADC Failure 是 Flat Panel Detector 数字化链路中的关键故障，其主要表现为基准电压异常、采样时钟故障、增益偏移、偏置误差、量化错误、位错误及通道失效等。由于 ADC 负责模拟信号向数字灰度数据的转换，因此故障通常表现为灰度偏移、动态范围下降、灰阶跳变、条带噪声及图像饱和等问题。故障分析应结合 Raw Image、Sampling Clock、Reference Voltage、Readout ASIC 输出及 FPGA 输入进行综合判断，以准确定位 ADC 故障根因，并为 DecisionTree 和现场维修提供可靠依据。