# FailureClassification

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
- FailureAnalysisMethod.md
- FailureCode.md
- ../03_Hardware/
- ../05_Calibration/
- ../06_Workflow/
- ../09_DecisionTree/

---

# 1. Purpose

Failure Classification 定义数字平板探测器（Flat Panel Detector，FPD）故障的统一分类标准。

通过建立统一的故障分类体系，使研发、测试、售后及现场工程师能够采用一致的术语描述故障，并为故障分析、决策树及维修流程提供统一入口。

本文件回答的问题是：

> **当前故障属于哪一类？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Clinical Installation
- Field Service
- Failure Analysis
- Technical Training

适用于 Detector 全生命周期中的所有故障。

---

# 3. Classification Principles

故障分类遵循以下原则：

- 按故障来源分类，而非按故障现象分类。
- 一种故障可对应多个图像现象。
- 一个图像现象可能由多个故障共同导致。
- 分类应与 Detector 系统架构保持一致。
- 分类结果应作为 Decision Tree 的输入。

---

# 4. Classification Architecture

```text
Detector Failure

├── Hardware Failure
├── Software Failure
├── Calibration Failure
├── Communication Failure
├── Image Failure
├── Environment Failure
├── Power Failure
└── System Failure
```

---

# 5. Hardware Failure

硬件故障指 Detector 内部电子器件或结构件异常所导致的故障。

主要包括：

| Category | Description |
|----------|-------------|
| Scintillator Failure | 闪烁体故障 |
| Photodiode Failure | 光电二极管故障 |
| TFT Failure | TFT 开关故障 |
| Gate Driver Failure | Gate Driver 故障 |
| Readout ASIC Failure | 读出 ASIC 故障 |
| FPGA Failure | FPGA 故障 |
| Main Board Failure | 主板故障 |
| Memory Failure | 存储器故障 |
| Interface Failure | 接口硬件故障 |

典型特点：

- 固定位置异常
- 重复出现
- 更换硬件可恢复

---

# 6. Software Failure

软件故障指 Firmware、驱动程序或应用软件导致的问题。

主要包括：

| Category | Description |
|----------|-------------|
| Firmware Failure | 固件异常 |
| Driver Failure | 驱动异常 |
| SDK Failure | SDK 异常 |
| Configuration Failure | 参数配置异常 |
| Upgrade Failure | 升级失败 |

典型特点：

- 可通过升级或配置恢复
- 不依赖硬件损坏

---

# 7. Calibration Failure

Calibration Failure 指校准数据或校准流程异常。

主要包括：

| Category | Description |
|----------|-------------|
| Offset Failure | Offset 校准失败 |
| Gain Failure | Gain 校准失败 |
| Defect Failure | Defect 校准失败 |
| Template Failure | Template 异常 |

典型特点：

- 图像整体异常
- 更换 Calibration Template 后可能恢复

---

# 8. Communication Failure

通信故障指 Detector 与外部设备之间的数据通信异常。

主要包括：

| Category | Description |
|----------|-------------|
| Ethernet Failure | 有线网络故障 |
| Wi-Fi Failure | 无线通信故障 |
| SDK Connection Failure | SDK 连接失败 |
| Image Transmission Failure | 图像发送失败 |
| Communication Timeout | 通信超时 |

典型特点：

- Detector 工作正常
- Host 无法接收数据

---

# 9. Image Failure

Image Failure 指最终图像质量异常。

主要包括：

| Category | Description |
|----------|-------------|
| Line Artifact | 行列伪影 |
| Dead Pixel | 坏点 |
| Bright Pixel | 亮点 |
| Dark Image | 图像偏暗 |
| Bright Image | 图像偏亮 |
| Noise | 噪声 |
| Ghost | 残影 |
| Lag | 图像滞后 |
| Uniformity Failure | 均匀性异常 |
| Image Distortion | 图像畸变 |

说明：

Image Failure 属于故障表现（Symptom），其根因可能来自 Hardware、Calibration、Communication 或 Software。

---

# 10. Environment Failure

环境因素导致 Detector 工作异常。

主要包括：

| Category | Description |
|----------|-------------|
| High Temperature | 高温 |
| Low Temperature | 低温 |
| High Humidity | 高湿 |
| Condensation | 冷凝 |
| EMI | 电磁干扰 |
| Mechanical Shock | 机械冲击 |
| Vibration | 振动 |

特点：

环境恢复后，故障可能消失。

---

# 11. Power Failure

供电系统故障。

主要包括：

| Category | Description |
|----------|-------------|
| Battery Failure | 电池故障 |
| DC Input Failure | 外部供电异常 |
| Power Management Failure | 电源管理异常 |
| Voltage Instability | 电压不稳定 |
| Over Current | 过流 |
| Over Temperature Protection | 过温保护 |

典型表现：

- 无法开机
- 自动关机
- 系统重启

---

# 12. System Failure

系统级故障指多个模块共同导致的问题。

主要包括：

| Category | Description |
|----------|-------------|
| Startup Failure | 启动失败 |
| Initialization Failure | 初始化失败 |
| Workflow Failure | 工作流程异常 |
| Resource Conflict | 系统资源冲突 |
| Synchronization Failure | 时序同步异常 |

特点：

通常涉及多个模块协同分析。

---

# 13. Cross-Module Failure

部分故障可能跨越多个模块。

例如：

| Symptom | Possible Categories |
|----------|--------------------|
| 图像全黑 | Power / Hardware / Calibration |
| 图像噪声 | Hardware / Environment / Calibration |
| 图像无法发送 | Communication / Software |
| Detector Offline | Communication / Power |
| 无法曝光 | Workflow / Software / Hardware |

因此：

> **图像现象不能直接作为故障分类依据。**

---

# 14. Failure Severity Level

建议按照影响程度划分：

| Level | Description |
|-------|-------------|
| Level 1 | Information（提示） |
| Level 2 | Minor（轻微异常） |
| Level 3 | Major（主要功能受影响） |
| Level 4 | Critical（系统不可工作） |

Severity 用于：

- Error Code
- Service Priority
- Decision Tree

---

# 15. Relationship with Other Modules

## Workflow

定义：

正常工作流程。

Failure Classification：

确定 Workflow 中发生的是哪一类故障。

---

## Failure Analysis Method

定义：

故障分析的方法。

Failure Classification：

提供分析入口。

---

## Decision Tree

Decision Tree 根据故障分类建立不同诊断路径。

例如：

```text
Image Noise

↓

Image Failure

↓

Decision Tree

↓

Hardware / Calibration 判断
```

---

## Service

Service 根据故障分类制定维修方案。

---

# 16. Knowledge Graph

```text
Detector Failure

├── Hardware
├── Software
├── Calibration
├── Communication
├── Image
├── Environment
├── Power
└── System

↓

Failure Analysis

↓

Decision Tree

↓

Service
```

---

# 17. Summary

Failure Classification 建立了 DetectorAssistant 的统一故障分类体系，将所有故障划分为 Hardware、Software、Calibration、Communication、Image、Environment、Power 和 System 八大类别。该分类标准作为整个故障知识库的基础，为故障分析、决策树构建及现场维修提供统一的术语和结构，实现故障识别、分析与处理的一致性。