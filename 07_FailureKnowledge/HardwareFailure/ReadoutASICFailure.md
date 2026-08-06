# ReadoutASICFailure

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
- GateDriverFailure.md
- ADCFailure.md
- ../../03_Hardware/ReadoutASIC.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

# 2. Scope

# 3. Readout ASIC Overview

- Readout ASIC 在 Detector 中的位置
- Charge Amplifier
- Integrator
- Sample & Hold
- Multiplexer
- ADC Interface
- Data Output

Signal Flow：

Photodiode

↓

TFT

↓

Data Line

↓

Charge Amplifier

↓

Sample & Hold

↓

MUX

↓

ADC

↓

FPGA

---

# 4. Failure Modes

- Input Channel Failure
- Charge Amplifier Failure
- Integrator Failure
- Sample & Hold Failure
- Multiplexer Failure
- Output Failure
- Bias Voltage Failure
- Clock Failure
- Configuration Failure
- Thermal Failure

---

# 5. Failure Mechanisms

## 5.1 Charge Amplifier Failure

影响：

- 信号幅值异常

表现：

- 图像整体偏暗
- SNR 降低

---

## 5.2 Input Channel Failure

表现：

- 单列异常
- 多列异常

---

## 5.3 Sample & Hold Failure

表现：

- 图像抖动
- 灰度不稳定

---

## 5.4 Multiplexer Failure

表现：

- 数据错位
- 图像重复
- 列顺序异常

---

## 5.5 Bias Failure

表现：

- Gain 漂移
- Offset 漂移

---

## 5.6 Clock Failure

表现：

- 图像随机异常
- 采样错误

---

# 6. Typical Image Symptoms

- Vertical Line
- Multi-column Failure
- Random Noise
- Band Noise
- Gray Shift
- Signal Saturation
- Image Clipping
- Missing Columns

---

# 7. Failure Impact

影响：

- Readout
- Calibration
- Image Generation

---

# 8. Detection Methods

- Offset Image
- Gain Image
- Raw Image
- Oscilloscope
- ASIC Register
- Clock Measurement
- Bias Measurement

---

# 9. Root Cause Analysis

Image Abnormal

↓

Column Related？

↓

YES

↓

ASIC Input

↓

Bias

↓

Clock

↓

MUX

↓

Confirm ASIC Failure

---

# 10. Common Failure Scenarios

- ASIC Aging
- ESD Damage
- Power Failure
- Overheating
- Configuration Error
- PCB Failure

---

# 11. Failure Severity

Minor

Moderate

Major

Critical

---

# 12. Engineering Recommendations

- 检查 Bias
- 检查 Clock
- 检查寄存器
- 检查输入信号
- 排除 ADC

---

# 13. Relationship

- GateDriverFailure
- ADCFailure
- ReadoutWorkflow
- DecisionTree

---

# 14. Knowledge Graph

Photodiode

↓

TFT

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Image

↓

Failure Analysis

↓

DecisionTree

---

# 15. Summary