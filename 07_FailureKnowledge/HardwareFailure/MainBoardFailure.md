# MainBoardFailure

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
- MemoryFailure.md
- PowerFailure.md
- ../../03_Hardware/MainBoard.md
- ../../06_Workflow/PowerOnWorkflow.md
- ../../06_Workflow/CommunicationWorkflow.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Main Board Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Main Board（主控制板）的典型故障模式、形成机理、图像表现、检测方法及根因分析。

Main Board 是 Detector 的核心硬件平台，负责连接 FPGA、Memory、Power、Communication Interface、Sensor 等关键模块，并完成供电管理、数据交换、通信控制及系统协调。

由于 Main Board 位于整个系统的中心，其故障通常表现为多个模块同时异常，而不仅仅是单一图像问题。

本文件回答的问题：

> **Main Board 为什么会发生故障？故障后会导致哪些系统及图像异常？**

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于 Detector 主控制板及其相关硬件故障分析。

---

# 3. Main Board Overview

Main Board 是 Detector 的核心控制平台。

主要职责：

- System Interconnection
- Power Distribution
- FPGA Hosting
- Memory Interface
- Communication Interface
- Peripheral Control
- Sensor Management
- Status Monitoring

系统结构：

```text
Power

↓

Main Board

├── FPGA
├── Memory
├── ADC
├── Communication
├── Battery (Wireless)
├── Sensors
└── Host Interface
```

Main Board 为整个 Detector 提供统一的硬件平台。

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| PCB Damage | PCB 损坏 |
| Power Distribution Failure | 电源分配异常 |
| Bus Failure | 总线故障 |
| Connector Failure | 接插件异常 |
| Interface Failure | 接口故障 |
| Clock Distribution Failure | 时钟分配异常 |
| Signal Integrity Failure | 信号完整性异常 |
| Component Failure | 板载器件故障 |
| Thermal Failure | 温度异常 |
| Mechanical Damage | 机械损坏 |

---

# 5. Failure Mechanisms

## 5.1 PCB Damage

PCB 线路断裂、短路或分层。

影响：

- 模块无法通信
- 信号中断

典型表现：

- Detector 无法启动
- 图像采集中断

---

## 5.2 Power Distribution Failure

主板供电异常。

影响：

- 多模块同时掉电
- 电压不稳定

典型表现：

- Detector 重启
- 图像中断
- 通信失败

---

## 5.3 Bus Failure

高速总线异常。

包括：

- DDR Bus
- SPI
- I²C
- PCIe（部分系统）

影响：

- 数据交换失败

典型表现：

- 图像错误
- 初始化失败

---

## 5.4 Connector Failure

连接器接触不良。

影响：

- 间歇性故障

典型表现：

- 偶发断连
- 图像随机异常

---

## 5.5 Interface Failure

外部接口损坏。

包括：

- Ethernet
- USB
- Optical Fiber
- Wireless Module Interface

影响：

- 图像无法传输

---

## 5.6 Clock Distribution Failure

主时钟无法正常分配。

影响：

- FPGA
- ADC
- Communication

全部异常。

---

## 5.7 Signal Integrity Failure

高速信号质量下降。

原因：

- 阻抗失配
- EMI
- PCB Layout

表现：

- 随机错误
- CRC Error
- 图像异常

---

## 5.8 Thermal Failure

主板局部过热。

影响：

- FPGA
- Memory
- Power Module

表现：

- 长时间运行异常
- 自动重启

---

## 5.9 Mechanical Damage

跌落、冲击、运输损伤。

表现：

- PCB 裂纹
- Connector 松动
- 焊点开裂

---

# 6. Typical Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| Detector Cannot Start | PCB / Power Failure |
| Initialization Failure | Bus Failure |
| Communication Failure | Interface Failure |
| Image Transmission Failure | Connector Failure |
| Random System Reset | Power Distribution Failure |
| Multiple Module Failure | Main Board Failure |
| Intermittent Fault | Connector / PCB Damage |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| FPGA | 无法工作 |
| Memory | 数据异常 |
| Communication | 图像无法发送 |
| Power | 多模块掉电 |
| System | Detector 停止工作 |

---

# 8. Detection Methods

## Visual Inspection

检查：

- PCB
- 焊点
- Connector
- 元器件

---

## Power Measurement

检查：

- 主板供电
- DC/DC 输出
- 电压纹波

---

## Bus Verification

检查：

- SPI
- I²C
- DDR
- Ethernet

---

## Communication Test

验证：

- USB
- Ethernet
- Wireless

---

## Thermal Inspection

检查：

- 热成像
- FPGA 温度
- Power Module 温度

---

# 9. Root Cause Analysis

```text
Detector Failure

↓

Power Normal？

↓

NO

↓

Power Distribution Failure

↓

YES

↓

Initialization Success？

↓

NO

↓

Main Board Bus Failure

↓

YES

↓

Communication Normal？

↓

NO

↓

Interface Failure

↓

YES

↓

Check FPGA / Memory
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| PCB Crack | PCB 裂纹 |
| Connector Damage | 接插件损坏 |
| DC/DC Failure | 电源模块故障 |
| Clock Distribution Failure | 时钟分配异常 |
| Water Damage | 液体侵入 |
| ESD Damage | 静电损伤 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单接口异常 |
| Moderate | 单模块异常 |
| Major | 多模块异常 |
| Critical | Detector 无法工作 |

---

# 12. Engineering Recommendations

建议：

- 定期检查 PCB 与连接器状态。
- 验证各路供电及纹波指标。
- 检查高速总线通信质量。
- 使用热成像检查异常发热区域。
- 排除 FPGA、Memory、Power 模块独立故障后，再确认 Main Board 故障。

---

# 13. Relationship with Other Modules

## MemoryFailure

Main Board 提供 Memory 所需的总线与供电。

---

## PowerFailure

Power Module 为 Main Board 提供稳定电源。

---

## CommunicationWorkflow

Main Board 负责通信接口管理。

---

## DecisionTree

Main Board Failure 是以下诊断的重要节点：

- Detector Cannot Start
- Multiple Module Failure
- Communication Failure
- Random Reset
- Initialization Failure

---

# 14. Knowledge Graph

```text
Power

↓

Main Board

├── PCB Failure
├── Bus Failure
├── Connector Failure
├── Interface Failure
├── Clock Failure
├── Signal Integrity Failure
├── Thermal Failure
└── Mechanical Damage

↓

FPGA

↓

Memory

↓

Communication

↓

Image

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

Main Board Failure 是 Flat Panel Detector 系统级硬件故障的重要组成部分，其主要表现为 PCB 损坏、电源分配异常、总线故障、接口故障、连接器异常及信号完整性下降等。由于 Main Board 是连接 FPGA、Memory、Power 和 Communication 的核心平台，因此故障通常影响多个模块，并可能导致 Detector 无法启动、通信失败、图像传输异常或系统重启。故障分析应结合供电、总线、接口、温度及系统日志进行综合判断，为 DecisionTree 和现场维修提供可靠依据。