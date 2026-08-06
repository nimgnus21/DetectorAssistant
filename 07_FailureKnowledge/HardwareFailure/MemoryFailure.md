# MemoryFailure

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
- FPGAFailure.md
- MainBoardFailure.md
- ../../03_Hardware/Memory.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Memory Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Memory（DDR、SDRAM、Flash、EEPROM 等存储器）的典型故障模式、形成机理、图像表现、检测方法及根因分析。

Memory 是 Detector 数字系统的数据缓存与配置存储中心，用于缓存 FPGA 采集的图像数据、保存运行参数及固件配置。当 Memory 工作异常时，可能导致图像损坏、数据丢失、系统异常甚至 Detector 无法正常启动。

本文件回答的问题：

> **Memory 为什么会发生故障？故障后会导致哪些图像及系统异常？**

---

# 2. Scope

适用于：

- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于 Detector 内部所有存储器件，包括：

- DDR
- SDRAM
- SRAM
- Flash
- EEPROM

---

# 3. Memory Overview

Memory 的主要职责：

- Image Buffer
- Frame Cache
- Temporary Storage
- Firmware Storage
- Configuration Storage
- Calibration Data Storage

系统位置：

```text
ADC

↓

FPGA

↓

DDR / SDRAM

↓

Image Processing

↓

Communication

↓

Host PC
```

部分 Detector 同时包含：

```text
Flash

↓

FPGA Configuration

↓

Detector Startup
```

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| Memory Initialization Failure | 初始化失败 |
| Read Failure | 读失败 |
| Write Failure | 写失败 |
| Address Error | 地址异常 |
| Data Corruption | 数据损坏 |
| Bit Error | 位错误 |
| ECC Error | ECC 校验错误 |
| Refresh Failure | DDR Refresh 异常 |
| Flash Corruption | Flash 数据损坏 |
| Thermal Failure | 温度异常 |

---

# 5. Failure Mechanisms

## 5.1 Initialization Failure

Memory 无法初始化。

影响：

- FPGA 无法建立 Buffer
- Detector 启动失败

典型表现：

- Detector 无法 Ready

---

## 5.2 Read Failure

Memory 数据无法读取。

影响：

- 图像数据缺失

典型表现：

- 图像残缺
- 图像读取失败

---

## 5.3 Write Failure

数据无法写入 Memory。

影响：

- 图像缓存失败

典型表现：

- 图像丢失
- 连续曝光失败

---

## 5.4 Address Error

地址译码异常。

影响：

- 数据写入错误位置

典型表现：

- 图像错位
- 图像重复
- 数据覆盖

---

## 5.5 Data Corruption

存储内容损坏。

影响：

- Image Buffer 错误
- Calibration 数据异常

典型表现：

- 图像随机异常
- Calibration 失效

---

## 5.6 Bit Error

Memory 单 Bit 或多 Bit 错误。

影响：

- Gray Value 错误

典型表现：

- 随机噪声
- 图像局部异常

---

## 5.7 ECC Error

ECC 检测到 Memory 错误。

影响：

- 自动纠错
- 超过能力时数据损坏

典型表现：

- 系统日志 ECC Error
- 图像间歇异常

---

## 5.8 Refresh Failure

DDR Refresh 异常。

影响：

- 数据逐渐丢失

典型表现：

- 长时间运行后图像异常
- 图像随机变化

---

## 5.9 Flash Corruption

Flash 配置损坏。

影响：

- Firmware 无法加载

典型表现：

- Detector 无法启动
- FPGA Configuration Failure

---

# 6. Typical Image Symptoms

| Image Symptom | Possible Cause |
|---------------|----------------|
| Image Missing | Write Failure |
| Image Corruption | Data Corruption |
| Image Repeat | Address Error |
| Random Noise | Bit Error |
| Image Freeze | Read Failure |
| Calibration Loss | Flash Corruption |
| Startup Failure | Initialization Failure |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| FPGA | Buffer 建立失败 |
| Image Generation | 图像处理异常 |
| Communication | 图像发送失败 |
| Calibration | 参数丢失 |
| System | Detector 启动失败 |

---

# 8. Detection Methods

推荐检测方法：

## Memory Self-Test

检查：

- Read Test
- Write Test
- Pattern Test

---

## ECC Log

检查：

- ECC Error Count
- Correctable Error
- Uncorrectable Error

---

## Image Analysis

观察：

- 图像重复
- 图像缺失
- 图像随机异常

---

## Firmware Log

检查：

- Memory Initialization
- Memory Allocation
- Buffer Status

---

## Temperature Test

观察：

- 长时间运行稳定性
- 高温下 Memory Error

---

# 9. Root Cause Analysis

```text
Image Corruption

↓

Buffer Normal？

↓

NO

↓

Memory Read/Write Test

↓

Pass？

├── NO

│      ↓

│   Confirm Memory Failure

└── YES

       ↓

Check FPGA

↓

Check Communication
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| DDR Failure | DDR 芯片损坏 |
| Flash Corruption | Flash 数据损坏 |
| ECC Error | ECC 校验失败 |
| Overheating | 温度过高 |
| Address Bus Failure | 地址总线异常 |
| Power Instability | 电源波动 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 偶发数据错误 |
| Moderate | 图像异常 |
| Major | Buffer 无法工作 |
| Critical | Detector 无法启动 |

---

# 12. Engineering Recommendations

建议：

- 定期执行 Memory Self-Test。
- 监控 ECC Error 数量变化。
- 检查 DDR 电源及时钟稳定性。
- 定期备份 Flash 配置及 Calibration 数据。
- 排除 FPGA、Main Board 及电源问题后，再确认 Memory 故障。

---

# 13. Relationship with Other Modules

## FPGAFailure

FPGA 控制 Memory 的读写。

Memory 故障可能表现为 FPGA 数据异常。

---

## MainBoardFailure

Main Board 提供 Memory 所需电源及总线连接。

---

## ImageGenerationWorkflow

Memory 是图像缓存的重要组成部分。

---

## DecisionTree

Memory Failure 是以下诊断的重要节点：

- Image Corruption
- Image Repeat
- Image Freeze
- Calibration Loss
- Startup Failure

---

# 14. Knowledge Graph

```text
FPGA

↓

Memory

├── Initialization Failure
├── Read Failure
├── Write Failure
├── Address Error
├── Data Corruption
├── Bit Error
├── ECC Error
├── Refresh Failure
└── Flash Corruption

↓

Image Processing

↓

Communication

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

Memory Failure 是 Flat Panel Detector 数字数据链中的关键故障之一，其主要表现为初始化失败、读写异常、数据损坏、地址错误、ECC 校验失败及 Flash 配置损坏等。由于 Memory 承担图像缓存、参数存储及固件保存等关键任务，其故障通常导致图像损坏、数据丢失、Calibration 失效及 Detector 启动失败。故障分析应结合 Memory Self-Test、ECC 日志、Firmware 日志及 FPGA 状态进行综合判断，以准确定位根因，并为 DecisionTree 和现场维修提供可靠依据。