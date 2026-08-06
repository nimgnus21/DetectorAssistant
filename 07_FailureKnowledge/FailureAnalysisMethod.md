# FailureAnalysisMethod

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
- FailureClassification.md
- FailureCode.md
- ../06_Workflow/
- ../03_Hardware/
- ../05_Calibration/
- ../09_DecisionTree/

---

# 1. Purpose

Failure Analysis Method 定义数字平板探测器（Flat Panel Detector，FPD）的标准故障分析方法。

本文档建立统一的故障分析流程，使研发、测试、售后及现场工程师能够采用一致的方法定位故障、验证原因并形成分析结论。

本文件回答的问题是：

> **如何科学地分析一个故障？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Product Verification
- Field Service
- Failure Analysis
- Technical Support

适用于所有 Hardware、Software、Calibration、Communication 及 Image Failure。

---

# 3. Analysis Principles

所有故障分析应遵循以下原则。

## 3.1 Evidence First

所有分析必须基于实际证据。

包括：

- Image
- Log
- Error Code
- Measurement
- Test Result

禁止仅依据经验直接判断根因。

---

## 3.2 Symptom ≠ Root Cause

图像表现只是故障现象。

例如：

```text
Image Noise

≠

ASIC Failure
```

噪声可能来自：

- Power
- TFT
- Readout ASIC
- Calibration
- EMI

因此必须进一步分析。

---

## 3.3 Single Variable Principle

每次仅修改一个变量。

例如：

错误：

```text
更换 ASIC

+

升级 Firmware

+

重新 Calibration
```

无法判断真正恢复原因。

正确：

```text
修改一个变量

↓

验证结果

↓

继续下一步
```

---

## 3.4 Progressive Isolation

采用逐层缩小范围的方法。

```text
System

↓

Workflow

↓

Module

↓

Signal

↓

Component

↓

Root Cause
```

避免直接拆机或更换器件。

---

# 4. Standard Analysis Workflow

推荐采用统一分析流程：

```text
Failure Report

↓

Collect Symptoms

↓

Failure Classification

↓

Workflow Location

↓

Module Location

↓

Signal Analysis

↓

Root Cause Verification

↓

Failure Conclusion
```

---

# 5. Failure Information Collection

故障分析前应收集完整信息。

包括：

## Detector Information

- Model
- Serial Number
- Firmware Version
- Hardware Version

---

## Environment

- Temperature
- Humidity
- Power Supply
- Network

---

## Exposure Information

- Trigger Mode
- Exposure Parameter
- Detector Status

---

## Image Information

- Raw Image
- Corrected Image
- Image Sample

---

## Log Information

- Detector Log
- SDK Log
- Error Code
- System Log

---

# 6. Workflow-Based Analysis

首先确定故障发生在哪一个 Workflow。

推荐顺序：

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

每个 Workflow 均应确认：

- 输入是否正常
- 执行是否完成
- 输出是否正确

---

# 7. Module-Based Analysis

确定故障所属模块。

```text
Detector

├── Hardware
├── Software
├── Calibration
├── Communication
├── Power
└── Environment
```

避免多个模块同时分析。

---

# 8. Signal Chain Analysis

按照信号流分析故障传播路径。

```text
X-ray

↓

Scintillator

↓

Photodiode

↓

TFT

↓

Gate Driver

↓

Data Line

↓

Readout ASIC

↓

ADC

↓

FPGA

↓

Calibration

↓

Image Generation

↓

Transmission
```

故障通常发生于信号首次异常的位置。

---

# 9. Root Cause Verification

定位疑似原因后必须验证。

推荐方法：

## Repeatability Test

重复执行测试。

确认故障稳定出现。

---

## Replacement Test

替换：

- Detector
- Board
- Cable
- Power Supply

观察故障是否消失。

---

## Comparison Test

对比：

- Good Unit
- Bad Unit

寻找差异。

---

## Isolation Test

逐步隔离：

- Hardware
- Software
- Communication
- Environment

缩小故障范围。

---

## Measurement Test

使用仪器测量：

- Voltage
- Clock
- Timing
- Signal Waveform

验证分析结果。

---

# 10. Failure Conclusion

分析完成后建议形成统一结论。

内容包括：

| Item | Description |
|------|-------------|
| Failure Name | 故障名称 |
| Symptom | 故障现象 |
| Classification | 故障分类 |
| Workflow | 所属 Workflow |
| Module | 所属模块 |
| Root Cause | 根本原因 |
| Verification | 验证方法 |
| Corrective Action | 处理建议 |

---

# 11. Common Analysis Mistakes

常见错误包括：

## 直接根据图像判断根因

例如：

```text
有横线

↓

一定是 Gate Driver
```

实际上可能是：

- Gate Driver
- Readout ASIC
- Calibration
- FPGA

---

## 忽略 Workflow

未确认故障阶段即开始维修。

---

## 同时修改多个条件

导致无法确认真正原因。

---

## 忽略日志

仅依据肉眼观察。

---

## 未进行验证

分析结束后未复现或验证。

---

# 12. Recommended Analysis Sequence

建议统一分析顺序：

```text
Collect Evidence

↓

Classify Failure

↓

Locate Workflow

↓

Locate Module

↓

Analyze Signal

↓

Verify Root Cause

↓

Document Result
```

---

# 13. Relationship with Other Modules

## Workflow

提供：

故障发生位置。

---

## Hardware

提供：

硬件结构及工作原理。

---

## Calibration

提供：

校准流程及模板信息。

---

## DecisionTree

根据 Failure Analysis 建立诊断路径。

---

## Service

根据分析结果制定维修方案。

---

# 14. Engineering Notes

工程建议：

- 优先使用客观数据进行分析。
- 每次分析仅验证一个假设。
- 保留原始 Image、Log 及 Error Code。
- 未完成根因验证前，不应修改多个系统参数。
- 所有分析结论应可复现、可验证。

---

# 15. Knowledge Graph

```text
Failure Report

↓

Evidence Collection

↓

Failure Classification

↓

Workflow Location

↓

Module Location

↓

Signal Analysis

↓

Root Cause Verification

↓

Failure Conclusion

↓

Decision Tree

↓

Service
```

---

# 16. Summary

Failure Analysis Method 定义了 DetectorAssistant 的统一故障分析方法，通过 **证据收集 → 故障分类 → Workflow 定位 → 模块定位 → 信号链分析 → 根因验证** 的标准流程，实现故障分析过程的规范化和可重复性。本文档作为所有故障文档的分析基础，为 DecisionTree、Service 及后续故障处理提供统一的方法论支撑。