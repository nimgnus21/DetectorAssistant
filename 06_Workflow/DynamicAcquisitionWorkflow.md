# DynamicAcquisitionWorkflow

Version: V1.0

Module: Workflow

Status: Released

---

# 1. Purpose

Dynamic Acquisition Workflow 描述动态平板探测器（Dynamic Flat Panel Detector）在连续采集模式下的完整工作流程，包括采集初始化、触发响应、曝光控制、图像读出、连续帧采集及结束流程。

本文档适用于动态探测器（Fluoroscopy、DSA、CBCT 等）工作模式分析、SDK 开发、Firmware 开发、FPGA 调试、FAE 故障分析及现场问题排查。

---

# 2. Scope

适用于：

- Dynamic Detector
- Continuous Acquisition
- Pulsed Acquisition
- External Trigger
- Internal Trigger
- Swap Mode

---

# 3. Dynamic Acquisition Overview

动态采集区别于静态采集。

静态模式：

```text
Trigger

↓

Exposure

↓

Readout

↓

Image

↓

End
```

动态模式：

```text
Initialize

↓

Start Acquisition

↓

Wait Trigger

↓

Exposure

↓

Readout

↓

Generate Image

↓

Transfer Image

↓

Next Frame

↓

Stop Acquisition
```

整个采集过程中 Detector 始终保持采集状态，直到收到 Stop Command。

---

# 4. Acquisition Initialization

开始采集前系统完成以下初始化：

- Detector Online 检查
- Firmware Version 检查
- Mode 加载
- ROI 配置
- Frame Rate 配置
- Offset / Gain / Defect 模板加载
- Buffer 初始化
- FPGA 初始化
- SDK 建立采集队列

初始化完成后进入等待 Trigger 状态。

---

# 5. Trigger Response

Detector 接收到 Trigger 后：

```text
Trigger

↓

Frame Request

↓

Enable Detector

↓

Exposure

↓

Readout
```

Trigger 来源：

- External Trigger
- Internal Timer
- Continuous Trigger

要求：

Trigger Frequency 不得高于当前 Mode 最大 Frame Rate。

否则：

- Trigger Ignore
- Frame Drop
- Image Loss

---

# 6. Exposure Process

收到 Trigger 后：

Detector 打开积分窗口（Enable）。

```text
Enable

↓

X-Ray ON

↓

Charge Integration

↓

Enable OFF
```

要求：

X-Ray 必须位于 Enable Window 内。

否则：

- Exposure Failure
- Brightness Error
- Partial Exposure

---

# 7. Readout Process

曝光结束后：

Detector 开始逐行读出。

```text
Exposure End

↓

Gate Driver Scan

↓

Pixel Readout

↓

ADC

↓

FPGA

↓

Memory
```

Readout 时间受到以下因素影响：

- ROI
- Frame Rate
- Detector Resolution
- Binning
- FPGA Performance

---

# 8. Image Generation

完成 Readout 后：

SDK 完成：

1. Offset Correction
2. Gain Correction
3. Defect Correction
4. Image Processing
5. Output Image

动态图通常连续生成多帧。

---

# 9. Continuous Acquisition

动态模式下：

```text
Frame 1

↓

Frame 2

↓

Frame 3

↓

...

↓

Frame N
```

每完成一帧：

立即等待下一 Trigger。

直到：

```text
Stop Command
```

结束采集。

---

# 10. Stop Acquisition

停止采集：

```text
Stop Command

↓

Finish Current Readout

↓

Close Enable

↓

Stop Trigger

↓

Release Buffer

↓

Acquisition End
```

注意：

不要在 Readout 未完成时强制停止。

否则可能导致：

- Incomplete Image
- Timeout
- Buffer Error

---

# 11. Engineering Notes

## Trigger Frequency

Trigger 频率必须小于或等于当前 Mode 配置值。

否则：

- 无法响应 Trigger
- 图像丢失
- 帧率异常

---

## ROI

ROI 越小：

- Readout 更快
- Frame Rate 更高

ROI 要求：

- Minimum 256 × 256
- Width 为 8 的倍数
- Height 为 8 的倍数

---

## Binning

开启 Binning：

优点：

- Readout 更快
- Frame Rate 提高

缺点：

- Spatial Resolution 降低

---

## Image Loss

Image Loss 常见原因：

- 网络丢包
- Jumbo Frame 配置错误
- Frame Rate 设置过高
- ROI 设置不合理
- Trigger Frequency 超限

---

# 12. Common Failure

## Detector No Response

检查：

- Connection
- Trigger
- Firmware
- Mode

---

## Image Loss

检查：

- Network
- Jumbo Frame
- Driver
- Packet Size
- Frame Rate

---

## Timeout

检查：

- Trigger
- Detector Status
- SDK
- FPGA

---

## Calibration Failure

检查：

- Offset
- Gain
- Defect Template
- ROI
- PGA

---

# 13. Related Documents

- TimingWorkflow.md
- ModeWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- ImageGenerationWorkflow.md
- CalibrationWorkflow.md
- WorkflowTroubleshooting.md

---

# 14. Summary

Dynamic Acquisition Workflow 描述了动态探测器从初始化、等待 Trigger、曝光、读出、图像生成到连续采集结束的完整流程。理解该流程能够帮助开发人员、FAE 和售后工程师快速定位 Trigger、Exposure、Readout、Image Loss 及 Frame Drop 等动态采集相关问题，并为动态模式配置和故障分析提供理论基础。