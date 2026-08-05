# Timing Architecture

Version: V2.0

Module: System

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- DetectorArchitecture.md
- SignalDomain.md
- ImagePipeline.md
- ../03_Hardware/Gate_Driver/README.md
- ../03_Hardware/TFT_Array/README.md
- ../03_Hardware/Readout_ASIC/README.md
- ../03_Hardware/FPGA/README.md

---

# 1. Purpose

Timing Architecture 定义数字平板探测器各功能模块在一次采集周期内的工作时序。

本文件描述系统状态、状态切换、时序关系及模块协同关系，不描述硬件实现及控制算法。

---

# 2. Scope

适用于所有 TFT 数字平板探测器。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Core Concept

一次完整采集由多个连续状态组成。

```

Idle

↓

Ready

↓

Exposure

↓

Integration

↓

Readout

↓

Image Processing

↓

Transfer

↓

Complete

```

各状态按照固定顺序执行。

---

# 4. Timing State Definition

| State | Description |
|--------|-------------|
| Idle | 空闲状态 |
| Ready | 等待曝光 |
| Exposure | X-Ray 曝光 |
| Integration | 电荷积分 |
| Readout | 图像读出 |
| Image Processing | 图像处理 |
| Transfer | 图像发送 |
| Complete | 本次采集结束 |

---

# 5. Timing Flow

```

Power On

↓

Detector Initialization

↓

Idle

↓

Ready

↓

Trigger Received

↓

Exposure

↓

Integration

↓

Readout

↓

Image Processing

↓

Transfer

↓

Ready

```

---

# 6. State Description

## 6.1 Idle

系统完成初始化。

探测器等待进入工作状态。

Related Module

- FPGA
- Communication

---

## 6.2 Ready

探测器完成准备。

等待 Trigger。

Related Module

- FPGA
- Trigger Logic

---

## 6.3 Exposure

探测器接收 X-Ray。

开始信号采集。

Related Domain

- X-Ray Domain
- Optical Domain

Reference

SignalDomain.md

---

## 6.4 Integration

Photodiode 收集并存储电荷。

电荷持续积分。

Related Domain

- Charge Domain

Reference

SignalDomain.md

---

## 6.5 Readout

Gate Driver 控制 TFT 逐行读出。

Readout ASIC 完成模拟信号处理。

ADC 完成数字化。

Related Domain

- Charge Domain
- Analog Domain
- Digital Domain

Reference

SignalDomain.md

---

## 6.6 Image Processing

数字图像执行校正流程。

包括：

- Offset
- Gain
- Defect

Reference

ImagePipeline.md

---

## 6.7 Transfer

图像发送至工作站。

Communication Interface 输出图像数据。

Reference

Communication.md

---

## 6.8 Complete

一次采集结束。

探测器重新进入 Ready。

---

# 7. Module Relationship

| Module | Active State |
|----------|-------------|
| Scintillator | Exposure |
| Photodiode | Exposure、Integration |
| TFT Array | Readout |
| Gate Driver | Readout |
| Readout ASIC | Readout |
| ADC | Readout |
| FPGA | Readout、Transfer |
| Ethernet | Transfer |

---

# 8. Signal Relationship

| Timing State | Signal Domain |
|--------------|---------------|
| Exposure | X-Ray Domain |
| Exposure | Optical Domain |
| Integration | Charge Domain |
| Readout | Charge Domain |
| Readout | Analog Domain |
| Readout | Digital Domain |
| Transfer | Communication Domain |

Reference

SignalDomain.md

---

# 9. Image Relationship

Image Pipeline 开始于 Readout 完成之后。

Timing Architecture 定义图像处理开始时间。

Reference

ImagePipeline.md

---

# 10. Calibration Relationship

Calibration 不参与 Exposure。

Calibration 作用于数字图像。

Reference

../05_Calibration/

---

# 11. Engineering Characteristics

一次采集周期按照固定状态顺序执行。

状态之间不得跳转。

Readout 完成前不得开始图像处理。

Image Processing 完成前不得发送图像。

---

# 12. Failure Mapping

| Timing State | Possible Failure | Related Knowledge |
|---------------|-----------------|-------------------|
| Ready | Trigger Not Received | FailureKnowledge |
| Exposure | Exposure Timeout | FailureKnowledge |
| Integration | Charge Collection Failure | ImageDiagnosis |
| Readout | Readout Failure | FailureKnowledge |
| Image Processing | Calibration Failure | Calibration |
| Transfer | Network Transmission Failure | Communication |

---

# 13. Knowledge Relationship

```

DetectorArchitecture

↓

SignalDomain

↓

TimingArchitecture

↓

ImagePipeline

↓

Calibration

↓

FailureKnowledge

↓

DecisionTree

```

---

# 14. Document Boundary

本文件负责：

- 系统时序定义
- 状态转换
- 模块时序关系
- 信号域时序关系

本文件不负责：

- Trigger 电路
- Gate Driver 原理
- FPGA 程序
- 校准算法
- 网络协议
- 图像算法

---

# 15. Reference

## Fact

- Mammo1012C 用户手册：设备工作流程及系统运行说明。:contentReference[oaicite:0]{index=0}
- Mammo1012X 用户手册：设备运行状态及操作流程。:contentReference[oaicite:1]{index=1}

## Theory

- 数字 X 射线探测器培训资料：曝光、积分、逐行读出、图像生成流程。（依据已提供培训资料）