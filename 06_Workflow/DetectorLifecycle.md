# DetectorLifecycle

Version: V2.0

Module: Workflow

Status: Released

Source Level:
- Engineering
- System

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- ../01_Product/ProductOverview.md
- ../02_System/SignalFlow.md
- ../02_System/ImagePipeline.md
- ../03_Hardware/README.md
- ../04_Software/README.md
- ../05_Calibration/CalibrationTheory/CalibrationFlow.md
- README.md

---

# 1. Purpose

Detector Lifecycle 定义数字平板探测器（Flat Panel Detector，FPD）从上电、初始化、曝光、图像采集、图像处理、数据传输到关机的完整生命周期。

本文件用于建立整个 Detector 的工程运行流程，是 Workflow 模块的总体框架，也是后续各 Workflow 文档的统一入口。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Static Detector
- Portable Detector

适用于 Detector 的整个运行周期。

---

# 3. Lifecycle Overview

Detector 生命周期如下：

```text
Power Off

↓

Power On

↓

Hardware Initialization

↓

Software Initialization

↓

Communication Establishment

↓

Detector Ready

↓

Exposure Preparation

↓

X-ray Exposure

↓

Charge Integration

↓

Signal Readout

↓

ADC Conversion

↓

Raw Image Generation

↓

Calibration

↓

Image Processing

↓

Image Transmission

↓

Image Display / Storage

↓

Idle

↓

Shutdown
```

Detector 在整个生命周期中不断在不同运行状态之间切换。

---

# 4. Lifecycle Stages

整个生命周期划分为十二个主要阶段。

## Stage 1 — Power On

完成 Detector 上电。

主要任务：

- 电源建立
- 电压稳定
- Power Board 工作
- FPGA 上电
- ASIC 上电
- MCU 启动

输出：

Detector Hardware Ready

---

## Stage 2 — Initialization

完成系统初始化。

包括：

- FPGA Configuration
- ASIC Configuration
- Memory Initialization
- Sensor Detection
- Battery Detection
- Temperature Detection

输出：

Detector Initialization Complete

---

## Stage 3 — Communication

建立与 Host 的通信。

包括：

- Ethernet
- WiFi（如支持）
- SDK Connection
- iDetector Connection

输出：

Communication Ready

---

## Stage 4 — Detector Ready

Detector 进入待曝光状态。

主要完成：

- Parameter Download
- Calibration Template Load
- Exposure Configuration
- Ready Signal

输出：

Ready for Exposure

---

## Stage 5 — Exposure

接收 X-ray。

过程：

```text
X-ray

↓

Scintillator

↓

Photodiode

↓

Charge Accumulation
```

输出：

Pixel Charge

---

## Stage 6 — Readout

开始读取 Pixel Charge。

包括：

- Gate Driver Scan
- TFT Switching
- Charge Readout
- Readout ASIC

输出：

Analog Signal

---

## Stage 7 — ADC

模拟信号数字化。

包括：

- CDS
- Amplifier
- ADC

输出：

Digital Pixel Data

---

## Stage 8 — Raw Image Generation

生成原始图像。

输出：

Raw Image

Raw Image 未经过任何校正。

---

## Stage 9 — Calibration

执行：

- Offset Correction
- Gain Correction
- Defect Correction

输出：

Corrected Image

---

## Stage 10 — Image Processing

完成图像处理。

包括：

- Window / Level
- LUT
- Noise Reduction
- Edge Enhancement
- Image Orientation

输出：

Processed Image

---

## Stage 11 — Image Transmission

完成图像传输。

包括：

- Host Transfer
- Network Transfer
- PACS（如支持）

输出：

Host Image

---

## Stage 12 — Shutdown

Detector 正常退出。

包括：

- Stop Exposure
- Save Configuration
- Close Communication
- Power Off

生命周期结束。

---

# 5. State Transition

Detector 状态转换如下：

```text
OFF

↓

BOOTING

↓

INITIALIZING

↓

CONNECTING

↓

READY

↓

EXPOSING

↓

READOUT

↓

PROCESSING

↓

TRANSMITTING

↓

IDLE

↓

SHUTDOWN
```

每个状态均对应特定的软件和硬件行为。

---

# 6. Relationship with Other Modules

## Product

定义产品功能及应用场景。

---

## System

定义信号流及系统架构。

---

## Hardware

完成信号采集与硬件控制。

---

## Software

完成设备控制、参数配置及通信。

---

## Calibration

完成图像校正。

---

## Image Processing

完成图像增强与显示优化。

---

# 7. Subsequent Workflow Documents

本文件作为 Workflow 总纲，后续各流程文档将进一步展开：

- PowerOnWorkflow.md
- InitializationWorkflow.md
- CommunicationWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- CalibrationWorkflow.md
- ImageProcessingWorkflow.md
- ImageTransmissionWorkflow.md
- ShutdownWorkflow.md

---

# 8. Knowledge Graph

```text
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

Readout

↓

ADC

↓

Raw Image

↓

Calibration

↓

Image Processing

↓

Transmission

↓

Shutdown
```

---

# 9. Document Boundary

本文件负责：

- Detector 生命周期定义
- Workflow 总体流程
- 状态转换
- 各阶段关系
- Workflow 导航

本文件不负责：

- 硬件原理
- 软件实现
- Calibration 算法
- 图像处理算法
- 故障分析

上述内容分别由对应模块说明。

---

# 10. Summary

Detector Lifecycle 描述了数字平板探测器从上电到关机的完整运行过程，是 Workflow 模块的核心总纲。它建立了系统运行阶段、状态转换及各模块之间的关系，为 Hardware、Software、Calibration、Image Processing、Failure Knowledge、Decision Tree 及 SOP 提供统一的流程基础和导航框架。