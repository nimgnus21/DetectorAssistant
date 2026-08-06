# ModeWorkflow

Version: V1.0

Module: Workflow

Status: Released

---

# 1. Purpose

Mode Workflow 用于描述动态平板（Dynamic Flat Panel Detector）不同工作模式（Mode）的定义、组成、配置原则及工作流程。

Mode 决定了 Detector 的采集行为，包括：

- Trigger 响应方式
- Exposure Timing
- Readout Timing
- Frame Rate
- ROI
- PGA
- Offset / Gain / Defect 模板使用方式

Mode 是动态探测器软件、Firmware、SDK 和 FPGA 协同工作的核心配置单元。

---

# 2. Scope

适用于：

- Dynamic Detector
- Firmware
- FPGA
- SDK
- FAE
- Calibration

---

# 3. What is Mode

Mode 可以理解为 Detector 的一组工作参数集合。

每一个 Mode 定义了一种完整的采集方式。

通常包含：

- Frame Rate
- ROI
- Exposure Mode
- Trigger Mode
- Readout Mode
- PGA
- Binning
- Gain Template
- Defect Template

---

# 4. Mode Architecture

```text
Mode

├── Trigger Configuration
├── Exposure Configuration
├── ROI Configuration
├── Readout Configuration
├── Frame Rate
├── PGA
├── Offset
├── Gain
└── Defect
```

---

# 5. Typical Workflow

```text
Load Mode

↓

Initialize Parameters

↓

Wait Trigger

↓

Enable Detector

↓

Exposure

↓

Readout

↓

Image Generation

↓

Image Transfer

↓

Next Frame
```

---

# 6. Common Mode Parameters

| Parameter | Description |
|------------|-------------|
| Frame Rate | 图像采集帧率 |
| ROI | 图像区域 |
| Exposure Mode | 曝光方式 |
| Trigger Mode | 触发方式 |
| Readout Mode | 读出方式 |
| PGA | 放大倍数 |
| Binning | 合并采样 |
| Offset Template | Offset 校正模板 |
| Gain Template | Gain 校正模板 |
| Defect Template | 坏点模板 |

---

# 7. Typical Dynamic Modes

## Mode 128

特点：

- 清空采集（Clear Acquisition）
- 用于初始化或清空电荷
- 不作为正常动态图像输出

应用：

- Calibration
- Detector Initialization

---

## Mode 129

特点：

- 脉冲采集（Pulse Acquisition）
- 等待外部 Trigger
- 每次 Trigger 对应一帧图像

应用：

- DR
- Pulse Fluoroscopy

---

## Mode 131

特点：

- 清空采集模式
- 用于连续动态图像前的准备阶段

应用：

- Dynamic Workflow
- Charge Clear

---

## Mode 132

特点：

- Swap Mode
- 支持双次曝光
- 支持 Pre Offset
- 支持 Post Offset

主要用于：

- Lag Correction
- Ghost Correction

---

# 8. Mode Configuration Rules

不同 Mode 可以拥有不同参数。

例如：

- ROI
- Frame Rate
- Exposure Time

但是以下参数相同时，可共用模板：

- PGA
- ROI
- Binning

因此：

- Gain Template 可共用
- Defect Template 可共用

无需重复校准。

---

# 9. Engineering Notes

## ROI

ROI 最小建议：

256 × 256

要求：

- Width 为 8 的整数倍
- Height 为 8 的整数倍

---

## Trigger

Trigger 频率不能超过当前 Mode 配置的最大 Frame Rate。

否则：

- Trigger 无法响应
- Frame Loss
- Image Loss

---

## Frame Rate

Frame Rate 越高：

- Readout 时间越紧张
- Exposure Window 越短
- 对网络带宽要求越高

---

# 10. Common Problems

## Mode Configuration Error

表现：

- Detector 无响应
- 无法曝光
- 图像异常

排查：

- Mode 是否正确加载
- Firmware 是否支持
- SDK 是否匹配

---

## Wrong Template

表现：

- 图像校正失败
- Fixed Pattern Noise
- Defect 校正异常

排查：

确认：

- ROI
- PGA
- Binning

是否与模板一致。

---

# 11. Related Documents

- TimingWorkflow.md
- AcquisitionWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- CalibrationWorkflow.md
- ImageGenerationWorkflow.md

---

# 12. Summary

Mode 是动态探测器工作流程的核心配置单元，不同 Mode 定义了 Detector 的采集方式、曝光策略、读出方式及校正模板使用规则。正确理解 Mode 的配置原则，对于动态采集、校准、故障诊断及性能优化具有重要意义。