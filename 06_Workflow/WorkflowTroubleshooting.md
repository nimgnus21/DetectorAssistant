# WorkflowTroubleshooting

Version: V2.0

Module: Workflow

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- DetectorLifecycle.md
- PowerOnWorkflow.md
- InitializationWorkflow.md
- ConnectionWorkflow.md
- ExposureWorkflow.md
- AcquisitionWorkflow.md
- ReadoutWorkflow.md
- CalibrationWorkflow.md
- ImageGenerationWorkflow.md
- ImageTransmissionWorkflow.md
- ShutdownWorkflow.md
- ../07_FailureKnowledge/
- ../09_DecisionTree/

---

# 1. Purpose

Workflow Troubleshooting 提供 Detector 在完整工作流程中的故障定位方法。

本文档按照 Workflow 的执行顺序组织排查流程，帮助工程人员快速确定故障发生阶段，并定位对应模块，为进一步进入 Failure Knowledge 或 Decision Tree 提供入口。

本文件关注 **"故障发生在哪一个 Workflow"**，不负责具体硬件维修或算法分析。

---

# 2. Scope

适用于：

- Factory Test
- Clinical Installation
- Field Service
- R&D Debug
- Technical Support

---

# 3. Troubleshooting Strategy

建议按照 Workflow 顺序逐步确认。

```text
Power On

↓

Initialization

↓

Connection

↓

Exposure

↓

Acquisition

↓

Readout

↓

Calibration

↓

Image Generation

↓

Image Transmission

↓

Shutdown
```

一旦某阶段异常，应停止继续排查后续 Workflow，优先解决当前阶段问题。

---

# 4. Workflow Fault Location

| Workflow | Typical Symptoms | Next Reference |
|-----------|------------------|----------------|
| PowerOn | 无法开机、无法上电 | PowerOnWorkflow |
| Initialization | 初始化失败、模块未就绪 | InitializationWorkflow |
| Connection | SDK 无法连接、设备离线 | ConnectionWorkflow |
| Exposure | 无法曝光、无法触发 | ExposureWorkflow |
| Acquisition | 无图像、采集失败 | AcquisitionWorkflow |
| Readout | 图像异常、数据错误 | ReadoutWorkflow |
| Calibration | 校正失败、Template 错误 | CalibrationWorkflow |
| Image Generation | 图像生成失败 | ImageGenerationWorkflow |
| Image Transmission | 图像无法发送 | ImageTransmissionWorkflow |
| Shutdown | 无法关机、异常断电 | ShutdownWorkflow |

---

# 5. Power On Troubleshooting

检查项目：

- 电源输入
- 电池状态（无线）
- Power LED
- Power Management
- 主板供电

常见现象：

- 无法开机
- 自动关机
- 电源异常

参考：

- PowerOnWorkflow.md

---

# 6. Initialization Troubleshooting

检查项目：

- FPGA Initialization
- ASIC Initialization
- Hardware Detection
- Firmware Loading
- Self Test

常见现象：

- Initialization Failed
- Hardware Not Ready
- Self Test Failed

参考：

- InitializationWorkflow.md

---

# 7. Connection Troubleshooting

检查项目：

- Ethernet/Wi-Fi
- IP Configuration
- SDK Session
- Heartbeat
- Detector Online

常见现象：

- Detector Not Found
- Connection Timeout
- SDK Connect Failed
- Offline

参考：

- ConnectionWorkflow.md

---

# 8. Exposure Troubleshooting

检查项目：

- Trigger Mode
- AED
- Exposure Command
- Detector Ready

常见现象：

- 无法曝光
- Trigger Timeout
- Exposure Interrupted

参考：

- ExposureWorkflow.md

---

# 9. Acquisition Troubleshooting

检查项目：

- Gate Driver
- TFT Scan
- Timing
- Pixel Charge

常见现象：

- 无图像
- 图像缺失
- 行扫描异常

参考：

- AcquisitionWorkflow.md

---

# 10. Readout Troubleshooting

检查项目：

- Readout ASIC
- ADC
- FPGA
- Data Interface

常见现象：

- 图像噪声
- 花屏
- 数据错误
- 图像缺行

参考：

- ReadoutWorkflow.md

---

# 11. Calibration Troubleshooting

检查项目：

- Offset Template
- Gain Template
- Defect Template
- Template Version

常见现象：

- Offset 异常
- Gain 异常
- Defect 校正失败

参考：

- 05_Calibration/
- CalibrationWorkflow.md

---

# 12. Image Generation Troubleshooting

检查项目：

- Image Assembly
- Metadata
- Frame Buffer
- Image Validation

常见现象：

- 图像生成失败
- Metadata 丢失
- Frame Error

参考：

- ImageGenerationWorkflow.md

---

# 13. Image Transmission Troubleshooting

检查项目：

- Network Connection
- SDK
- Image Queue
- Buffer
- Transmission Status

常见现象：

- 图像发送失败
- Transmission Timeout
- Host 未收到图像

参考：

- ImageTransmissionWorkflow.md

---

# 14. Shutdown Troubleshooting

检查项目：

- Running Task
- Image Queue
- Communication Status
- Hardware Shutdown

常见现象：

- 无法关机
- 强制断电
- Shutdown Timeout

参考：

- ShutdownWorkflow.md

---

# 15. Troubleshooting Flow

```text
发现故障

↓

确认发生阶段

↓

定位对应 Workflow

↓

检查输入条件

↓

检查关键模块

↓

确认输出状态

↓

恢复正常流程

↓

如仍异常

↓

进入 FailureKnowledge

↓

进入 DecisionTree
```

---

# 16. Escalation Path

建议按以下顺序升级分析：

```text
Workflow

↓

FailureKnowledge

↓

DecisionTree

↓

Hardware Module

↓

Firmware

↓

Software

↓

Engineering Support
```

---

# 17. Engineering Notes

工程建议：

- 严格按照 Workflow 顺序排查，不建议跨阶段分析。
- 每次仅确认一个 Workflow 是否正常。
- 保留 Detector Log、SDK Log、Error Code 及 Image Sample。
- 不建议在未完成 Initialization 时继续排查 Exposure。
- 进入 Decision Tree 前，应首先确定故障所属 Workflow。

---

# 18. Relationship with Other Modules

## Workflow

定义正常运行流程。

---

## FailureKnowledge

解释各类故障原理、成因及影响。

---

## DecisionTree

提供现场故障诊断路径和处理流程。

---

## Hardware

负责最终硬件故障定位。

---

## Software

负责 SDK、Firmware 及应用层问题分析。

---

# 19. Document Boundary

本文件负责：

- Workflow 故障定位
- Workflow 排查顺序
- Workflow 与其他模块的关系
- Workflow 故障入口

本文件不负责：

- 故障机理分析
- 电路维修
- 图像异常分类
- 校准算法分析
- 维修操作指导

上述内容分别由 **07_FailureKnowledge** 和 **09_DecisionTree** 负责。

---

# 20. Knowledge Graph

```text
Workflow Fault

↓

Identify Workflow Stage

↓

Locate Workflow

↓

Check Input

↓

Check Process

↓

Check Output

↓

Recovered

      │

      └─────────────► FailureKnowledge

                              │

                              ▼

                        DecisionTree

                              │

                              ▼

                      Root Cause Analysis
```

---

# 21. Summary

WorkflowTroubleshooting 是整个 Workflow 模块的统一故障入口。它按照 Detector 生命周期对故障进行阶段划分，帮助工程人员快速判断问题发生位置，并将故障分析逐步引导至 **FailureKnowledge** 和 **DecisionTree** 模块，实现从流程定位到根因分析的完整闭环。