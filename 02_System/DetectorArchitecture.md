# Detector Architecture

Version: V2.0

Module: System

Source Level:
- Fact
- Theory
- Engineering

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- SignalFlow.md
- ImagePipeline.md
- TimingArchitecture.md
- Communication.md
- PowerArchitecture.md

---

# 1. Purpose

Detector Architecture 用于定义数字平板探测器的整体系统架构。

本文件仅描述系统组成、模块职责及模块之间的关系。

各模块的内部工作原理、算法、校准方法及故障分析不在本文件展开，统一引用对应知识模块。

本文件作为整个 Detector Assistant 知识库的系统入口。

---

# 2. Scope

适用于所有数字平板探测器产品，包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

适用于：

- 产品培训
- 售前支持
- 售后支持
- 故障分析
- SOP 建立
- AI Knowledge Base

---

# 3. Design Principle

Detector Assistant 采用分层知识架构。

System 层负责描述系统组成和模块关系。

Hardware 层负责描述硬件模块原理。

Software 层负责描述软件模块功能。

Calibration 层负责描述校准流程。

Workflow 层负责描述现场操作流程。

FailureKnowledge 层负责描述故障知识。

ImageDiagnosis 层负责描述图像异常。

DecisionTree 层负责建立诊断逻辑。

Case 层负责沉淀现场案例。

---

# 4. System Overview

数字平板探测器由多个相互协作的子系统组成。

整个系统可划分为：

- Hardware System
- Software System
- Communication System
- Calibration System
- Power System
- Workflow System

各子系统共同完成：

X-Ray Detection

↓

Signal Conversion

↓

Image Generation

↓

Image Transmission

↓

Image Display

---

# 5. Functional Architecture

Detector

```

Hardware

↓

SignalFlow

↓

ImagePipeline

↓

Communication

↓

SDK

↓

Workstation

```

Calibration 作用于 ImagePipeline。

TimingArchitecture 控制 SignalFlow。

PowerArchitecture 为所有硬件模块提供供电。

Workflow 定义整个系统的操作过程。

---

# 6. Hardware Architecture

Hardware System 包括以下模块：

- Scintillator
- TFT Array
- Gate Driver
- Readout ASIC
- ADC
- FPGA
- DDR
- WiFi
- Battery
- Power Board

各模块详细内容引用：

03_Hardware

---

# 7. Software Architecture

Software System 包括：

- Detector
- Acquire
- Calibrate
- SDK
- Home
- Log
- Upgrade
- Settings

详细内容引用：

04_Software

---

# 8. Signal Architecture

Signal Flow 定义探测器内部信号转换过程。

包括：

X-Ray

↓

Visible Light

↓

Electrical Charge

↓

Analog Signal

↓

Digital Signal

详细内容引用：

SignalFlow.md

---

# 9. Image Architecture

Image Pipeline 定义图像处理流程。

包括：

Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Corrected Image

详细内容引用：

ImagePipeline.md

---

# 10. Timing Architecture

Timing Architecture 定义系统各模块工作时序。

包括：

Idle

↓

Exposure

↓

Integration

↓

Readout

↓

Transfer

详细内容引用：

TimingArchitecture.md

---

# 11. Communication Architecture

Communication Architecture 定义探测器与工作站之间的数据传输。

包括：

Detector

↓

Gigabit Ethernet

↓

SDK

↓

iDetector

详细内容引用：

Communication.md

---

# 12. Power Architecture

Power Architecture 定义系统供电关系。

包括：

Battery

↓

Power Board

↓

Hardware Module

详细内容引用：

PowerArchitecture.md

---

# 13. Calibration Architecture

Calibration System 包括：

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Template Management

详细内容引用：

05_Calibration

---

# 14. Workflow Architecture

Workflow 定义产品生命周期中的操作流程。

包括：

Installation

↓

Connection

↓

Activation

↓

Calibration

↓

Acquisition

↓

Maintenance

详细内容引用：

06_Workflow

---

# 15. System Dependency

Detector Architecture

↓

SignalFlow

↓

TimingArchitecture

↓

ImagePipeline

↓

Calibration

↓

FailureKnowledge

↓

ImageDiagnosis

↓

DecisionTree

↓

Case

↓

SOP

---

# 16. Engineering Characteristics

本文件仅描述系统结构。

本文件不描述：

- 硬件电路原理
- 软件算法
- 校准算法
- 图像算法
- 故障分析
- 维修流程

上述内容统一引用对应知识模块。

---

# 17. Failure Mapping

System Module | Related Knowledge
---|---
Hardware | 03_Hardware
Software | 04_Software
Calibration | 05_Calibration
Workflow | 06_Workflow
Signal | SignalFlow.md
Timing | TimingArchitecture.md
Communication | Communication.md
Power | PowerArchitecture.md
Image | ImagePipeline.md

---

# 18. Knowledge Relationship

Detector Architecture 是整个知识库的系统入口。

所有系统文档均引用本文件。

本文件引用关系如下：

Detector Architecture

↓

SignalFlow

↓

TimingArchitecture

↓

ImagePipeline

↓

Hardware

↓

Software

↓

Calibration

↓

Workflow

↓

FailureKnowledge

↓

ImageDiagnosis

↓

DecisionTree

↓

Case

↓

SOP

---

# 19. Document Boundary

本文件负责：

✓ 系统组成

✓ 系统关系

✓ 模块职责

✓ 知识导航

本文件不负责：

✗ 模块内部原理

✗ 参数说明

✗ 校准步骤

✗ 软件操作

✗ 故障诊断

✗ 图像分析

✗ SOP

---

# 20. Reference

## Fact

- 产品用户手册（系统组成、软件组成、网络通信等）
- 产品规格说明书

## Theory

- 数字 X 射线探测器培训资料
- 内部培训 PPT

## Engineering

- 售前实施经验
- 售后维护经验
- 现场故障案例