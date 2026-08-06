# ImageLoss

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
- ImageArtifact.md
- ImageDistortion.md
- ../HardwareFailure/FPGAFailure.md
- ../HardwareFailure/MemoryFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../SoftwareFailure/CommunicationFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Image Loss 描述数字平板探测器（Flat Panel Detector，FPD）图像丢失（Image Loss）及相关异常现象，包括图像未生成、图像丢失、图像冻结、图像截断、图像不更新及帧丢失等故障。

Image Loss 属于 Detector 使用过程中影响最大的故障之一，其根因通常涉及图像采集、缓存、重建、传输及接收等多个环节。

本文件回答的问题：

> **为什么 Detector 没有图像？为什么图像停止更新或只显示部分内容？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- No Image
- Image Loss
- Frame Loss
- Image Freeze
- Partial Image
- Black Image
- White Image

---

# 3. What is Image Loss

Image Loss 指：

**Detector 在曝光后未能正确生成、缓存、传输或显示完整图像，导致图像缺失或异常。**

主要特点：

- 无图像
- 图像停止更新
- 图像部分缺失
- 图像只有一半
- 黑屏
- 白屏
- 连续曝光过程中丢帧

---

# 4. Classification

```text
Image Loss

├── No Image
├── Frame Loss
├── Image Freeze
├── Partial Image
├── Black Image
├── White Image
├── Continuous Frame Drop
└── Image Timeout
```

---

# 5. Image Characteristics

## 5.1 No Image

特点：

- 曝光后无任何图像返回

可能原因：

- Detector Offline
- Communication Failure
- FPGA Failure

---

## 5.2 Frame Loss

特点：

- 连续曝光时部分图像丢失

可能原因：

- Network Packet Loss
- DDR Buffer Overflow
- Communication Timeout

---

## 5.3 Image Freeze

特点：

- 图像停留在上一帧
- 曝光后无更新

可能原因：

- Firmware Deadlock
- FPGA State Error
- SDK Failure

---

## 5.4 Partial Image

特点：

- 图像只有一部分
- 下半部分或右半部分缺失

可能原因：

- Data Transmission Interrupted
- Readout Failure
- Memory Error

---

## 5.5 Black Image

特点：

- 图像全黑
- 灰度接近零

可能原因：

- Trigger Failure
- Exposure Failure
- Offset Error

---

## 5.6 White Image

特点：

- 图像全白
- 灰度饱和

可能原因：

- ADC Saturation
- Firmware Processing Error

---

## 5.7 Continuous Frame Drop

特点：

- 连续动态图像频繁掉帧

可能原因：

- Network Bandwidth Insufficient
- FPGA Throughput Limitation
- CPU Overload

---

## 5.8 Image Timeout

特点：

- 图像返回时间过长
- 软件提示 Timeout

可能原因：

- Communication Delay
- Detector Busy
- Driver Timeout

---

# 6. Typical Root Causes

| Symptom | Possible Root Cause |
|----------|---------------------|
| No Image | Communication Failure |
| Image Freeze | Firmware / FPGA |
| Partial Image | Memory / Readout |
| Black Image | Exposure Failure |
| White Image | ADC Saturation |
| Frame Loss | Network Packet Loss |
| Timeout | Communication Delay |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| FPGA | No Image |
| DDR Memory | Frame Loss |
| Communication Board | Image Timeout |
| Readout ASIC | Partial Image |
| Power Module | Random Image Loss |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Image Freeze |
| Driver | Timeout |
| SDK | Image Reception Failure |
| Communication Service | Packet Loss |

---

# 9. Relationship with Workflow

Image Loss 可能发生于以下流程：

```text
Exposure

↓

Readout

↓

Image Generation

↓

Memory Buffer

↓

Image Transmission

↓

Workstation Display
```

任何一个阶段异常均可能导致 Image Loss。

---

# 10. Diagnostic Workflow

```text
No Image

↓

Detector Online？

↓

NO

↓

Communication

↓

YES

↓

Exposure Successful？

↓

NO

↓

Trigger / Generator

↓

YES

↓

Image Generated？

↓

NO

↓

FPGA

↓

YES

↓

Image Complete？

↓

NO

↓

Memory / ASIC

↓

YES

↓

Transmission OK？

↓

NO

↓

Communication

↓

Display Problem？

↓

SDK / Driver
```

---

# 11. Detection Methods

## Exposure Verification

确认：

- 曝光是否正常完成
- Trigger 是否收到

---

## Communication Test

检查：

- Ping
- Packet Loss
- Network Speed
- USB Status

---

## Memory Test

检查：

- DDR Buffer
- Memory Usage
- Overflow Log

---

## Firmware Log

分析：

- Timeout
- Buffer Error
- State Machine Error

---

## Continuous Acquisition Test

连续曝光：

观察：

- 是否存在丢帧
- 是否出现冻结
- 是否规律性异常

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| No Image After Exposure | Communication Failure |
| Previous Image Remains | Firmware Freeze |
| Half Image | Readout Failure |
| Black Screen | Exposure Failure |
| White Screen | ADC Saturation |
| Missing Frames | Network Packet Loss |

---

# 13. Engineering Recommendations

建议：

- 首先确认 Detector 在线状态。
- 检查曝光是否正常完成。
- 验证 FPGA 是否完成图像生成。
- 检查 Memory Buffer 是否溢出。
- 检查网络传输及丢包情况。
- 使用 Firmware Log 与 DecisionTree 进一步定位。

---

# 14. Relationship with Other Modules

## CommunicationFailure

Image Loss 最常见的软件原因。

---

## FPGAFailure

负责图像生成失败。

---

## MemoryFailure

负责图像缓存异常。

---

## ImageTransmissionWorkflow

负责图像传输过程分析。

---

## DecisionTree

Image Loss 是现场故障诊断中最高优先级的分析入口之一。

---

# 15. Knowledge Graph

```text
Image Loss

├── No Image
├── Frame Loss
├── Image Freeze
├── Partial Image
├── Black Image
├── White Image
├── Timeout
└── Packet Loss

↓

Workflow Analysis

↓

Hardware Analysis

├── FPGA
├── Memory
├── ASIC
├── Communication
└── Power

↓

Software Analysis

├── Firmware
├── Driver
├── SDK
└── Network

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Image Loss 是 Flat Panel Detector 最严重的图像异常之一，主要表现为无图像、图像冻结、图像截断、黑屏、白屏及连续丢帧等。其根因通常涉及 FPGA 图像生成、DDR Memory 缓存、Readout ASIC 数据读出、通信链路、Firmware 状态机及 Driver/SDK 接收等多个模块。通过曝光验证、通信测试、缓存检查、日志分析及 Workflow 排查，可快速定位图像丢失的根因，并结合 HardwareFailure、SoftwareFailure 与 DecisionTree 建立标准化故障分析流程。