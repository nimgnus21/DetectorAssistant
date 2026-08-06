# PowerQualityFailure

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
- TemperatureFailure.md
- HumidityFailure.md
- EMIFailure.md
- VibrationFailure.md
- ../HardwareFailure/PowerFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../HardwareFailure/FPGAFailure.md
- ../ImageFailure/NoiseArtifact.md
- ../ImageFailure/ImageLoss.md
- ../../06_Workflow/StartupWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Power Quality Failure 描述数字平板探测器（Flat Panel Detector，FPD）由于供电质量异常导致的各种故障，包括电压异常、电流异常、电源纹波、电压跌落、浪涌、接地异常及瞬时断电等问题。

Detector 的模拟前端、ADC、FPGA、通信模块及电源管理系统均依赖稳定的供电。当供电质量不符合要求时，即使硬件本身正常，也可能导致系统运行异常、图像质量下降或设备无法正常工作。

本文件回答的问题：

> **为什么 Detector 在某些医院或机房频繁出现随机故障？为什么更换电源后故障消失？**

---

# 2. Scope

适用于：

- Factory Test
- EMC Test
- Reliability Test
- Installation
- Field Service
- Technical Support

适用于：

- AC Power
- DC Power
- Battery Power
- External Power Adapter
- Hospital Power System

---

# 3. What is Power Quality Failure

Power Quality Failure 指：

**由于供电质量异常导致 Detector 电源系统无法稳定工作，从而影响图像采集、数据处理及通信功能。**

主要表现：

- Detector Restart
- Startup Failure
- Communication Failure
- Noise Increase
- Image Loss
- Calibration Failure
- Random System Failure

---

# 4. Failure Classification

```text
Power Quality Failure

├── Undervoltage
├── Overvoltage
├── Voltage Drop
├── Voltage Ripple
├── Surge / Transient
├── Ground Failure
├── Power Interruption
└── Battery Power Failure
```

---

# 5. Typical Symptoms

## 5.1 Undervoltage

特点：

- 无法启动
- 自动关机
- 系统重启

可能原因：

- 电源输出不足
- 电缆压降
- 电池电量不足

---

## 5.2 Overvoltage

特点：

- 系统保护
- 电源报警

可能原因：

- 电源异常
- 外部供电错误

---

## 5.3 Voltage Drop

特点：

- 曝光瞬间重启
- 大负载时异常

可能原因：

- 电源容量不足
- 电缆阻抗过大

---

## 5.4 Voltage Ripple

特点：

- 图像噪声增加
- ADC 数据波动

可能原因：

- DC/DC Converter
- Filter Failure
- Poor Power Supply

---

## 5.5 Surge / Transient

特点：

- 偶发重启
- 数据损坏

可能原因：

- 雷击
- 大型设备启动
- 电网浪涌

---

## 5.6 Ground Failure

特点：

- 通信异常
- EMI 增加
- 图像噪声

可能原因：

- Ground Open
- Ground Loop
- Poor Earth Connection

---

## 5.7 Power Interruption

特点：

- 系统突然断电
- 图像丢失

可能原因：

- AC Power Failure
- Adapter Failure

---

## 5.8 Battery Power Failure

特点：

- Wireless Detector 工作时间缩短
- 电量显示异常

可能原因：

- Battery Aging
- Battery Protection
- Battery Failure

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Startup Failure | Undervoltage |
| Random Restart | Voltage Drop |
| Noise Increase | Ripple |
| Communication Failure | Ground Failure |
| Detector Shutdown | Power Loss |
| Short Runtime | Battery Aging |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Power Module | Voltage Instability |
| FPGA | Unexpected Reset |
| ADC | Noise Increase |
| Communication Board | Packet Loss |
| Main Board | System Restart |

---

# 8. Relationship with Image Failure

Power Quality Failure 可导致：

- Noise Artifact
- Image Loss
- Line Artifact
- Uniformity Failure
- Random Artifact

---

# 9. Relationship with Calibration

供电异常可能导致：

- Offset Calibration Failure
- Gain Calibration Failure
- Calibration Data Corruption
- Calibration Repeatability Poor

Calibration 应在稳定供电条件下执行。

---

# 10. Diagnostic Workflow

```text
Power Related Failure

↓

Power Supply Stable？

↓

NO

↓

Measure Voltage

↓

Measure Ripple

↓

Check Ground

↓

Power Restored？

↓

YES

↓

Power Quality Failure

↓

NO

↓

Hardware Analysis
```

---

# 11. Detection Methods

## Input Voltage Measurement

检查：

- AC Input Voltage
- DC Output Voltage
- Voltage Stability

---

## Ripple Measurement

使用示波器检查：

- Ripple Voltage
- Switching Noise

---

## Ground Inspection

检查：

- Ground Resistance
- Protective Earth
- Ground Loop

---

## Battery Verification

检查：

- Battery Voltage
- Battery Capacity
- Charge Cycle
- Battery Health

---

## Dynamic Load Test

在曝光及连续采集过程中监测：

- Voltage Drop
- Current Change
- Power Stability

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Detector Restarts During Exposure | Voltage Drop |
| Noise Appears on All Images | Ripple |
| Communication Randomly Disconnects | Ground Failure |
| Detector Cannot Start | Undervoltage |
| Battery Runtime Becomes Very Short | Battery Aging |
| Failure After Lightning Storm | Surge Damage |

---

# 13. Engineering Recommendations

建议：

- 使用符合规格的电源适配器。
- 定期检查医院供电系统及接地质量。
- 避免与大功率设备共用电源回路。
- 定期检测电池健康状态（Wireless Detector）。
- 使用示波器检测纹波及瞬态干扰。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## PowerFailure

Power Module 自身故障分析。

---

## EMIFailure

供电质量异常可能伴随 EMI 问题。

---

## CommunicationFailure

供电波动可能导致通信异常。

---

## CalibrationFailure

供电不稳定可能导致 Calibration 失败。

---

## DecisionTree

Power Quality Failure 是现场环境故障的重要诊断入口。

---

# 15. Knowledge Graph

```text
Power Quality Failure

├── Undervoltage
├── Overvoltage
├── Voltage Drop
├── Ripple
├── Surge
├── Ground Failure
├── Power Interruption
└── Battery Failure

↓

Power Verification

↓

Voltage Measurement

↓

Ground Inspection

↓

Hardware Analysis

├── Power Module
├── FPGA
├── ADC
├── Communication
└── Main Board

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Power Quality Failure 是 Flat Panel Detector 现场应用中最常见的环境故障之一，主要包括欠压、过压、电压跌落、纹波、浪涌、接地异常及电池性能下降等问题。其典型表现包括设备无法启动、随机重启、通信异常、图像噪声增加、校准失败及图像丢失。通过电压测量、纹波分析、接地检查、电池检测及动态负载测试，可快速确认供电质量是否为故障根因，并结合 Hardware Failure、Calibration Failure、Image Failure 与 DecisionTree 建立完整的供电环境故障分析体系。