# OffsetParameter

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
- OffsetWorkflow.md
- OffsetFailure.md
- OffsetTroubleshooting.md
- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationData.md
- ../../02_System/ImagePipeline.md

---

# 1. Purpose

Offset Parameter 定义 Offset Calibration 过程中涉及的工程参数、输入条件、输出结果及质量评价指标。

本文件用于统一 Offset Calibration 相关术语，为 Calibration、Troubleshooting、Decision Tree 及 SOP 提供统一参数定义。

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

Offset Calibration 涉及的参数可分为：

- Input Parameters
- Environment Parameters
- Acquisition Parameters
- Output Parameters
- Quality Parameters

---

# 4. Input Parameters

## Detector Status

Detector 应处于 Ready 状态。

---

## Communication Status

Detector 与主机通信正常。

---

## Exposure Condition

无 X-Ray 曝光。

---

## Calibration Command

系统下发 Offset Calibration 指令。

---

# 5. Environment Parameters

执行 Offset Calibration 时应满足：

- 无 X-Ray 辐射
- 无杂散射线
- Detector 工作环境稳定
- 电源稳定
- 网络通信稳定

环境异常可能影响 Offset Data 的准确性。

---

# 6. Acquisition Parameters

Offset Calibration 采集对象：

Dark Image。

采集要求：

- 无曝光
- 全图采集
- 所有 Pixel 参与计算

采集结果作为 Offset Calculation 输入。

---

# 7. Calculation Parameters

系统依据 Dark Image 计算：

- Pixel Offset
- Global Offset Distribution
- Offset Table

Calculation Algorithm 由 Firmware 或上位机软件实现。

---

# 8. Output Parameters

Offset Calibration 输出：

- Offset Data
- Offset Table
- Calibration Data Update

输出结果用于图像处理阶段。

---

# 9. Quality Parameters

Offset Calibration 完成后，应关注：

## Calibration Result

Calibration Success / Failure。

---

## Offset Uniformity

各 Pixel Offset 分布是否正常。

---

## Background Stability

背景灰度是否稳定。

---

## Fixed Pattern Noise

是否存在固定模式噪声。

---

## Offset Repeatability

重复 Calibration 结果是否保持一致。

---

# 10. Parameter Relationship

```text
Input Condition

↓

Dark Image

↓

Offset Calculation

↓

Offset Data

↓

Image Correction

↓

Corrected Image
```

---

# 11. Parameter Influence

Input Parameter 异常可能导致：

- Calibration Failure
- Offset Error
- Offset Data Error

Environment Parameter 异常可能导致：

- Background Noise
- Offset Instability

Calculation Parameter 异常可能导致：

- Offset Correction Failure

Output Parameter 异常可能导致：

- Image Artifact
- Fixed Pattern Noise

---

# 12. Relationship with Troubleshooting

排查 Offset Calibration 故障时，应依次确认：

1. Detector Status
2. Communication Status
3. Exposure Condition
4. Dark Image Acquisition
5. Offset Calculation
6. Offset Data Generation
7. Calibration Data Update

---

# 13. Related Documents

Calibration：

- OffsetWorkflow.md
- OffsetFailure.md
- OffsetTroubleshooting.md

Theory：

- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationData.md

System：

- ../../02_System/ImagePipeline.md

---

# 14. Document Boundary

本文件负责：

- Offset Calibration 工程参数定义
- 输入条件
- 输出结果
- 环境要求
- 质量评价指标

本文件不负责：

- Offset Calibration 操作流程
- Offset Failure 分析
- Offset Troubleshooting
- 软件界面说明
- SDK API

---

# 15. Reference

## Theory

- Offset Calibration 通过 Dark Image 建立 Offset Data。
- Offset Parameter 用于保证 Calibration 过程及结果满足图像校正要求。

## Engineering

- Parameter 定义适用于不同软件版本及不同 Detector 产品，不依赖具体软件界面或参数命名。