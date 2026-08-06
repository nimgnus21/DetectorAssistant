# GateDriverFailure

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
- TFTFailure.md
- ReadoutASICFailure.md
- ../../03_Hardware/GateDriver.md
- ../../06_Workflow/AcquisitionWorkflow.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Gate Driver Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Gate Driver 的典型故障模式、形成机理、图像表现、检测方法及根因分析。

Gate Driver 是 Detector 行扫描（Row Scan）的控制核心，其负责按照设定时序依次输出 Gate Pulse，驱动 TFT 阵列逐行导通，使 Pixel 电荷能够顺序输出至 Data Line。

由于 Gate Driver 控制整个 Row 的工作，因此其故障通常表现为**整行或多行异常**，而不是单个 Pixel 异常。

本文件回答的问题：

> **Gate Driver 为什么会发生故障？故障后会产生哪些图像异常？**

---

# 2. Scope

适用于：

- a-Si Flat Panel Detector
- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于所有 Gate Driver 相关故障分析。

---

# 3. Gate Driver Overview

Gate Driver 的主要职责：

- 产生 Gate Pulse
- 控制 Row Scan
- 驱动 TFT 导通
- 控制 Pixel Readout Timing
- 保证整幅图像按正确顺序完成采集

工作流程：

```text
FPGA

↓

Timing Generator

↓

Gate Driver

↓

Gate Line

↓

TFT Array

↓

Pixel Readout

↓

Readout ASIC
```

正常情况下：

- 每次仅有一行 Gate Pulse 有效
- 所有 Row 按顺序依次扫描
- Gate Pulse 宽度、幅值及周期保持一致

---

# 4. Failure Modes

Gate Driver 常见故障模式如下：

| Failure Mode | Description |
|--------------|-------------|
| No Gate Output | 无 Gate 输出 |
| Gate Pulse Missing | Gate Pulse 丢失 |
| Low Gate Voltage | Gate 电压不足 |
| High Gate Voltage | Gate 电压异常升高 |
| Timing Error | 行扫描时序异常 |
| Clock Failure | Gate Clock 丢失 |
| Driver IC Failure | Driver IC 损坏 |
| Multi-channel Failure | 多通道异常 |
| Partial Channel Failure | 部分通道异常 |
| Flexible Cable Failure | FPC 连接异常 |

---

# 5. Failure Mechanisms

## 5.1 No Gate Output

Gate Driver 无输出。

影响：

- 对应 Row TFT 永远不导通
- Charge 无法读出

典型表现：

- 固定黑线
- 整行无信号

---

## 5.2 Gate Pulse Missing

某一行 Pulse 消失。

影响：

- 单行无法采集

典型表现：

- 单条水平黑线
- 固定 Row 异常

---

## 5.3 Low Gate Voltage

Gate Voltage 无法达到 TFT 导通电压。

影响：

- TFT 导通不完全
- Charge Transfer 不充分

典型表现：

- 行亮度降低
- Horizontal Band

---

## 5.4 High Gate Voltage

Gate 电压过高。

影响：

- TFT 长时间导通
- Pixel Charge 提前释放

典型表现：

- 行亮度异常
- Blooming
- 图像拖尾

---

## 5.5 Timing Error

扫描时序错误。

包括：

- Pulse Width 异常
- Pulse Delay
- Scan Order Error

影响：

- Readout Timing 错误
- Image Distortion

---

## 5.6 Clock Failure

Gate Clock 丢失或频率异常。

影响：

- Scan 停止
- 行扫描错乱

典型表现：

- 图像停止更新
- 大面积水平异常

---

## 5.7 Driver IC Failure

Gate Driver 芯片内部损坏。

可能导致：

- 单通道异常
- 多通道异常
- 全部输出失效

---

## 5.8 Flexible Cable Failure

Gate Driver 与 TFT 阵列之间连接异常。

影响：

- 部分 Gate Line 开路
- 间歇性接触不良

典型表现：

- 多条固定水平线
- 敲击或弯折后故障变化

---

# 6. Typical Image Symptoms

| Image Symptom | Possible Cause |
|---------------|----------------|
| Single Horizontal Line | Gate Pulse Missing |
| Multiple Horizontal Lines | Multi-channel Failure |
| Horizontal Black Band | No Gate Output |
| Horizontal Bright Band | Gate Voltage Abnormal |
| Periodic Horizontal Artifact | Clock Failure |
| Partial Image Missing | Timing Error |
| Image Misalignment | Scan Timing Error |

