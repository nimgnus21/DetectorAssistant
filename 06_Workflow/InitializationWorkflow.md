# InitializationWorkflow

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
- DetectorLifecycle.md
- PowerOnWorkflow.md
- CommunicationWorkflow.md
- ../03_Hardware/FPGA.md
- ../03_Hardware/Readout_ASIC.md
- ../03_Hardware/Main_Board.md
- ../03_Hardware/Battery.md
- ../04_Software/README.md
- ../05_Calibration/CalibrationTheory/CalibrationFlow.md
- README.md

---

# 1. Purpose

Initialization Workflow 定义数字平板探测器（Flat Panel Detector，FPD）完成上电后，对硬件、固件及系统资源进行初始化的标准流程。

本流程确保 Detector 在进入通信阶段前，各硬件模块已正确配置、系统参数已加载、基础资源已建立，并具备进入 Ready 状态的运行条件。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Portable Detector
- Fixed Detector

适用于：

- Cold Boot
- Warm Boot
- Software Reset
- Factory Test
- Service Maintenance

---

# 3. Workflow Objectives

Initialization Workflow 的主要目标包括：

- 启动 MCU 及 Firmware
- 配置 FPGA
- 初始化 Readout ASIC
- 初始化 Memory
- 检测关键硬件状态
- 加载系统参数
- 加载 Calibration 数据
- 建立系统运行环境
- 为 Communication Workflow 做准备

---

# 4. Workflow Overview

```text
PowerOn Complete

↓

MCU Boot

↓

Firmware Startup

↓

FPGA Configuration

↓

ASIC Initialization

↓

Memory Initialization

↓

Peripheral Detection

↓

Sensor Detection

↓

Temperature Check

↓

Battery Check

↓

Load System Configuration

↓

Load Calibration Data

↓

Hardware Self-Test

↓

Initialization Complete

↓

Communication Workflow
```

---

# 5. Workflow Inputs

Initialization Workflow 输入包括：

- Stable Power Rails
- Hardware Ready
- Power Good Signal
- Firmware Image
- FPGA Bitstream
- Configuration File
- Calibration File

所有输入均来自 PowerOn Workflow。

---

# 6. MCU Boot

MCU 开始执行启动程序。

主要任务：

- Bootloader 启动
- Firmware 校验
- Firmware 加载
- System Clock 配置
- Interrupt 初始化
- Watchdog 配置

输出：

MCU Running

---

# 7. FPGA Configuration

FPGA 完成逻辑配置。

主要内容：

- Bitstream Loading
- Logic Configuration
- Internal Reset
- Clock Configuration
- Interface Enable

配置完成后进入正常工作状态。

输出：

FPGA Ready

---

# 8. Readout ASIC Initialization

初始化 Readout ASIC。

包括：

- Register Reset
- Default Parameter Loading
- Bias Configuration
- Clock Configuration
- Gain Configuration（默认值）
- Offset Configuration（默认值）
- Interface Test

输出：

ASIC Ready

---

# 9. Memory Initialization

初始化系统存储资源。

包括：

- DDR Initialization（如适用）
- SRAM Test
- Flash Detection
- EEPROM Detection
- Buffer Allocation

输出：

Memory Ready

---

# 10. Peripheral Detection

检测外围硬件。

包括：

- Battery Management
- Temperature Sensor
- Power Board
- Communication Module
- LED
- Button
- Trigger Interface

确认所有外围设备状态正常。

输出：

Peripheral Ready

---

# 11. Detector Component Detection

检测 Detector 核心部件。

包括：

- TFT Array Status
- Readout Board Status
- FPGA Status
- ASIC Status
- Main Board Status

确认关键硬件能够正常工作。

输出：

Detector Hardware Verified

---

# 12. System Configuration

加载系统配置。

包括：

- Product Information
- Detector ID
- Serial Number
- Firmware Version
- Network Configuration
- Exposure Configuration
- Operating Mode

输出：

System Configuration Ready

---

# 13. Calibration Data Loading

加载校准相关数据。

包括：

- Offset Template
- Gain Template
- Defect Template
- Calibration Parameters
- Factory Calibration Data

