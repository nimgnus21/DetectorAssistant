# TemperatureFailure

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
- HumidityFailure.md
- EMIFailure.md
- ../CalibrationFailure/OffsetCalibrationFailure.md
- ../CalibrationFailure/GainCalibrationFailure.md
- ../ImageFailure/NoiseArtifact.md
- ../ImageFailure/UniformityFailure.md
- ../HardwareFailure/ADCFailure.md
- ../HardwareFailure/PowerFailure.md
- ../../05_Calibration/
- ../../09_DecisionTree/

---

# 1. Purpose

Temperature Failure 描述数字平板探测器（Flat Panel Detector，FPD）由于环境温度超出正常工作范围或温度快速变化而导致的各种故障，包括图像质量下降、校准漂移、通信异常及系统稳定性下降等问题。

温度是影响 Flat Panel Detector 性能最重要的环境因素之一。无论是低温启动、高温连续工作，还是快速冷热变化，都可能影响探测器内部电子器件、模拟前端电路、光电二极管及校准参数的稳定性。

本文件回答的问题：

> **为什么 Detector 在高温或低温环境下容易出现图像异常、校准漂移或工作不稳定？如何快速确认温度是否为故障根因？**

---

# 2. Scope

适用于：

- Factory Environmental Test
- Reliability Test
- High Temperature Test
- Low Temperature Test
- Field Service
- Technical Support

适用于：

- High Temperature
- Low Temperature
- Thermal Drift
- Temperature Cycling
- Warm-up Stability

---

# 3. What is Temperature Failure

Temperature Failure 指：

**由于环境温度或设备自身温升导致 Detector 性能偏离正常工作状态，从而产生图像、校准或系统异常。**

主要表现：

- Offset Drift
- Gain Drift
- Noise Increase
- Uniformity Degradation
- Detector Restart
- Calibration Failure
- Communication Instability

---

# 4. Failure Classification

```text
Temperature Failure

├── High Temperature Failure
├── Low Temperature Failure
├── Temperature Drift
├── Warm-up Instability
├── Temperature Cycling Failure
└── Thermal Protection Trigger
```

---

# 5. Typical Symptoms

## 5.1 High Temperature Failure

特点：

- 连续工作后故障出现
- 温度升高时图像质量下降

可能原因：

- ADC Temperature Drift
- FPGA Temperature Rise
- Analog Circuit Drift

---

## 5.2 Low Temperature Failure

特点：

- 冷启动异常
- 启动速度变慢
- 图像灰度异常

可能原因：

- Electronic Component Characteristics
- Battery Performance Reduction（Wireless Detector）
- Oscillator Instability

---

## 5.3 Temperature Drift

特点：

- 图像随温度缓慢变化
- 多次曝光灰度不一致

可能原因：

- Offset Drift
- Gain Drift
- Analog Circuit Drift

---

## 5.4 Warm-up Instability

特点：

- 开机初期图像异常
- 工作一段时间后恢复正常

可能原因：

- Detector 未达到热稳定状态
- Offset 未稳定

---

## 5.5 Temperature Cycling Failure

特点：

- 冷热循环后出现间歇性故障

可能原因：

- Connector Expansion/Contraction
- Solder Joint Fatigue
- PCB Stress

---

## 5.6 Thermal Protection Trigger

特点：

- Detector 自动停止工作
- 自动重启
- 温度报警

可能原因：

- Internal Temperature Too High
- Cooling Failure

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| High Temperature | Internal Heat Accumulation |
| Low Temperature | Component Characteristics |
| Temperature Drift | ADC / Analog Circuit |
| Warm-up Instability | Offset Drift |
| Thermal Protection | Overheating |
| Temperature Cycling | Mechanical Stress |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| ADC | Offset Drift |
| FPGA | Processing Instability |
| Photodiode | Sensitivity Drift |
| Power Module | Efficiency Reduction |
| Main Board | Clock Drift |

---

# 8. Relationship with Calibration

Temperature Failure 可导致：

- Offset Calibration Failure
- Gain Calibration Failure
- Calibration Drift
- Calibration Verification Failure

因此：

- Calibration 应在规定温度范围内进行。
- Detector 应达到热稳定状态后再执行 Calibration。

---

# 9. Relationship with Image Failure

Temperature Failure 可能导致：

- Noise Artifact
- Uniformity Failure
- Offset Artifact
- Gain Artifact
- Ghost Artifact
- Brightness Drift

---

# 10. Diagnostic Workflow

```text
Image Abnormal

↓

Environment Temperature Normal？

↓

NO

↓

Return to Specified Temperature

↓

Repeat Test

↓

Recovered？

↓

YES

↓

Temperature Failure

↓

NO

↓

Warm-up Completed？

↓

NO

↓

Warm-up

↓

YES

↓

Calibration Verification

↓

Hardware Analysis
```

---

# 11. Detection Methods

## Ambient Temperature Verification

检查：

- 当前环境温度
- 是否超过产品规格

---

## Internal Temperature Monitoring

检查：

- FPGA Temperature
- ADC Temperature
- Main Board Temperature

---

## Warm-up Test

开机后：

- 立即采集
- 15 分钟
- 30 分钟
- 60 分钟

比较图像变化。

---

## Temperature Cycling Test

进行：

- High Temperature
- Low Temperature
- Thermal Cycling

观察故障是否复现。

---

## Calibration Verification

不同温度下：

- Offset Calibration
- Gain Calibration

比较 Calibration 数据变化。

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Image Stable After Warm-up | Temperature Drift |
| Noise Increases at High Temperature | ADC Drift |
| Uniformity Changes with Temperature | Gain Drift |
| Detector Restarts Automatically | Thermal Protection |
| Calibration Invalid After Temperature Change | Offset Drift |
| Cold Start Image Abnormal | Low Temperature Failure |

---

# 13. Engineering Recommendations

建议：

- 确保 Detector 在产品规定温度范围内运行。
- 校准前完成充分预热。
- 高温连续曝光时关注内部温度。
- 避免快速冷热切换。
- 若温度恢复正常后故障消失，应优先判定为环境因素。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## OffsetCalibrationFailure

温度变化可能导致 Offset 漂移。

---

## GainCalibrationFailure

温度变化可能导致 Gain 漂移。

---

## NoiseArtifact

高温可能导致噪声增加。

---

## PowerFailure

过热可能导致供电模块性能下降。

---

## DecisionTree

Temperature Failure 是环境故障分析的重要入口。

---

# 15. Knowledge Graph

```text
Temperature Failure

├── High Temperature
├── Low Temperature
├── Temperature Drift
├── Warm-up Instability
├── Temperature Cycling
└── Thermal Protection

↓

Temperature Verification

↓

Calibration Verification

↓

Image Analysis

↓

Hardware Analysis

├── ADC
├── FPGA
├── Power
├── Photodiode
└── Main Board

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Temperature Failure 是 Flat Panel Detector 最常见的环境类故障之一，可导致 Offset 漂移、Gain 漂移、噪声增加、均匀性下降、校准失效及系统稳定性降低。其影响通常具有随温度变化而变化、预热后改善或高温连续工作后恶化等特点。通过环境温度验证、内部温度监测、热稳定测试及校准验证，可快速确认温度是否为故障根因，并结合 Calibration Failure、Image Failure、Hardware Failure 与 DecisionTree 建立完整的温度故障分析体系。