# DynamicCorrectionWorkflow

Version: V1.0

Module: Workflow

Status: Released

Related Documents:

- TimingWorkflow.md
- ModeWorkflow.md
- DynamicAcquisitionWorkflow.md
- CalibrationWorkflow.md
- ReadoutWorkflow.md
- ImageGenerationWorkflow.md
- WorkflowTroubleshooting.md

---

# 1. Purpose

Dynamic Correction Workflow 描述动态平板探测器（Dynamic Flat Panel Detector）在连续采集过程中，为保证动态图像质量所执行的各种校正流程。

动态图像由于连续曝光、连续读出及高速采集，相比静态平板需要更多的图像补偿算法。

Dynamic Correction Workflow 包括：

- Offset Correction
- Gain Correction
- Defect Correction
- Ghost Correction
- Lag Correction
- Swap Correction
- Dynamic Image Compensation

本文档用于说明动态图像校正的整体流程、工作原理及工程应用。

---

# 2. Scope

适用于：

- Dynamic Detector
- Fluoroscopy
- DSA
- CBCT
- Continuous Acquisition
- Swap Mode

适用于：

- Firmware
- FPGA
- SDK
- FAE
- Technical Support

---

# 3. Why Dynamic Correction is Required

动态采集过程中：

```text
Frame1

↓

Frame2

↓

Frame3

↓

Frame4
```

Detector 连续工作。

由于：

- X-Ray 连续曝光
- Scintillator 持续发光
- Photodiode 存在残余电荷
- Readout 存在时间延迟

导致：

- Ghost
- Lag
- Brightness Drift
- Residual Signal
- Dynamic Noise

因此需要动态图像校正流程。

---

# 4. Dynamic Correction Architecture

动态图像校正通常包含以下模块：

```text
Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Ghost Correction

↓

Lag Correction

↓

Dynamic Compensation

↓

Image Enhancement

↓

Output Image
```

各模块共同完成动态图像优化。

---

# 5. Offset Correction

目的：

消除 Detector 暗电流及电子零点偏移。

流程：

```text
Acquire Offset

↓

Generate Offset Template

↓

Subtract Offset

↓

Corrected Image
```

特点：

- 所有动态图必须执行
- Offset 应与当前 Mode 匹配

---

# 6. Gain Correction

目的：

校正 Pixel Sensitivity 差异。

流程：

```text
Flat Field

↓

Gain Template

↓

Pixel Compensation

↓

Uniform Image
```

说明：

当多个 Mode 满足以下条件时：

- ROI 相同
- PGA 相同
- Binning 相同

可共用 Gain Template。

---

# 7. Defect Correction

目的：

修正坏点及坏线。

流程：

```text
Defect Template

↓

Pixel Mapping

↓

Interpolation

↓

Corrected Image
```

Defect Template 应与 Detector 当前配置一致。

---

# 8. Ghost Correction

Ghost 来源：

Scintillator Afterglow。

形成过程：

```text
Exposure

↓

Scintillator 发光

↓

Exposure End

↓

持续发光

↓

Next Frame

↓

Ghost
```

特点：

- 高亮区域明显
- 与曝光剂量有关
- 与闪烁体材料有关

Ghost Correction 用于降低余辉造成的残影。

---

# 9. Lag Correction

Lag 来源：

Detector 内部残余电荷。

包括：

- Photodiode
- TFT
- Readout Circuit

形成过程：

```text
Exposure

↓

Charge Storage

↓

Readout

↓

Residual Charge

↓

Next Frame

↓

Lag
```

特点：

- 与读出时间有关
- 与 Frame Rate 有关
- 与 Detector 温度有关

Lag Correction 用于补偿残余电荷造成的拖尾。

---

# 10. Swap Correction

Swap Mode 是动态图常用校正方式。

典型流程：

```text
Exposure

↓

Image

↓

Offset

↓

Exposure

↓

Image
```

作用：

- 获取动态 Offset
- 降低 Ghost
- 降低 Lag

主要用于：

- Mode132
- Dynamic Detector

---

# 11. Pre Offset

Pre Offset：

曝光前采集 Offset。

流程：

```text
Acquire Offset

↓

Exposure

↓

Image
```

优点：

- Offset 与当前环境一致
- 温漂影响较小

适用于：

- Dynamic Acquisition
- Continuous Exposure

---

# 12. Post Offset

Post Offset：

曝光结束后采集 Offset。

流程：

```text
Exposure

↓

Image

↓

Acquire Offset
```

作用：

用于：

- Swap Correction
- Ghost Compensation
- Offset 更新

---

# 13. Dynamic Image Compensation

动态图像除基础校正外，还可能执行：

- Brightness Compensation
- Temporal Filtering
- Motion Compensation
- Dynamic Noise Reduction
- Residual Signal Compensation

具体算法由 Firmware 或 SDK 实现。

---

# 14. Workflow

动态图像校正完整流程：

```text
Start Acquisition

↓

Load Mode

↓

Acquire Offset

↓

Exposure

↓

Readout

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Ghost Correction

↓

Lag Correction

↓

Dynamic Compensation

↓

Image Enhancement

↓

Image Output

↓

Next Frame
```

---

# 15. Engineering Notes

## Ghost

来源：

Scintillator。

不是 Detector Electronics。

---

## Lag

来源：

Detector Electronics。

不是 Scintillator。

Ghost 与 Lag 应分别分析。

---

## Template Matching

动态图模板必须匹配：

- ROI
- PGA
- Binning
- Detector Model

否则可能导致：

- Image Artifact
- Brightness Error
- Calibration Failure

---

## Swap Mode

建议：

开启 Swap Mode 时：

确认：

- Firmware 支持
- SDK 支持
- Offset 更新正常

---

# 16. Common Problems

## Ghost Too Strong

检查：

- Scintillator
- Exposure Dose
- Swap 是否开启
- Offset 是否更新

---

## Lag Too Strong

检查：

- Readout Time
- Detector Temperature
- Frame Rate
- Firmware

---

## Brightness Drift

检查：

- Offset
- Gain
- Dynamic Compensation

---

## Correction Failure

检查：

- Template 是否正确
- ROI 是否一致
- PGA 是否一致
- Firmware 是否匹配

---

# 17. Related Documents

- TimingWorkflow.md
- ModeWorkflow.md
- DynamicAcquisitionWorkflow.md
- CalibrationWorkflow.md
- ImageGenerationWorkflow.md
- WorkflowTroubleshooting.md

---

# 18. Summary

Dynamic Correction Workflow 是动态平板图像处理的重要组成部分，涵盖 Offset、Gain、Defect、Ghost、Lag 及动态补偿等多个校正环节。通过合理的模板管理、Swap 模式及动态补偿算法，可有效降低连续曝光带来的余辉、残余电荷、亮度漂移及动态图像噪声，提高动态图像质量，并为 Firmware、SDK 及现场故障分析提供统一的流程参考。