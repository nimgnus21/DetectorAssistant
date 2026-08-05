# Gain Calibration

Version: V2.0

Module: Calibration

Status: Released

---

# 1. Purpose

Gain 模块描述数字平板探测器 Gain Calibration 的完整知识体系。

包括：

- Gain 理论
- Gain Workflow
- Gain 工程参数
- Gain Failure
- Gain Troubleshooting

本模块用于建立 Gain Calibration 的统一知识入口，为 Calibration、Image Processing、Failure Analysis 及现场技术支持提供标准参考。

---

# 2. Module Position

Gain Calibration 是 Detector Calibration 的第二阶段。

理论关系如下：

```text
Pixel Response

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Gain Calibration 建立 Detector 各 Pixel 的响应一致性模型，对 Pixel Sensitivity 差异进行补偿。

---

# 3. Knowledge Architecture

```text
Gain

├── GainWorkflow.md
├── GainParameter.md
├── GainFailure.md
├── GainTroubleshooting.md
├── GainFAQ.md
└── README.md
```

---

# 4. Knowledge Dependency

Gain 模块依赖以下理论文档：

```text
CalibrationOverview

↓

PixelResponse

↓

OffsetTheory

↓

GainTheory

↓

GainWorkflow

↓

GainParameter

↓

GainFailure

↓

GainTroubleshooting
```

Gain Calibration 建立在 Offset Calibration 基础之上。

---

# 5. Workflow Summary

Gain Calibration 标准流程：

```text
Detector Ready

↓

Verify Offset Calibration

↓

Prepare Uniform X-Ray Exposure

↓

Acquire Flat Field Image

↓

Gain Calculation

↓

Generate Gain Data

↓

Update Calibration Data

↓

Gain Correction
```

Gain Calibration 的核心目标是建立 Gain Data，提高 Detector 图像均匀性。

---

# 6. Input

执行 Gain Calibration 前，应满足以下条件：

- Detector Online
- Detector Ready
- Communication Normal
- Offset Calibration Completed
- Calibration Data Available
- X-Ray Generator Normal
- Uniform X-Ray Exposure
- Detector Imaging Area Fully Covered

---

# 7. Output

Gain Calibration 完成后生成：

- Gain Data
- Gain Table
- Calibration Data Update

上述数据将在所有后续图像处理中参与 Gain Correction。

---

# 8. Image Processing Position

Gain Correction 位于 Image Pipeline 中 Offset Correction 之后。

```text
Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Corrected Image
```

Gain Correction 用于补偿 Pixel Response 差异，提高图像整体均匀性。

---

# 9. Failure Scope

Gain Calibration Failure 包括：

- Calibration Start Failure
- Detector Failure
- Communication Failure
- Offset Dependency Failure
- Exposure Failure
- Flat Field Image Acquisition Failure
- Gain Calculation Failure
- Gain Data Failure
- Calibration Data Failure
- Gain Correction Failure

---

# 10. Troubleshooting Principle

建议按照以下顺序排查：

```text
Detector

↓

Communication

↓

Offset Calibration

↓

Exposure Condition

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Data

↓

Calibration Data

↓

Image Verification
```

所有排查应遵循 Calibration Workflow 与 Signal Flow 的执行顺序，避免跳步分析。

---

# 11. Relationship with Other Modules

## Calibration Theory

- ../CalibrationTheory/CalibrationOverview.md
- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationData.md

## Calibration

- ../Offset/
- ../Defect/

## System

- ../../02_System/ImagePipeline.md

## Failure Knowledge

- ../../07_FailureKnowledge/

## Decision Tree

- ../../09_DecisionTree/

## SOP

- ../../11_SOP/

---

# 12. Knowledge Graph

```text
Gain Theory

↓

Gain Workflow

↓

Gain Parameters

↓

Gain Failure

↓

Gain Troubleshooting

↓

Decision Tree

↓

SOP
```

---

# 13. Document Index

| Document | Purpose |
|----------|---------|
| GainWorkflow.md | Gain Calibration 标准执行流程 |
| GainParameter.md | Gain Calibration 工程参数定义 |
| GainFailure.md | Gain Calibration Failure 分类、原因及影响 |
| GainTroubleshooting.md | Gain Calibration 标准故障排查流程 |
| GainFAQ.md | Gain Calibration 常见问题及标准解答 |
| README.md | Gain 模块知识索引 |

---

# 14. Module Boundary

本模块负责：

- Gain Calibration
- Flat Field Image
- Gain Data
- Gain Correction
- Gain Failure
- Gain Troubleshooting

本模块不负责：

- Offset Calibration
- Defect Calibration
- 图像算法实现
- Firmware 软件实现
- SDK API
- Detector 硬件维修

上述内容分别由对应模块负责。

---

# 15. Learning Path

建议按照以下顺序学习 Gain 模块：

```text
GainTheory

↓

GainWorkflow

↓

GainParameter

↓

GainFailure

↓

GainTroubleshooting

↓

GainFAQ
```

完成 Gain 模块后，再继续学习 Defect Calibration 模块。

---

# 16. Relationship with Image Quality

Gain Calibration 直接影响：

- Image Uniformity
- Pixel Response Consistency
- Bright Area
- Dark Area
- Contrast Consistency
- Residual Fixed Pattern

Gain Data 异常会降低图像质量，并影响后续 Defect Calibration 的有效性。

---

# 17. Summary

Gain Calibration 是 Detector Calibration 的第二阶段，也是建立图像均匀性的核心过程。

通过采集均匀曝光图像并生成 Gain Data，系统能够补偿各 Pixel 的响应差异，提高图像一致性和稳定性。

Gain 模块与 Offset 模块共同构成图像校准的基础，为 Defect Calibration、Image Processing、Image Diagnosis、Decision Tree 及 SOP 提供可靠的数据基础。