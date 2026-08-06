# FPGAFailure

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
- ADCFailure.md
- MemoryFailure.md
- ../../03_Hardware/FPGA.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

FPGA Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 FPGA（Field Programmable Gate Array）的典型故障模式、形成机理、图像表现、检测方法及根因分析。

FPGA 是 Detector 的核心数字控制器，负责协调各硬件模块工作、控制图像采集时序、缓存数据、执行图像预处理并完成图像输出。

由于 FPGA 位于整个数字信号链的中心，其故障通常会影响多个 Workflow，而不仅仅表现为单一图像异常。

本文件回答的问题：

> **FPGA 为什么会发生故障？故障后会导致哪些系统及图像异常？**

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于所有 FPGA 相关故障分析。

---

# 3. FPGA Overview

FPGA 是 Detector 的数字控制中心。

主要职责：

- System Control
- Timing Generation
- Gate Driver Control
- ADC Data Acquisition
- Image Buffer Management
- Image Processing
- Communication Control
- Status Monitoring

系统位置：

```text
ADC

↓

FPGA

├── Timing Control
├── Data Buffer
├── Image Processing
├── Communication
└── System Control

↓

Memory

↓

Host PC
```

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| Configuration Failure | FPGA 配置失败 |
| Firmware Corruption | 固件损坏 |
| Timing Generator Failure | 时序发生器异常 |
| Data Buffer Failure | 数据缓存异常 |
| Logic Failure | 内部逻辑错误 |
| Clock Failure | 时钟异常 |
| Reset Failure | 复位异常 |
| Communication Interface Failure | 接口异常 |
| Resource Overflow | 资源占用异常 |
| Thermal Failure | 温度异常 |

---

# 5. Failure Mechanisms

## 5.1 Configuration Failure

FPGA 未正确加载配置文件。

表现：

- Detector 无法启动
- 初始化失败

---

## 5.2 Timing Generator Failure

FPGA 输出 Timing 错误。

影响：

- Gate Driver 工作异常
- Readout Timing 错误

表现：

- 图像错位
- 行列异常

---

## 5.3 Data Buffer Failure

缓存数据错误。

表现：

- 图像缺失
- 图像重复
- 图像撕裂

---

## 5.4 Logic Failure

内部状态机异常。

表现：

- Workflow 中断
- 图像随机异常
- 功能失效

---

## 5.5 Clock Failure

系统时钟异常。

表现：

- Detector 不稳定
- 图像随机噪声
- 通信异常

---

## 5.6 Reset Failure

FPGA 无法正确初始化。

表现：

- Detector 无法进入 Ready 状态
- Workflow 无法启动

---

## 5.7 Interface Failure

与 ADC、Memory 或 Communication Interface 的连接异常。

表现：

- 图像数据丢失
- 通信失败

---

## 5.8 Thermal Failure

FPGA 温度过高。

表现：

- 长时间运行后异常
- 自动重启
- 图像间歇性错误

---

# 6. Typical Image Symptoms

| Image Symptom | Possible Cause |
|---------------|----------------|
| Image Missing | Buffer Failure |
| Image Corruption | Logic Failure |
| Random Artifact | Clock Failure |
| Image Misalignment | Timing Failure |
| Repeated Image | Buffer Failure |
| Image Freeze | Logic Failure |
| Communication Timeout | Interface Failure |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| Acquisition | Timing 控制异常 |
| Readout | 数据采集异常 |
| Image Generation | 图像处理异常 |
| Communication | 图像发送异常 |
| System | Detector 无法正常运行 |

---

# 8. Detection Methods

## Detector Log

检查：

- FPGA Initialization
- FPGA Error
- Configuration Status

---

## Firmware Verification

检查：

- Firmware Version
- Bitstream
- Configuration File

---

## Timing Verification

检查：

- Gate Timing
- ADC Timing
- System Clock

---

## Communication Test

验证：

- Host Connection
- Image Transmission
- Interface Status

---

## Temperature Monitoring

检查：

- FPGA Temperature
- 散热状态
- 长时间运行稳定性

---

# 9. Root Cause Analysis

```text
Detector Failure

↓

Initialization Normal？

↓

NO

↓

FPGA Configuration

↓

YES

↓

Image Abnormal？

↓

Timing Normal？

↓

NO

↓

Timing Generator Failure

↓

YES

↓

Buffer Normal？

↓

NO

↓

FPGA Buffer Failure

↓

YES

↓

Check Memory
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Firmware Upgrade Failure | 固件升级异常 |
| FPGA Configuration Error | 配置错误 |
| Clock Instability | 时钟异常 |
| Overheating | 散热不足 |
| Logic Bug | FPGA Logic Bug |
| Power Instability | 电源波动 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 单一功能异常 |
| Moderate | 图像处理异常 |
| Major | Workflow 无法完成 |
| Critical | Detector 无法工作 |

---

# 12. Engineering Recommendations

建议：

- 定期验证 FPGA Firmware 与 Configuration。
- 检查系统时钟及 PLL 状态。
- 监控 FPGA 温度及散热性能。
- 验证数据缓存与 Memory 通信。
- 在确认 FPGA 故障前，应排除 ADC、Memory、电源及通信接口问题。

---

# 13. Relationship with Other Modules

## ADCFailure

ADC 提供数字数据。

FPGA 接收并处理数字数据。

---

## MemoryFailure

FPGA 将图像数据写入 Memory。

Memory 异常可能表现为 FPGA 数据错误。

---

## ReadoutWorkflow

FPGA 控制整个 Readout 流程。

---

## ImageGenerationWorkflow

FPGA 完成图像预处理及输出控制。

---

## DecisionTree

FPGA Failure 是以下诊断的重要节点：

- Initialization Failure
- Image Freeze
- Image Corruption
- Communication Timeout
- Workflow Failure

---

# 14. Knowledge Graph

```text
ADC

↓

FPGA

├── Configuration Failure
├── Timing Failure
├── Logic Failure
├── Buffer Failure
├── Clock Failure
├── Reset Failure
├── Interface Failure
└── Thermal Failure

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

FPGA Failure 是 Flat Panel Detector 数字控制系统的核心故障，其主要表现为配置失败、时序异常、逻辑错误、缓存异常、时钟故障及接口故障等。由于 FPGA 负责整个 Detector 的控制与图像数据处理，因此故障通常会影响多个 Workflow，并可能导致初始化失败、图像异常、通信失败或系统无法正常运行。故障分析应结合 Firmware、Timing、Buffer、Clock、Temperature 及系统日志进行综合判断，为 DecisionTree 和现场维修提供可靠依据。