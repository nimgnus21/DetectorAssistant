# ExposureFailure

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
- StartupFailure.md
- DetectorOffline.md
- CommunicationTimeout.md
- WorkflowFailure.md
- ../HardwareFailure/TFTFailure.md
- ../HardwareFailure/GateDriverFailure.md
- ../HardwareFailure/ADCFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../SoftwareFailure/DriverFailure.md
- ../CalibrationFailure/OffsetCalibrationFailure.md
- ../CalibrationFailure/GainCalibrationFailure.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Exposure Failure 描述数字平板探测器（Flat Panel Detector，FPD）在曝光（Exposure）过程中发生的各种异常，包括触发失败、曝光未开始、曝光完成但无图像、曝光中断、图像生成失败及曝光超时等故障。

Exposure 是 Detector 工作流程中最关键的阶段，涉及 X-ray Generator、Trigger、TFT Gate Driver、Photodiode、ADC、FPGA、Firmware、通信系统等多个模块协同工作，任何一个环节发生异常都可能导致曝光失败。

本文件回答的问题：

> **为什么按下曝光后没有图像？为什么曝光结束后软件一直等待？为什么曝光流程偶尔成功、偶尔失败？**

---

# 2. Scope

适用于：

- Factory Test
- Production Test
- Installation
- Acceptance Test
- Technical Support
- Field Service

适用于：

- Wired Detector
- Wireless Detector
- Static Exposure
- Dynamic Exposure

---

# 3. What is Exposure Failure

Exposure Failure 指：

**Detector 在曝光准备、曝光执行、图像采集、图像生成或图像传输过程中发生异常，导致完整曝光流程无法完成。**

主要表现：

- Exposure Not Triggered
- Exposure Timeout
- No Image
- Exposure Interrupted
- Image Generation Failed
- Exposure Aborted

---

# 4. Failure Classification

```text
Exposure Failure

├── Trigger Failure
├── Exposure Not Started
├── Exposure Interrupted
├── Image Acquisition Failure
├── Image Generation Failure
├── Image Transfer Failure
└── Exposure Timeout
```

---

# 5. Typical Symptoms

## 5.1 Trigger Failure

特点：

- 按下曝光后无反应
- Detector 未进入曝光状态

可能原因：

- Trigger Signal Failure
- Generator Interface Failure
- Firmware Trigger Error

---

## 5.2 Exposure Not Started

特点：

- 软件等待曝光
- Detector 无曝光状态

可能原因：

- Trigger Missing
- Communication Failure

---

## 5.3 Exposure Interrupted

特点：

- 曝光过程中终止
- 软件提示 Exposure Abort

可能原因：

- Power Instability
- Firmware Exception
- Generator Stop

---

## 5.4 Image Acquisition Failure

特点：

- 曝光正常
- 无 Raw Image

可能原因：

- TFT Failure
- Gate Driver Failure
- Photodiode Failure
- ADC Failure

---

## 5.5 Image Generation Failure

特点：

- Raw Data 存在
- 无最终图像

可能原因：

- FPGA Failure
- Firmware Processing Error
- Calibration Failure

---

## 5.6 Image Transfer Failure

特点：

- 图像生成成功
- 软件未收到图像

可能原因：

- Communication Timeout
- Network Failure
- Packet Loss

---

## 5.7 Exposure Timeout

特点：

- 软件一直等待
- 超时退出

可能原因：

- Firmware Busy
- Image Processing Timeout
- Communication Delay

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Trigger Failure | Generator / Trigger |
| No Exposure | Firmware |
| No Image | TFT / ADC |
| Exposure Abort | Power |
| Image Timeout | Communication |
| Image Generation Failure | FPGA |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Gate Driver | No Readout |
| TFT Array | No Charge Transfer |
| Photodiode | No Signal |
| ADC | No Digital Data |
| FPGA | Image Processing Failure |
| Communication Board | Image Cannot Upload |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Exposure Control Failure |
| Driver | Trigger Failure |
| SDK | Exposure Timeout |
| Application | Waiting for Image |

---

# 9. Relationship with Calibration

Exposure Failure 可能与以下校准异常有关：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Pixel Calibration Failure

Calibration 数据异常可能导致图像生成失败或图像质量异常。

---

# 10. Diagnostic Workflow

```text
Exposure Failed

↓

Trigger Received？

↓

NO

↓

Trigger Analysis

↓

YES

↓

Exposure Started？

↓

NO

↓

Firmware Analysis

↓

YES

↓

Raw Image Generated？

↓

NO

↓

Hardware Analysis

↓

YES

↓

Image Generated？

↓

NO

↓

FPGA / Calibration

↓

YES

↓

Image Transferred？

↓

NO

↓

Communication Analysis

↓

Exposure Success
```

---

# 11. Detection Methods

## Trigger Verification

检查：

- Trigger Signal
- Generator Interface
- Exposure Timing

---

## Firmware Log

检查：

- Exposure Start
- Exposure End
- Exception Log

---

## Raw Data Verification

确认：

- Raw Buffer
- ADC Output
- Readout Status

---

## Image Processing Verification

检查：

- FPGA Status
- Image Processing Queue
- Calibration Loading

---

## Image Transmission Verification

检查：

- Image Packet
- Network Traffic
- SDK Receive Status

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Press Exposure but No Response | Trigger Failure |
| Exposure Completed but No Image | Image Acquisition Failure |
| Raw Data Exists but No Image | FPGA Processing Failure |
| Exposure Randomly Stops | Firmware Exception |
| Large Images Timeout | Communication Delay |
| Exposure Only Fails After Calibration | Calibration Failure |

---

# 13. Engineering Recommendations

建议：

- 首先确认 Trigger 是否正常到达 Detector。
- 检查 Firmware 是否进入 Exposure 状态。
- 验证 TFT、ADC 是否正常输出 Raw Data。
- 检查 FPGA 图像处理状态。
- 检查图像传输链路及 SDK 日志。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## GateDriverFailure

Gate Driver 异常会直接导致无法完成图像读出。

---

## ADCFailure

ADC 故障导致 Raw Data 无法生成。

---

## CommunicationTimeout

图像传输失败最终表现为 Exposure Timeout。

---

## WorkflowFailure

Exposure Failure 是 Workflow Failure 的核心组成部分。

---

## DecisionTree

Exposure Failure 是图像采集故障分析的重要入口。

---

# 15. Knowledge Graph

```text
Exposure Failure

├── Trigger
├── Exposure Start
├── Image Acquisition
├── Image Processing
├── Image Transfer
└── Exposure Timeout

↓

Trigger Verification

↓

Firmware Verification

↓

Raw Data Verification

↓

FPGA Processing

↓

Communication Verification

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Exposure Failure 是 Flat Panel Detector 最关键的系统级故障之一，覆盖 Trigger、曝光控制、图像采集、图像处理及图像传输全过程。其根因可能涉及 Generator、Gate Driver、TFT、Photodiode、ADC、FPGA、Firmware、通信网络及 Calibration 等多个模块。通过 Trigger 验证、Raw Data 检查、FPGA 状态分析、通信验证及日志分析，可快速定位曝光失败的具体阶段，并结合 Hardware Failure、Software Failure、Calibration Failure 与 DecisionTree 建立完整的 Exposure Failure 故障分析体系。