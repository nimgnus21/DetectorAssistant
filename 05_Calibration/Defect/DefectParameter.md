# DefectParameter

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
- DefectWorkflow.md
- DefectTemplate.md
- DefectFailure.md
- DefectTroubleshooting.md
- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationData.md
- ../../02_System/ImagePipeline.md

---

# 1. Purpose

Defect Parameter 定义 Defect Calibration 过程中涉及的工程参数、输入条件、输出结果及质量评价指标。

本文件用于统一 Defect Calibration 相关参数定义，为 Workflow、Template、Failure、Troubleshooting、Decision Tree 及 SOP 提供统一的工程基础。

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

Defect Calibration 涉及的参数包括：

- Input Parameters
- Image Parameters
- Detection Parameters
- Defect Parameters
- Template Parameters
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

## Gain Status

Gain Calibration 应已成功完成。

Gain Data 应可正常使用。

---

## Communication Status

Detector 与主机通信正常。

---

## Calibration Command

系统下发 Defect Calibration 指令。

---

# 5. Image Parameters

Defect Calibration 所使用的 Calibration Image 应满足：

- 图像完整
- 图像无截断
- 图像无通信错误
- Offset Correction 正常
- Gain Correction 正常
- 曝光稳定
- 成像区域完整覆盖 Detector

Calibration Image 是 Defect Detection 的基础数据。

---

# 6. Detection Parameters

Defect Detection 包括：

- Pixel Response Analysis
- Pixel Consistency Analysis
- Threshold Comparison
- Defect Pixel Identification
- Defect Line Identification

Detection Algorithm 根据 Pixel 响应特性识别异常像素。

---

# 7. Defect Parameters

Defect Calibration 生成的数据包括：

- Defect Pixel List
- Defect Line List
- Defect Map
- Defect Count

上述数据用于 Defect Correction。

---

# 8. Template Parameters

Defect Calibration 完成后生成：

- Defect Template
- Defect Data
- Calibration Data Update

Defect Template 用于保存 Defect Detection 的结果，并参与后续图像校正。

Template 的生成、编辑、导入、导出及版本管理详见《DefectTemplate.md》。

---

# 9. Output Parameters

Defect Calibration 输出：

- Defect Data
- Defect Template
- Calibration Data Update

输出结果将在图像处理阶段参与 Defect Correction。

---

# 10. Quality Parameters

Defect Calibration 完成后，应重点确认：

## Defect Count

坏点数量是否在产品允许范围内。

---

## Defect Distribution

坏点分布是否合理。

---

## Cluster Defect

是否存在坏点聚集。

---

## Image Continuity

插值后的图像连续性是否正常。

---

## Image Artifact

是否存在新的图像伪影。

---

## Calibration Result

Calibration 是否成功完成。

---

# 11. Parameter Relationship

```text
Calibration Image

↓

Defect Detection

↓

Defect Pixel Identification

↓

Defect Template

↓

Calibration Data

↓

Defect Correction

↓

Corrected Image
```

---

# 12. Parameter Influence

Input Parameter 异常可能导致：

- Calibration Failure
- Workflow Interrupted

Image Parameter 异常可能导致：

- Defect Detection Error
- False Defect

Detection Parameter 异常可能导致：

- Bad Pixel Missed
- False Positive Defect

Template Parameter 异常可能导致：

- Defect Correction Failure
- Wrong Defect Compensation

Output Parameter 异常可能导致：

- Residual Defect
- Image Artifact
- Interpolation Error

---

# 13. Relationship with Troubleshooting

发生 Defect Calibration 异常时，应依次确认：

1. Detector Status
2. Offset Calibration Status
3. Gain Calibration Status
4. Calibration Image
5. Defect Detection
6. Defect Template
7. Calibration Data
8. Image Verification

---

# 14. Related Documents

Calibration：

- DefectWorkflow.md
- DefectTemplate.md
- DefectFailure.md
- DefectTroubleshooting.md

Theory：

- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationData.md

System：

- ../../02_System/ImagePipeline.md

---

# 15. Document Boundary

本文件负责：

- Defect Calibration 工程参数定义
- 输入条件
- Detection 参数
- Template 参数
- 输出结果
- 质量评价指标

本文件不负责：

- Defect Calibration 操作流程
- Template 生命周期管理
- Defect Failure 分析
- Defect Troubleshooting
- 软件界面说明
- SDK API

上述内容分别由对应文档说明。

---

# 16. Reference

## Theory

- Defect Calibration 基于 Calibration Image 识别响应异常 Pixel，并生成 Defect Template。
- Defect Parameter 定义适用于不同产品型号及软件版本，不依赖具体软件界面或参数命名。

## Engineering

- Defect Calibration 的输出结果包括 Defect Pixel、Defect Template 及 Calibration Data，并用于后续 Defect Correction。
- Defect Template 的管理方式（生成、编辑、下载、上传、叠加）由 DefectTemplate.md 统一说明。