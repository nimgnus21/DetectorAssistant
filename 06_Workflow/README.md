# Workflow

Version: V2.0

Module: Detector Workflow

Status: Released

---

# 1. Purpose

Workflow 模块定义数字平板探测器（Flat Panel Detector，FPD）在整个工作生命周期中的标准运行流程。

本模块以工程运行过程为主线，系统描述 Detector 从上电、初始化、建立通信、曝光、信号采集、图像生成、图像传输直至关机的完整流程，并建立各阶段之间的逻辑关系，为系统设计、软件开发、硬件调试、售后维护、故障分析及标准作业流程（SOP）提供统一的流程框架。

Workflow 不关注某个模块的内部实现，而关注各模块之间的协同关系及运行顺序。

---

# 2. Module Position

Workflow 位于整个 Detector 知识体系的工程运行层。

```text
Product

↓

System

↓

Hardware

↓

Software

↓

Calibration

↓

Workflow

↓

Failure Knowledge

↓

Image Diagnosis

↓

Decision Tree

↓

SOP
```

其中：

- Product 定义产品能力。
- System 定义系统架构。
- Hardware 提供硬件基础。
- Software 控制设备运行。
- Calibration 提供校准能力。
- Workflow 将上述模块串联为完整工程流程。

---

# 3. Module Objectives

Workflow 模块主要实现以下目标：

- 建立 Detector 全生命周期模型。
- 规范各功能模块的执行顺序。
- 明确各阶段输入与输出。
- 定义模块之间的数据流及控制流。
- 为故障定位建立标准排查路径。
- 为 SOP 提供流程依据。
- 为 Decision Tree 提供流程基础。

---

# 4. Knowledge Architecture

```text
06_Workflow

├── README.md
├── DetectorLifecycle.md
├── PowerOnWorkflow.md
├── InitializationWorkflow.md
├── CommunicationWorkflow.md
├── ExposureWorkflow.md
├── AcquisitionWorkflow.md
├── ReadoutWorkflow.md
├── CalibrationWorkflow.md
├── ImageProcessingWorkflow.md
├── ImageTransmissionWorkflow.md
├── ShutdownWorkflow.md
└── WorkflowTroubleshooting.md
```

---

# 5. Workflow Hierarchy

Workflow 采用三级流程结构。

```text
Detector Lifecycle
        │
        ├── System Workflow
        │
        ├── Operation Workflow
        │
        └── Maintenance Workflow
```

其中：

**Detector Lifecycle**

定义 Detector 全生命周期。

**System Workflow**

描述 Detector 正常工作流程。

**Operation Workflow**

描述单次曝光及图像生成流程。

**Maintenance Workflow**

描述维护、升级、恢复及异常处理流程。

---

# 6. Detector Lifecycle

Detector 生命周期如下：

```text
Power Off

↓

Power On

↓

Initialization

↓

Communication

↓

Detector Ready

↓

Exposure

↓

Signal Acquisition

↓

Readout

↓

Raw Image

↓

Calibration

↓

Image Processing

↓

Image Transmission

↓

Idle

↓

Shutdown
```

所有 Workflow 均围绕上述生命周期展开。

---

# 7. Workflow Categories

Workflow 分为四类。

## Startup Workflow

包括：

- Power On
- Hardware Initialization
- Software Initialization
- Detector Ready

主要目标：

完成 Detector 启动。

---

## Acquisition Workflow

包括：

- Exposure
- Signal Acquisition
- Readout
- ADC
- Raw Image

主要目标：

完成图像采集。

---

## Image Workflow

包括：

- Calibration
- Image Processing
- Image Transmission

主要目标：

生成最终图像。

---

## Shutdown Workflow

包括：

- Save Configuration
- Close Communication
- Power Off

主要目标：

安全退出系统。

---

# 8. Relationship with Other Modules

## Product

提供：

- Product Configuration
- Detector Features
- Product Capability

---

## System

提供：

- Signal Flow
- Communication
- Image Pipeline
- Power Architecture

Workflow 根据 System Architecture 建立执行流程。

---

## Hardware

负责：

- Signal Generation
- Signal Readout
- Hardware Control

Workflow 定义 Hardware 的运行顺序。

