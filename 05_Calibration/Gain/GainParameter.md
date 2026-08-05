# GainParameter

Version: V2.0

Module: Calibration

Source Level:
- Theory
- Engineering

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- GainWorkflow.md
- GainFailure.md
- GainTroubleshooting.md
- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationData.md
- ../../02_System/ImagePipeline.md

---

# 1. Purpose

Gain Parameter 定义 Gain Calibration 过程中涉及的工程参数、输入条件、输出结果及质量评价指标。

本文件用于统一 Gain Calibration 相关参数定义，为 Workflow、Failure、Troubleshooting、Decision Tree 及 SOP 提供统一的工程基础。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Parameter Classification

Gain Calibration 涉及的参数包括：

- Input Parameters
- Exposure Parameters
- Environment Parameters
- Acquisition Parameters
- Calculation Parameters
- Output Parameters
- Quality Parameters

---

# 4. Input Parameters

## Detector Status

Detector 应处于 Ready 状态。

---

## Offset Status

Offset Calibration 应已成功完成。

Offset Data 应可正常使用。

---

## Communication Status

Detector 与主机通信正常。

---

## Calibration Command

系统下发 Gain Calibration 指令。

---

# 5. Exposure Parameters

Gain Calibration 采用均匀曝光。

曝光条件应满足：

- X-Ray Generator 工作正常
- 曝光剂量稳定
- 曝光时间稳定
- 曝光区域覆盖整个 Detector
- X-Ray Beam 分布均匀

曝光条件直接影响 Gain Data 的准确性。

---

# 6. Environment Parameters

执行 Gain Calibration 时应满足：

- Detector 工作环境稳定
- 电源稳定
- 网络通信稳定
- 无机械振动
- 无外部遮挡
- Detector 前方无异物

环境异常可能导致 Flat Field Image 不均匀。

---

# 7. Acquisition Parameters

Gain Calibration 采集对象：

Flat Field Image。

采集要求：

- 均匀曝光
- 全图采集
- 所有 Pixel 参与计算
- 图像完整
- 图像无截断

采集结果作为 Gain Calculation 输入。

---

# 8. Calculation Parameters

系统依据 Flat Field Image 计算：

- Pixel Gain
- Gain Distribution
- Gain Table

Calculation Algorithm 由 Firmware 或上位机软件实现。

---

# 9. Output Parameters

Gain Calibration 输出：

- Gain Data
- Gain Table
- Calibration Data Update

输出结果用于图像处理阶段。

---

# 10. Quality Parameters

Gain Calibration 完成后，应重点关注：

## Calibration Result

Calibration Success / Failure。

---

## Image Uniformity

图像整体均匀性。

---

## Gain Distribution

Gain 分布是否连续。

---

## Response Consistency

Pixel Response 是否一致。

---

## Repeatability

重复 Calibration 后 Gain 是否稳定。

---

# 11. Parameter Relationship

```text
Uniform X-Ray

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Table

↓

Calibration Data

↓

Gain Correction

↓

Uniform Image
```

---

# 12. Parameter Influence

Input Parameter 异常可能导致：

- Calibration Failure
- Workflow Interrupted

Exposure Parameter 异常可能导致：

- Gain Error
- Image Nonuniformity
- Calibration Failure

Environment Parameter 异常可能导致：

- Flat Field Image Error
- Gain Instability

Calculation Parameter 异常可能导致：

- Gain Table Error
- Gain Correction Failure

Output Parameter 异常可能导致：

- Image Artifact
- Bright Area
- Dark Area
- Response Difference

---

# 13. Relationship with Troubleshooting

发生 Gain Calibration 异常时，应依次确认：

1. Detector Status
2. Offset Calibration Status
3. Communication Status
4. Exposure Condition
5. Flat Field Image
6. Gain Calculation
7. Gain Data Generation
8. Calibration Data Update

---

# 14. Related Documents

Calibration：

- GainWorkflow.md
- GainFailure.md
- GainTroubleshooting.md

Theory：

- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationData.md

System：

- ../../02_System/ImagePipeline.md

---

# 15. Document Boundary

本文件负责：

- Gain Calibration 工程参数定义
- 输入条件
- 曝光条件
- 输出结果
- 质量评价指标

本文件不负责：

- Gain Calibration 操作流程
- Gain Failure 分析
- Gain Troubleshooting
- 软件界面说明
- SDK API

上述内容分别由对应文档说明。

---

# 16. Reference

## Theory

- Gain Calibration 基于均匀曝光建立 Gain Data。
- Gain Parameter 用于保证 Gain Calibration 过程及结果满足图像均匀性要求。

## Engineering

- Parameter 定义适用于不同产品型号及软件版本，不依赖具体软件界面或参数命名。
```