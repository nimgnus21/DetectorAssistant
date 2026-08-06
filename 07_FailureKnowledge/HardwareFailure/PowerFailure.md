# PowerFailure

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
- MainBoardFailure.md
- ../../03_Hardware/Power.md
- ../../06_Workflow/PowerOnWorkflow.md
- ../../06_Workflow/ShutdownWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Power Failure 描述数字平板探测器（Flat Panel Detector，FPD）电源系统的典型故障模式、形成机理、图像表现、检测方法及根因分析。

Power System 是 Detector 的基础系统，为 FPGA、Memory、ADC、Readout ASIC、Gate Driver、Communication Module 等所有硬件模块提供稳定供电。任何电源异常都会影响整个 Detector 的稳定运行，因此 Power Failure 往往属于系统级故障。

本文件回答的问题：

> **Power System 为什么会发生故障？故障后会导致哪些系统及图像异常？**

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于：

- AC/DC Power
- DC/DC Converter
- Battery System（Wireless）
- Power Management
- Voltage Regulation
- Power Distribution

---

# 3. Power System Overview

Power System 的主要职责：

- External Power Input
- Battery Management（Wireless）
- DC/DC Conversion
- Voltage Regulation
- Power Sequencing
- Power Monitoring
- Over Current Protection
- Over Voltage Protection
- Under Voltage Protection

系统结构：

```text
External Power / Battery

↓

Power Management

↓

DC/DC Converter

↓

Power Distribution

├── FPGA
├── Memory
├── ADC
├── Readout ASIC
├── Gate Driver
├── Communication
└── Sensors
```

Power System 是所有模块正常工作的基础。

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| Power Input Failure | 输入电源异常 |
| DC/DC Failure | DC/DC 转换异常 |
| Voltage Drop | 电压下降 |
| Over Voltage | 过压 |
| Under Voltage | 欠压 |
| Ripple Noise | 电源纹波过大 |
| Power Sequence Failure | 上电时序异常 |
| Battery Failure | 电池异常 |
| Protection Circuit Failure | 保护电路异常 |
| Thermal Shutdown | 过热保护 |

---

# 5. Failure Mechanisms

## 5.1 Power Input Failure

外部供电异常。

影响：

- Detector 无法启动
- 系统掉电

典型表现：

- 无法开机
- 指示灯不亮

---

## 5.2 DC/DC Failure

DC/DC 转换器输出异常。

影响：

- 某一路电源失效

典型表现：

- FPGA 无法工作
- ADC 无法工作
- 局部模块掉电

---

## 5.3 Voltage Drop

输出电压低于规格。

影响：

- 数字逻辑不稳定
- 模拟电路性能下降

典型表现：

- 图像随机异常
- Detector 自动重启

---

## 5.4 Over Voltage

输出电压高于规格。

影响：

- 器件损坏
- 系统保护

典型表现：

- Detector 无法启动
- 元器件发热

---

## 5.5 Ripple Noise

输出纹波过大。

影响：

- 模拟信号受到干扰

典型表现：

- 图像噪声增加
- Band Noise
- Fixed Pattern Noise

---

## 5.6 Power Sequence Failure

上电顺序错误。

影响：

- FPGA Configuration Failure
- Memory Initialization Failure

典型表现：

- 初始化失败
- 系统无法 Ready

---

## 5.7 Battery Failure（Wireless）

包括：

- Battery Aging
- Capacity Loss
- Battery Protection Trigger

典型表现：

- 工作时间缩短
- 自动关机

---

## 5.8 Protection Circuit Failure

保护电路误动作或失效。

影响：

- 频繁断电
- 无法恢复供电

---

## 5.9 Thermal Shutdown

温度超过安全范围。

影响：

- 自动关闭电源

典型表现：

- 长时间运行后自动关机

---

# 6. Typical Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| Detector Cannot Power On | Input Failure |
| Random Restart | Voltage Drop |
| Image Noise | Ripple Noise |
| Initialization Failure | Power Sequence Failure |
| Communication Failure | Local Power Failure |
| Image Freeze | FPGA Power Failure |
| Automatic Shutdown | Thermal Protection |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| FPGA | 无法运行 |
| Memory | 初始化失败 |
| ADC | 转换异常 |
| Readout ASIC | 模拟采集异常 |
| Gate Driver | 行扫描异常 |
| Communication | 通信中断 |
| Entire Detector | 系统停止工作 |

---

# 8. Detection Methods

## Power Rail Measurement

检查：

- Input Voltage
- 12V
- 5V
- 3.3V
- 2.5V
- 1.8V
- 1.2V

---

## Oscilloscope Measurement

测量：

- Ripple
- Startup Sequence
- Voltage Stability

---

## Load Test

观察：

- 满载电压
- 动态响应
- 电压恢复时间

---

## Thermal Inspection

检查：

- DC/DC Temperature
- Power IC Temperature
- Battery Temperature

---

## System Log

检查：

- Power Alarm
- Brown-out
- Thermal Shutdown
- Battery Status

---

# 9. Root Cause Analysis

```text
Detector Cannot Start

↓

Input Power Normal？

↓

NO

↓

External Power Failure

↓

YES

↓

Power Rails Normal？

↓

NO

↓

DC/DC Failure

↓

YES

↓

Power Sequence Normal？

↓

NO

↓

Power Management Failure

↓

YES

↓

Check Main Board
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Adapter Failure | 电源适配器损坏 |
| DC/DC Module Failure | 电源模块故障 |
| Battery Aging | 电池老化 |
| Overheating | 电源过热 |
| Ripple Increase | 滤波器失效 |
| Short Circuit | 输出短路 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单路供电异常 |
| Moderate | 单模块掉电 |
| Major | 多模块异常 |
| Critical | Detector 无法启动 |

---

# 12. Engineering Recommendations

建议：

- 定期检查各路电源电压及纹波。
- 验证 Power Sequence 是否符合设计要求。
- 对无线产品定期检查 Battery Health。
- 使用示波器分析 DC/DC 输出稳定性。
- 排除 Main Board 短路及负载异常后，再确认 Power System 故障。

---

# 13. Relationship with Other Modules

## MainBoardFailure

Power System 为 Main Board 提供稳定供电。

Main Board 异常也可能导致 Power Distribution 异常。

---

## PowerOnWorkflow

Power System 是整个上电流程的起点。

---

## ShutdownWorkflow

正常关机依赖 Power Management 正确执行。

---

## DecisionTree

Power Failure 是以下诊断的重要节点：

- Detector Cannot Power On
- Random Restart
- Thermal Shutdown
- Initialization Failure
- Multiple Module Failure

---

# 14. Knowledge Graph

```text
External Power / Battery

↓

Power Management

├── Input Failure
├── DC/DC Failure
├── Voltage Drop
├── Over Voltage
├── Under Voltage
├── Ripple Noise
├── Power Sequence Failure
├── Battery Failure
└── Thermal Shutdown

↓

Power Distribution

↓

All Hardware Modules

↓

Image / System Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

Power Failure 是 Flat Panel Detector 最基础、影响范围最广的系统级硬件故障。其主要表现为输入电源异常、DC/DC 转换故障、电压异常、纹波过大、上电时序错误、电池故障及过热保护等。由于所有硬件模块均依赖稳定供电，Power Failure 往往会导致多模块同时异常，表现为无法开机、初始化失败、随机重启、图像噪声增加、通信中断或系统停机。故障分析应结合电源测量、纹波分析、温度监测及系统日志进行综合判断，为 DecisionTree 和现场维修提供可靠依据。