---

## Software

负责：

- Device Control
- Parameter Configuration
- Firmware
- SDK
- Communication

Workflow 定义 Software 的执行时序。

---

## Calibration

负责：

- Offset Correction
- Gain Correction
- Defect Correction

Workflow 定义 Calibration 的执行位置。

---

## Failure Knowledge

Workflow 为故障分析提供标准流程。

---

## Image Diagnosis

Workflow 提供图像异常发生位置。

---

## Decision Tree

Workflow 为 Decision Tree 提供流程节点。

---

## SOP

Workflow 为标准操作流程提供执行依据。

---

# 9. Learning Path

建议按照以下顺序学习。

```text
DetectorLifecycle

↓

PowerOnWorkflow

↓

InitializationWorkflow

↓

CommunicationWorkflow

↓

ExposureWorkflow

↓

AcquisitionWorkflow

↓

ReadoutWorkflow

↓

CalibrationWorkflow

↓

ImageProcessingWorkflow

↓

ImageTransmissionWorkflow

↓

ShutdownWorkflow

↓

WorkflowTroubleshooting
```

建议严格按照生命周期顺序学习。

---

# 10. Workflow Dependency

各 Workflow 之间存在严格依赖关系。

```text
Power On

↓

Initialization

↓

Communication

↓

Ready

↓

Exposure

↓

Acquisition

↓

Readout

↓

Calibration

↓

Image Processing

↓

Transmission

↓

Shutdown
```

任何阶段异常均可能导致后续流程无法继续执行。

---

# 11. Failure Scope

Workflow 涉及以下典型异常：

- Startup Failure
- Initialization Failure
- Communication Failure
- Exposure Failure
- Acquisition Failure
- Readout Failure
- Calibration Failure
- Image Processing Failure
- Transmission Failure
- Shutdown Failure

所有异常最终汇总至：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge

---

# 12. Document Index

| Document | Purpose |
|----------|---------|
| DetectorLifecycle.md | 定义 Detector 全生命周期及状态转换 |
| PowerOnWorkflow.md | 定义设备上电流程 |
| InitializationWorkflow.md | 定义硬件及软件初始化流程 |
| CommunicationWorkflow.md | 定义设备通信建立流程 |
| ExposureWorkflow.md | 定义曝光控制流程 |
| AcquisitionWorkflow.md | 定义信号采集流程 |
| ReadoutWorkflow.md | 定义电荷读出及数据采集流程 |
| CalibrationWorkflow.md | 定义 Calibration 执行流程 |
| ImageProcessingWorkflow.md | 定义图像处理流程 |
| ImageTransmissionWorkflow.md | 定义图像传输流程 |
| ShutdownWorkflow.md | 定义设备关机流程 |
| WorkflowTroubleshooting.md | 定义 Workflow 故障排查流程 |
| README.md | Workflow 模块导航及学习指南 |

---

# 13. Module Boundary

本模块负责：

- Detector 生命周期
- 系统运行流程
- 模块执行顺序
- 数据流与控制流
- Workflow 标准化
- 流程依赖关系

本模块不负责：

- 硬件设计原理
- 软件实现细节
- Calibration 算法
- 图像处理算法
- 故障原因分析
- 临床图像诊断

上述内容分别由对应模块负责。

---

# 14. Knowledge Graph

```text
Product

↓

System

↓

Hardware

↓

Software

↓

Calibration

↓

Detector Lifecycle

├── Startup
├── Acquisition
├── Processing
├── Transmission
└── Shutdown

↓

Failure Knowledge

↓

Image Diagnosis

↓

Decision Tree

↓

SOP
```

---

# 15. Summary

Workflow 模块是 DetectorAssistant 工程知识体系中的流程中枢，负责建立数字平板探测器从启动、曝光、信号采集、图像校正、图像处理到关机的完整运行流程，并明确各模块之间的协作关系及执行顺序。

通过统一的 Workflow 框架，可以将 Product、System、Hardware、Software 及 Calibration 等模块整合为可执行的工程流程，为故障分析、决策树构建、SOP 编制及现场技术支持提供统一的流程基础，是连接基础知识与工程应用的重要桥梁。