若产品支持多个模板，则加载当前启用模板。

输出：

Calibration Ready

---

# 14. Hardware Self-Test

执行初始化自检。

检查内容：

- FPGA Running
- ASIC Communication
- Memory Test
- Battery Status
- Temperature Range
- Sensor Status
- Internal Communication
- Power Status

所有项目通过后进入下一阶段。

输出：

Initialization Passed

---

# 15. Workflow Outputs

Initialization Workflow 输出：

- FPGA Ready
- ASIC Ready
- Memory Ready
- Peripheral Ready
- Calibration Loaded
- System Configuration Loaded
- Detector Initialized

输出作为 Communication Workflow 的输入。

---

# 16. State Transition

```text
POWER ON

↓

MCU BOOT

↓

FIRMWARE START

↓

FPGA READY

↓

ASIC READY

↓

MEMORY READY

↓

CONFIGURATION LOADED

↓

SELF TEST

↓

INITIALIZATION COMPLETE

↓

COMMUNICATION
```

---

# 17. Timing Relationship

```text
PowerOnWorkflow

↓

InitializationWorkflow

├── MCU Boot
├── FPGA Configuration
├── ASIC Initialization
├── Memory Initialization
├── Peripheral Detection
├── Configuration Loading
├── Calibration Loading
└── Hardware Self-Test

↓

CommunicationWorkflow
```

---

# 18. Common Initialization Failure

| Failure | Description |
|----------|-------------|
| Firmware Load Failure | 固件加载失败 |
| FPGA Configuration Failure | FPGA 配置失败 |
| ASIC Initialization Failure | ASIC 初始化失败 |
| Memory Initialization Failure | 存储器初始化失败 |
| Peripheral Detection Failure | 外设检测失败 |
| Temperature Sensor Failure | 温度传感器异常 |
| Battery Detection Failure | 电池检测失败 |
| Calibration File Missing | 校准文件缺失 |
| Configuration File Error | 配置文件异常 |
| Self-Test Failed | 初始化自检失败 |

详细处理参见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge（规划中）

---

# 19. Engineering Notes

工程建议：

- FPGA 配置完成前禁止初始化 ASIC。
- ASIC 初始化完成前禁止建立图像采集流程。
- Calibration 数据必须在进入 Ready 状态前完成加载。
- 所有初始化失败均应记录日志及错误代码。
- Initialization 完成后建议再次验证关键硬件状态，确保系统稳定。

---

# 20. Relationship with Other Modules

## PowerOn Workflow

提供稳定供电及硬件运行环境。

---

## Hardware

完成 FPGA、ASIC、Memory 等硬件初始化。

---

## Software

负责 Firmware、Configuration 及参数加载。

---

## Calibration

提供校准模板及相关参数。

---

## Communication Workflow

Initialization 完成后进入 Communication Workflow，建立 Host 与 Detector 的连接。

---

# 21. Document Boundary

本文件负责：

- MCU 启动
- Firmware 加载
- FPGA 配置
- ASIC 初始化
- Memory 初始化
- 外设检测
- 系统配置加载
- Calibration 数据加载
- 初始化自检

本文件不负责：

- 网络连接建立
- SDK 通信
- 曝光控制
- 图像采集
- 图像处理
- 图像传输

上述内容由后续 Workflow 文档说明。

---

# 22. Knowledge Graph

```text
PowerOn Complete

↓

MCU Boot

↓

Firmware Startup

↓

FPGA Configuration

↓

ASIC Initialization

↓

Memory Initialization

↓

Peripheral Detection

↓

Detector Component Detection

↓

System Configuration

↓

Calibration Data Loading

↓

Hardware Self-Test

↓

Initialization Complete

↓

Communication Workflow
```

---

# 23. Summary

Initialization Workflow 是 Detector 生命周期中的关键阶段，其主要任务是在完成供电后建立完整的软件和硬件运行环境。通过 MCU 启动、FPGA 配置、ASIC 初始化、系统配置加载、Calibration 数据加载及硬件自检，确保 Detector 具备稳定、可靠的工作状态，并为后续 Communication Workflow 建立 Host 连接及进入 Ready 状态提供基础。