说明：

若异常随曝光重复出现在固定行位置，应优先检查 Gate Driver。

---

# 7. Failure Impact

Gate Driver Failure 对系统的影响：

| Module | Impact |
|---------|--------|
| Acquisition | 行扫描异常 |
| TFT | 无法正常导通 |
| Readout | Charge 无法输出 |
| Calibration | 校正数据异常 |
| Image Generation | 图像缺行、横向伪影 |

---

# 8. Detection Methods

推荐检测方法：

## Image Analysis

检查：

- 水平线
- Row Band
- 固定位置异常

---

## Offset Image

观察：

- 固定 Row 是否异常

---

## Gain Image

检查：

- 是否存在整行响应差异

---

## Oscilloscope Measurement

测量：

- Gate Pulse Width
- Gate Voltage
- Gate Clock
- Scan Frequency

---

## FPGA Signal Verification

检查：

- Timing Generator
- Gate Enable
- Driver Input Signal

---

## Hardware Inspection

检查：

- Driver IC
- FPC
- Connector
- PCB Trace

---

# 9. Root Cause Analysis

建议分析流程：

```text
Horizontal Artifact

↓

Single Row ?

├── YES

│      ↓

│   Gate Pulse Present ?

│      ↓

│   NO

│      ↓

│   Gate Driver Failure

│
└── YES

       ↓

Pulse Normal ?

       ↓

NO

↓

Timing Error

↓

YES

↓

Check TFT

↓

Check Readout ASIC
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Driver IC Damage | 驱动芯片损坏 |
| Power Supply Abnormal | Gate 电源异常 |
| Clock Failure | 时钟异常 |
| FPGA Timing Error | FPGA 输出错误 |
| FPC Damage | 排线损坏 |
| PCB Trace Open | PCB 线路断裂 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单行异常 |
| Moderate | 多行异常 |
| Major | 大面积扫描异常 |
| Critical | 无法完成图像采集 |

---

# 12. Engineering Recommendations

建议：

- 定期检查 Gate Pulse 波形质量。
- 使用示波器验证 Gate Voltage、Pulse Width 和 Scan Frequency。
- 若出现固定位置水平异常，应优先排查 Gate Driver，再检查 TFT。
- 检查 Driver IC 供电及 FPGA Timing 输出。
- 排除 FPC、Connector 和 PCB Trace 的机械连接问题。

---

# 13. Relationship with Other Modules

## TFTFailure

Gate Driver 控制 TFT 导通。

Gate Driver 故障通常导致整行 TFT 无法工作。

---

## ReadoutASICFailure

Gate Driver 控制"何时读"。

Readout ASIC 控制"如何读"。

两者可能产生类似图像异常，应结合时序和波形进行区分。

---

## AcquisitionWorkflow

Gate Driver 是 Acquisition Workflow 行扫描控制核心。

---

## ReadoutWorkflow

Gate Driver 完成扫描后，Readout ASIC 才能完成数据采集。

---

## DecisionTree

Gate Driver Failure 是以下诊断的重要节点：

- Horizontal Line
- Horizontal Band
- Missing Rows
- Scan Failure
- Timing Error

---

# 14. Knowledge Graph

```text
FPGA

↓

Timing Generator

↓

Gate Driver

├── No Output
├── Missing Pulse
├── Low Voltage
├── High Voltage
├── Timing Error
├── Clock Failure
├── Driver IC Failure
└── FPC Failure

↓

Gate Line

↓

TFT Array

↓

Readout ASIC

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

Gate Driver Failure 是 Flat Panel Detector 行扫描系统的关键故障，其主要表现为 Gate Pulse 丢失、电压异常、扫描时序错误、时钟故障及驱动芯片异常等。由于 Gate Driver 控制整行 TFT 的导通，因此故障通常表现为固定位置的水平黑线、水平亮带、多行异常或整幅图像扫描异常。分析过程中应结合 Gate Pulse 波形、FPGA Timing、TFT 状态及 Readout ASIC 工作情况进行综合判断，准确定位故障根因，并为 DecisionTree 和现场维修提供可靠依据。