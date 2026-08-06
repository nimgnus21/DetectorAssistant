# ModeConfiguration

Version: V1.0

Module: 17_Tools / SDKTool

Status: Draft

Applicable Products:

- Dynamic Flat Panel Detector
- Static Flat Panel Detector
- Pluto Dynamic Series
- SDK_AIO Platform

Related Documents:

- README.md
- CalibrationTools.md
- FirmwareUpgrade.md
- ../../06_Workflow/ConfigurationWorkflow.md
- ../../06_Workflow/ModeWorkflow.md
- ../../06_Workflow/DynamicAcquisitionWorkflow.md
- ../../06_Workflow/TimingWorkflow.md

---

# 1. Purpose

Mode Configuration 用于配置 Detector 的工作模式（Mode），决定探测器在不同应用场景下的采集方式、曝光方式、读出时序及动态图像输出策略。

Mode 是 Detector 运行过程中最重要的配置项之一。

错误的 Mode 配置可能导致：

- 无法曝光
- 无法触发
- 图像异常
- Image Loss
- Timeout
- Ghost
- Lag
- Frame Rate 异常

---

# 2. Overview

Detector 的每一种工作模式均由一组配置参数组成。

Mode Configuration 包括：

- Acquisition Mode
- Exposure Mode
- Trigger Mode
- Readout Mode
- ROI
- Frame Rate
- PGA
- Gain
- Offset
- Defect
- Dynamic Parameters

不同 Mode 可以理解为不同的"运行模板"。

系统初始化时：

```text
Load Mode

↓

Read Parameters

↓

Load Calibration

↓

Initialize Detector

↓

Ready
```

---

# 3. Mode Architecture

```text
Mode

├── Basic Configuration
│      ├── ROI
│      ├── Binning
│      ├── Frame Rate
│      └── Trigger
│
├── Exposure
│      ├── Enable
│      ├── Integration
│      └── Pulse
│
├── Readout
│      ├── Readout Time
│      ├── Readout Direction
│      └── Timing
│
├── Calibration
│      ├── Offset
│      ├── Gain
│      └── Defect
│
└── Dynamic
       ├── Swap
       ├── Ghost
       └── Lag
```

---

# 4. Common Mode Types

根据目前培训资料，常见 Mode 包括：

| Mode | Description |
|------|-------------|
| Mode128 | 清空采集模式（Clear Acquisition） |
| Mode129 | 脉冲采集模式（Pulse Acquisition） |
| Mode131 | 清空采集模式（另一工作流程） |
| Mode132 | Swap Mode（动态残影校正） |

> **说明**
>
> 当前文档仅依据现有培训资料整理。各 Mode 的详细寄存器定义、参数含义及时序实现需以 SDK/Firmware 官方文档为准。

---

# 5. Configuration Items

每个 Mode 一般包含以下配置。

## ROI

配置：

- Width
- Height
- Start X
- Start Y

工程要求：

- 最小 ROI：256 × 256（当前平台培训要求）
- Width 为 8 的整数倍
- Height 为 8 的整数倍

---

## Frame Rate

配置：

- FPS
- Exposure Time
- Readout Time

要求：

Frame Rate 应满足当前硬件能力。

设置过高可能导致：

- Image Loss
- Timeout

---

## Trigger

支持：

- Internal Trigger
- External Trigger
- Software Trigger

动态图通常采用：

External Trigger。

---

## Exposure

包括：

- Exposure Mode
- Enable Time
- Integration Time

Exposure Window 必须满足当前时序要求。

---

## Readout

包括：

- Readout Time
- Readout Direction

Readout 时间决定：

- 最大 FPS
- 最小曝光间隔

---

## PGA

决定模拟放大倍数。

不同 PGA：

通常需要不同：

- Gain
- Offset

模板。

---

# 6. Mode Loading Workflow

```text
Read Mode File

↓

Parse Parameters

↓

Check Detector Model

↓

Load ROI

↓

Load Trigger

↓

Load Frame Rate

↓

Load Calibration

↓

Detector Ready
```

任何步骤失败：

Detector 不应进入 Ready 状态。

---

# 7. Engineering Experience

## 7.1 共用 Calibration Template

培训资料指出：

多个 Mode 在满足以下条件时：

- PGA 相同
- ROI 相同
- Binning 相同

可以共用：

- Gain Template
- Defect Template

这样可以减少重复校准。

---

## 7.2 ROI 配置

工程建议：

ROI：

- 不小于 256 × 256
- Width 为 8 的整数倍
- Height 为 8 的整数倍

否则：

Firmware 可能拒绝配置。

---

## 7.3 Frame Rate

动态图：

Frame Rate 不应超过当前 Mode 能够支持的最大值。

否则：

Detector 无法响应 Trigger。

可能表现为：

- Timeout
- Image Loss

---

## 7.4 Swap Mode

Mode132：

主要用于：

Ghost Correction。

支持：

- Pre Offset
- Post Offset

降低动态图残影。

---

# 8. Common Problems

## Mode Cannot Be Loaded

检查：

- Firmware Version
- SDK Version
- Mode File

---

## Trigger Failure

检查：

- Trigger Source
- Trigger Edge
- Trigger Timing

---

## Image Loss

检查：

- Frame Rate
- Network
- Jumbo Frame
- Mode Parameters

---

## Calibration Mismatch

检查：

- ROI
- PGA
- Gain Template
- Defect Template

---

## Timeout

检查：

- Trigger
- Frame Rate
- Exposure Time

---

# 9. Troubleshooting

建议排查流程：

```text
Mode File

↓

Firmware

↓

ROI

↓

Frame Rate

↓

Trigger

↓

Calibration

↓

Detector Ready

↓

Acquire Image
```

---

# 10. Best Practices

建议：

- 使用正式发布的 Mode 文件
- 修改 Mode 前备份原配置
- 修改后重新加载 Detector
- 完成一次完整采图测试
- 验证 Calibration 是否仍然匹配

---

# 11. FAQ

## Q1：Mode 修改后为什么需要重新连接 Detector？

A：

多数 SDK 在初始化时读取 Mode 配置。

修改后重新初始化，可确保所有参数重新加载。

---

## Q2：不同 Mode 可以共用 Gain 吗？

A：

可以，但应满足：

- ROI 相同
- PGA 相同
- Binning 相同

否则建议重新校准。

---

## Q3：为什么 Frame Rate 设置过高会导致 Image Loss？

A：

当 Trigger 频率超过当前 Mode 的处理能力时，Detector 无法完成上一帧读出，就可能出现丢帧（Image Loss）或 Timeout。

---

## Q4：Mode132 的主要作用是什么？

A：

根据培训资料，Mode132 为 **Swap Mode**，主要用于动态采集中的残影（Ghost）校正，通过 Pre Offset 或 Post Offset 的方式降低动态图像残影。

---

# 12. References

- SDK User Manual
- Detector Mode Specification
- Dynamic Detector Training Notes
- FAE Engineering Experience
- Internal Development Training

---

# 13. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 Mode Configuration 文档，整理 Mode 配置结构、参数说明、工程经验及常见问题。 |