# Power Architecture

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
- TimingArchitecture.md
- Communication.md
- ../03_Hardware/Battery/README.md
- ../03_Hardware/Power_Board/README.md
- ../03_Hardware/FPGA/README.md
- ../03_Hardware/Readout_ASIC/README.md
- ../03_Hardware/Gate_Driver/README.md

---

# 1. Purpose

Power Architecture 定义数字平板探测器供电系统的整体架构。

本文件描述电能来源、供电路径、供电对象及供电关系，建立系统级电源模型。

本文件不描述电源电路设计、电源管理算法及具体器件实现。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

适用于：

- 系统供电架构
- 电源模块关系
- 电源分配
- 产品培训
- 售前方案说明
- 售后故障定位

---

# 3. Core Concept

Power Architecture 为整个探测器提供稳定的电能。

系统电源负责：

- 提供输入电源
- 完成电源转换
- 分配不同工作电压
- 为各功能模块持续供电

Power Architecture 不参与：

- X-Ray 信号采集
- 图像处理
- 图像校准
- 图像传输

---

# 4. Power Architecture Overview

```text
External Power / Battery
          │
          ▼
Power Management
          │
          ▼
Power Board
          │
 ┌────────┼────────┐
 │        │        │
 ▼        ▼        ▼
Analog   Digital  Communication
Power    Power      Power
 │        │        │
 ▼        ▼        ▼
ASIC     FPGA     Ethernet
 │
 ▼
Gate Driver
 │
 ▼
TFT Array
```

---

# 5. Power Components

| Component | Function |
|-----------|----------|
| External Power | 外部供电输入 |
| Battery | 电池供电（适用型号） |
| Power Management | 电源管理 |
| Power Board | 电压转换与分配 |
| Analog Power | 模拟电路供电 |
| Digital Power | 数字电路供电 |
| Communication Power | 通信模块供电 |

---

# 6. Power Flow

```text
Power Source

↓

Power Management

↓

Power Board

↓

Voltage Distribution

↓

Hardware Modules

↓

Detector Operation
```

---

# 7. Power Distribution

| Power Consumer | Power Source |
|----------------|--------------|
| Gate Driver | Power Board |
| TFT Array | Gate Driver / Power Board |
| Readout ASIC | Analog Power |
| ADC | Analog Power |
| FPGA | Digital Power |
| DDR | Digital Power |
| Ethernet Controller | Communication Power |
| WiFi Module | Communication Power |
| Control MCU | Digital Power |

---

# 8. Power Domain

系统按照功能划分为多个供电域。

## Analog Power Domain

供电对象：

- Readout ASIC
- ADC
- Analog Front End

特点：

提供低噪声模拟电源。

---

## Digital Power Domain

供电对象：

- FPGA
- DDR
- MCU

特点：

提供数字逻辑工作电源。

---

## Communication Power Domain

供电对象：

- Ethernet Controller
- WiFi Module

特点：

支持数据通信。

---

## Control Power Domain

供电对象：

- Power Management
- Control Logic

特点：

负责系统控制。

---

# 9. Relationship With SignalDomain

Power Architecture 为 Signal Domain 各阶段提供工作电源。

Power 不参与信号转换。

Reference：

SignalDomain.md

---

# 10. Relationship With TimingArchitecture

系统进入不同 Timing State 时，各模块按照时序工作。

Power 系统持续提供稳定供电。

Reference：

TimingArchitecture.md

---

# 11. Relationship With ImagePipeline

Image Pipeline 建立于数字系统供电基础之上。

Power Architecture 不参与图像处理。

Reference：

ImagePipeline.md

---

# 12. Relationship With Communication

Communication 模块由 Communication Power Domain 提供电源。

Reference：

Communication.md

---

# 13. Engineering Characteristics

Power Architecture 负责：

- 电源输入
- 电压转换
- 电源分配
- 电源稳定性

Power Architecture 不负责：

- 图像采集
- 图像处理
- 图像校准
- 图像传输

不同功能模块可采用不同电压等级。

供电应满足稳定、连续、可靠的要求。

---

# 14. Failure Mapping

| Power Stage | Possible Failure | Related Knowledge |
|--------------|------------------|-------------------|
| External Power | Input Power Loss | FailureKnowledge |
| Battery | Low Battery | FailureKnowledge |
| Power Management | Startup Failure | FailureKnowledge |
| Power Board | Voltage Distribution Failure | FailureKnowledge |
| Analog Power | Analog Circuit Failure | Hardware |
| Digital Power | FPGA Startup Failure | Hardware |
| Communication Power | Communication Module Failure | Communication |

---

# 15. Knowledge Relationship

```text
DetectorArchitecture
        │
        ▼
PowerArchitecture
        │
        ├────────► Hardware
        │
        ├────────► TimingArchitecture
        │
        ├────────► SignalDomain
        │
        ├────────► Communication
        │
        ├────────► FailureKnowledge
        │
        └────────► DecisionTree
```

---

# 16. Document Boundary

本文件负责：

- 电源架构
- 电源路径
- 电源分配
- 电源域划分
- 系统供电关系

本文件不负责：

- 电源电路设计
- DC/DC 转换原理
- 电池管理算法
- 电源时序控制
- 电压参数配置
- 电源维修方法

---

# 17. Reference

## Fact

- 产品用户手册中关于电源连接、设备启动及供电要求。
- 产品规格说明书中关于供电方式及电源接口。

## Theory

- 数字平板探测器培训资料中关于系统供电架构及模块供电关系。

## Engineering

相关内容在以下模块展开：

- 03_Hardware/Battery
- 03_Hardware/Power_Board
- 03_Hardware/FPGA
- 03_Hardware/Readout_ASIC
- 07_FailureKnowledge/Power
- 09_DecisionTree/PowerFailure