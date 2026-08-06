# PowerOnWorkflow

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
- InitializationWorkflow.md
- ../02_System/PowerArchitecture.md
- ../02_System/Communication.md
- ../03_Hardware/Power_Board.md
- ../03_Hardware/Battery.md
- ../03_Hardware/FPGA.md
- ../03_Hardware/Readout_ASIC.md
- ../04_Software/README.md
- README.md

---

# 1. Purpose

Power On Workflow 定义数字平板探测器（Flat Panel Detector，FPD）从接收到上电请求开始，到硬件完成供电并进入初始化阶段的标准工作流程。

本文件用于说明 Detector 上电阶段的执行顺序、关键控制节点、输入输出及异常处理，为 Hardware、Software、Failure Knowledge 及 SOP 提供统一参考。

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Portable Detector
- Fixed Detector

适用于：

- 冷启动（Cold Boot）
- 热重启（Warm Boot）
- 软件重启（Software Reset）
- 维修后的首次启动

---

# 3. Workflow Objectives

Power On Workflow 的主要目标包括：

- 建立稳定电源系统
- 完成供电时序控制
- 启动核心硬件
- 检查基础硬件状态
- 为 Initialization Workflow 提供运行环境

Power On 阶段仅负责建立运行环境，不负责设备配置及功能初始化。

---

# 4. Workflow Overview

Power On 的标准流程如下：

```text
Power On Request

↓

Power Source Detection

↓

Power Management Enable

↓

Power Rail Sequence

↓

Core Hardware Power On

↓

Voltage Stabilization

↓

Basic Hardware Check

↓

Hardware Ready

↓

Initialization Workflow
```

Power On 完成后，系统进入 Initialization Workflow。

---

# 5. Workflow Inputs

Power On Workflow 的输入包括：

- 用户按下 Power Button
- Host Power Command
- External Trigger（如支持）
- Battery Wake-up
- AC Adapter Connected

输入信号经过 Power Management Unit（PMU）处理后启动上电流程。

---

# 6. Power Source Detection

系统首先确认供电来源。

可能包括：

- Internal Battery
- External DC Adapter
- Medical Power Supply（如适用）

主要检查内容：

- 电源是否存在
- 电压是否满足启动条件
- 极性是否正确
- 电源状态是否稳定

若检测失败，则停止启动流程。

输出：

Valid Power Source

---

# 7. Power Management

PMU（Power Management Unit）开始工作。

主要职责：

- Enable Power
- 控制 Power Sequence
- 管理各路电源输出
- 电源保护
- 电流监测
- 电压监测

PMU 保证各供电轨按照规定时序启动。

---

# 8. Power Rail Sequence

系统按照预定顺序开启各电源轨。

典型流程：

```text
Main Input

↓

3.3 V

↓

1.8 V

↓

1.2 V

↓

Analog Power

↓

Digital Power

↓

Peripheral Power
```

不同产品的具体电压及顺序可能有所不同，但必须遵循硬件设计要求。

输出：

Stable Power Rails

---

# 9. Core Hardware Power-On

完成核心硬件供电。

包括：

- FPGA
- Readout ASIC
- MCU
- DDR（如适用）
- Flash Memory
- Communication Module
- Battery Management Module（无线产品）

各器件仅完成上电，不进行功能配置。

输出：

Core Hardware Powered

---

# 10. Voltage Stabilization

所有供电轨建立后，系统进行稳定性检查。

检查项目包括：

- Voltage Within Range
- Power Good（PG）信号
- 电压纹波
- 电流异常
- 电源短路
- 欠压 / 过压

全部满足要求后进入下一阶段。

输出：

Stable Power Environment

---

# 11. Basic Hardware Check

Power On 阶段进行基础硬件自检。

主要检查：

- FPGA Power Status
- ASIC Power Status
- MCU Running
- Battery Status（无线产品）
- Temperature Sensor
- Power Board Status

此阶段仅确认硬件能够正常运行，不进行详细初始化。

输出：

Hardware Ready

---

# 12. Workflow Outputs

Power On Workflow 输出：

- Stable Power
- Hardware Ready
- Valid Power Status
- Power Sequence Complete

上述输出作为 Initialization Workflow 的输入。

---

# 13. State Transition

Power On 期间状态变化如下：

```text
OFF

↓

POWER REQUEST

↓

POWER DETECT

↓

POWER ENABLE

↓

POWER STABLE

↓

HARDWARE READY

↓

INITIALIZING
```

状态转换成功后进入 Initialization Workflow。

---

# 14. Common Startup Failure

Power On 阶段可能出现以下异常：

| Failure | Description |
|----------|-------------|
| No Power Input | 未检测到输入电源 |
| Battery Low | 电池电量不足 |
| Power Sequence Error | 电源时序异常 |
| Voltage Out of Range | 电压异常 |
| Power Good Timeout | PG 信号超时 |
| FPGA Power Failure | FPGA 未正常上电 |
| ASIC Power Failure | ASIC 未正常上电 |
| MCU Boot Failure | MCU 未启动 |
| Over Current Protection | 过流保护触发 |
| Over Voltage Protection | 过压保护触发 |

详细分析见：

- WorkflowTroubleshooting.md
- 07_FailureKnowledge/PowerFailure.md（规划中）

---

# 15. Engineering Notes

工程实施建议：

- 严格遵循硬件设计规定的 Power Sequence。
- 禁止在电压未稳定时启动 FPGA 或 ASIC。
- 无线产品需优先确认电池状态。
- Power Good 信号应作为进入下一阶段的重要条件。
- 所有电源异常应记录日志，便于后续故障分析。

---

# 16. Relationship with Other Modules

## System

提供：

- Power Architecture
- Communication Architecture

---

## Hardware

执行：

- Power Board
- Battery
- FPGA
- Readout ASIC

---

## Software

负责：

- Power Command
- Power Status Monitoring
- Boot Control

---

## Initialization Workflow

Power On Workflow 完成后立即进入 Initialization Workflow。

---

# 17. Document Boundary

本文件负责：

- 上电触发
- 电源检测
- PMU 控制
- Power Sequence
- 核心硬件供电
- 电压稳定检查
- 基础硬件自检

本文件不负责：

- FPGA 配置
- ASIC 配置
- 网络建立
- 参数下载
- Calibration 数据加载
- 图像采集

上述内容由后续 Workflow 文档说明。

---

# 18. Knowledge Graph

```text
Power Request

↓

Power Source Detection

↓

PMU Enable

↓

Power Rail Sequence

↓

Core Hardware Power On

↓

Voltage Stabilization

↓

Basic Hardware Check

↓

Hardware Ready

↓

Initialization Workflow
```

---

# 19. Summary

Power On Workflow 是 Detector 生命周期的起点，其核心任务是建立稳定可靠的供电环境，并按照预定时序启动核心硬件，为后续 Initialization Workflow 提供运行基础。

通过标准化的 Power Source Detection、Power Management、Power Rail Sequence、Voltage Verification 及 Basic Hardware Check，可以确保 Detector 在进入初始化阶段之前具备稳定、可靠的硬件运行条件，为整个系统生命周期奠定基础。