# HardwareFailure

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
- ../README.md
- ../FailureClassification.md
- ../FailureAnalysisMethod.md
- ../FailureCode.md
- ../../03_Hardware/README.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Module Purpose

Hardware Failure 模块建立数字平板探测器（Flat Panel Detector，FPD）硬件故障知识体系。

本模块围绕 Detector 各硬件组件，分析故障产生机理、典型表现、影响范围、诊断依据及关联关系，为研发、测试、售后及现场工程师提供统一的硬件故障分析参考。

本模块回答的问题是：

> **某个硬件为什么会发生故障？故障后会造成什么影响？**

---

# 2. Module Scope

本模块覆盖 Detector 内部所有关键硬件组件，包括：

- Scintillator
- Photodiode
- TFT Array
- Gate Driver
- Readout ASIC
- ADC
- FPGA
- Memory
- Main Board
- Power Management

适用于：

- Hardware Design Verification
- Factory Test
- Engineering Debug
- Failure Analysis
- Field Service
- Technical Training

---

# 3. Module Objectives

Hardware Failure 的主要目标包括：

- 建立硬件故障分类体系
- 解释硬件失效机理
- 分析故障传播路径
- 总结典型图像表现
- 建立故障与 Workflow 的对应关系
- 为 Decision Tree 提供理论依据

---

# 4. Module Structure

```text
HardwareFailure/

README.md

ScintillatorFailure.md

PhotodiodeFailure.md

TFTFailure.md

GateDriverFailure.md

ReadoutASICFailure.md

ADCFailure.md

FPGAFailure.md

MemoryFailure.md

MainBoardFailure.md

PowerFailure.md
```

---

# 5. Hardware Failure Architecture

Detector 硬件故障可按照信号链进行组织：

```text
X-ray

↓

Scintillator

↓

Photodiode

↓

TFT Array

↓

Gate Driver

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Memory

↓

Main Board

↓

Image Output
```

故障通常会沿信号流逐级传播，因此分析时建议按照上述顺序定位。

---

# 6. Hardware Failure Classification

| Component | Failure Document |
|-----------|------------------|
| Scintillator | ScintillatorFailure.md |
| Photodiode | PhotodiodeFailure.md |
| TFT Array | TFTFailure.md |
| Gate Driver | GateDriverFailure.md |
| Readout ASIC | ReadoutASICFailure.md |
| ADC | ADCFailure.md |
| FPGA | FPGAFailure.md |
| Memory | MemoryFailure.md |
| Main Board | MainBoardFailure.md |
| Power Management | PowerFailure.md |

---

# 7. Standard Failure Analysis Model

所有硬件故障文档采用统一分析框架：

```text
Component

↓

Working Principle

↓

Failure Mode

↓

Failure Mechanism

↓

Image Symptoms

↓

Detection Method

↓

Root Cause

↓

Engineering Recommendations
```

保证所有文档具有一致的结构和分析深度。

---

# 8. Relationship with Hardware Module

**03_Hardware** 负责说明：

- 硬件结构
- 工作原理
- 信号流程
- 功能职责

**Hardware Failure** 负责说明：

- 如何失效
- 为什么失效
- 失效后的影响
- 如何识别失效

例如：

```text
03_Hardware

TFT

↓

07_FailureKnowledge

TFTFailure
```

两者形成"正常工作"与"故障分析"的对应关系。

---

# 9. Relationship with Workflow

硬件故障通常发生在特定 Workflow 中。

| Workflow | Related Hardware |
|----------|------------------|
| PowerOnWorkflow | Power Management、Main Board |
| InitializationWorkflow | FPGA、Memory |
| ExposureWorkflow | Gate Driver |
| AcquisitionWorkflow | TFT、Photodiode |
| ReadoutWorkflow | Readout ASIC、ADC、FPGA |
| CalibrationWorkflow | 受硬件状态影响 |
| ImageGenerationWorkflow | FPGA、Memory |
| ImageTransmissionWorkflow | Main Board、Communication Interface |

Workflow 用于确定故障发生阶段，Hardware Failure 用于解释故障原因。

---

# 10. Relationship with Image Failure

多数图像异常都源于硬件故障。

例如：

| Image Symptom | Possible Hardware Failure |
|--------------|---------------------------|
| Line Artifact | Gate Driver、TFT、Readout ASIC |
| Dead Pixel | TFT、Photodiode |
| Bright Pixel | TFT Leakage、Photodiode |
| Noise | Readout ASIC、ADC、Power |
| Uniformity | Scintillator、Gain Calibration |
| Image Distortion | FPGA、Memory |

Image Failure 描述图像现象，Hardware Failure 分析硬件根因。

---

# 11. Relationship with DecisionTree

DecisionTree 以 Hardware Failure 为理论基础。

例如：

```text
Image Noise

↓

ReadoutASICFailure

↓

DecisionTree

↓

ASIC Signal Verification

↓

Root Cause
```

---

# 12. Applicable Personnel

适用于：

| Role | Purpose |
|------|---------|
| Hardware Engineer | 硬件失效分析 |
| Firmware Engineer | 软硬件协同调试 |
| Test Engineer | 产品验证 |
| Service Engineer | 现场故障定位 |
| Technical Support | 客户问题分析 |
| Training Engineer | 技术培训 |

---

# 13. Design Principles

本模块遵循以下原则：

- 每篇文档仅分析一种硬件组件。
- 基于硬件工作原理解释故障机理。
- 不重复 Hardware 模块内容。
- 不描述维修步骤。
- 与 Workflow、Image Failure、DecisionTree 建立对应关系。
- 所有分析均基于信号链进行组织。

---

# 14. Recommended Reading Order

建议阅读顺序：

```text
03_Hardware

↓

HardwareFailure

↓

ImageFailure

↓

DecisionTree

↓

Service
```

首次学习建议按照 Detector 信号链阅读：

```text
Scintillator

↓

Photodiode

↓

TFT

↓

Gate Driver

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Memory

↓

Main Board

↓

Power
```

---

# 15. Knowledge Graph

```text
03_Hardware

↓

Component

↓

Working Principle

↓

Failure Mechanism

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree

↓

Service
```

---

# 16. Summary

Hardware Failure 是 DetectorAssistant 硬件故障知识体系的核心模块，系统分析 Detector 各硬件组件的失效模式、故障机理、图像表现及影响范围，并与 Workflow、Image Failure、DecisionTree 等模块建立对应关系，为硬件故障定位、根因分析及工程诊断提供统一的理论基础。