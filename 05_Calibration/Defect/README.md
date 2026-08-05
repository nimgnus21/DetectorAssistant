# Defect Calibration

Version: V2.0

Module: Calibration

Status: Released

---

# 1. Purpose

Defect 模块描述数字平板探测器 Defect Calibration 的完整知识体系。

包括：

- Defect 理论
- Defect Workflow
- Defect 工程参数
- Defect Template
- Defect Failure
- Defect Troubleshooting
- Defect FAQ

本模块用于建立 Defect Calibration 的统一知识入口，为 Calibration、Image Processing、Failure Analysis、Template Management 及现场技术支持提供标准参考。

---

# 2. Module Position

Defect Calibration 是 Detector Calibration 的第三阶段，也是 Calibration 的最终阶段。

理论关系如下：

```text
Pixel Response

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Image Processing
```

Defect Calibration 用于识别响应异常的 Pixel，并建立 Defect Template，为 Defect Correction 提供基础数据。

---

# 3. Knowledge Architecture

```text
Defect

├── DefectWorkflow.md
├── DefectParameter.md
├── DefectTemplate.md
├── DefectFailure.md
├── DefectTroubleshooting.md
├── DefectFAQ.md
└── README.md
```

---

# 4. Knowledge Dependency

Defect 模块依赖以下理论文档：

```text
CalibrationOverview

↓

PixelResponse

↓

OffsetTheory

↓

GainTheory

↓

DefectTheory

↓

DefectWorkflow

↓

DefectParameter

↓

DefectTemplate

↓

DefectFailure

↓

DefectTroubleshooting
```

Defect Calibration 建立在 Offset Calibration 与 Gain Calibration 完成的基础之上。

---

# 5. Workflow Summary

Defect Calibration 标准流程如下：

```text
Detector Ready

↓

Verify Offset Calibration

↓

Verify Gain Calibration

↓

Acquire Calibration Image

↓

Defect Detection

↓

Generate Defect Template

↓

Update Calibration Data

↓

Defect Correction
```

Defect Calibration 的核心目标是建立准确的 Defect Template，用于后续图像校正。

---

# 6. Input

执行 Defect Calibration 前，应满足以下条件：

- Detector Online
- Detector Ready
- Communication Normal
- Offset Calibration Completed
- Gain Calibration Completed
- Calibration Data Available
- Calibration Image Available

---

# 7. Output

Defect Calibration 完成后生成：

- Defect Template
- Defect Pixel List
- Defect Line List
- Defect Map
- Calibration Data Update

上述数据将在后续图像处理中参与 Defect Correction。

---

# 8. Image Processing Position

Defect Correction 位于 Image Pipeline 的最后一级校正。

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

Defect Correction 根据 Defect Template 对异常 Pixel 进行补偿，提高图像连续性与完整性。

---

# 9. Defect Template Position

Defect Template 是 Defect Calibration 的核心输出，也是 Defect Correction 的核心输入。

生命周期如下：

```text
Generate

↓

Save

↓

Upload

↓

Overlay

↓

Activate

↓

Image Correction

↓

Update
```

Active Template 是参与图像校正的最终模板。

---

# 10. Failure Scope

Defect Calibration Failure 包括：

- Calibration Start Failure
- Calibration Image Acquisition Failure
- Defect Detection Failure
- Defect Template Generation Failure
- Template Upload Failure
- Template Download Failure
- Template Overlay Failure
- Template Modification Failure
- Calibration Data Update Failure
- Defect Correction Failure

---

# 11. Troubleshooting Principle

建议按照以下顺序排查：

```text
Detector

↓

Communication

↓

Offset Calibration

↓

Gain Calibration

↓

Calibration Image

↓

Defect Detection

↓

Defect Template

↓

Template Management

↓

Calibration Data

↓

Image Verification
```

所有排查均应遵循 Calibration Workflow 与 Template Lifecycle 的执行顺序。

---

# 12. Relationship with Other Modules

## Calibration Theory

- ../CalibrationTheory/CalibrationOverview.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationData.md
- ../CalibrationTheory/DefectTheory.md

## Calibration

- ../Offset/
- ../Gain/

## System

- ../../02_System/ImagePipeline.md

## Software

- ../../04_Software/

## Failure Knowledge

- ../../07_FailureKnowledge/

## Decision Tree

- ../../09_DecisionTree/

## SOP

- ../../11_SOP/

---

# 13. Knowledge Graph

```text
Defect Theory

↓

Defect Workflow

↓

Defect Parameters

↓

Defect Template

↓

Defect Failure

↓

Defect Troubleshooting

↓

Decision Tree

↓

SOP
```

---

# 14. Document Index

| Document | Purpose |
|----------|---------|
| DefectWorkflow.md | Defect Calibration 标准执行流程 |
| DefectParameter.md | Defect Calibration 工程参数定义 |
| DefectTemplate.md | Defect Template 生命周期及管理 |
| DefectFailure.md | Defect Calibration Failure 分类、原因及影响 |
| DefectTroubleshooting.md | Defect Calibration 标准故障排查流程 |
| DefectFAQ.md | Defect Calibration 常见问题及标准解答 |
| README.md | Defect 模块知识索引 |

---

# 15. Module Boundary

本模块负责：

- Defect Calibration
- Defect Detection
- Defect Template
- Template Management
- Defect Correction
- Defect Failure
- Defect Troubleshooting

本模块不负责：

- Offset Calibration
- Gain Calibration
- 图像插值算法实现
- Firmware 软件实现
- SDK API
- Detector 硬件维修

上述内容分别由对应模块负责。

---

# 16. Learning Path

建议按照以下顺序学习 Defect 模块：

```text
DefectTheory

↓

DefectWorkflow

↓

DefectParameter

↓

DefectTemplate

↓

DefectFailure

↓

DefectTroubleshooting

↓

DefectFAQ
```

完成 Defect 模块后，可继续学习 Image Diagnosis、Failure Knowledge、Decision Tree 及 SOP。

---

# 17. Relationship with Image Quality

Defect Calibration 直接影响：

- Bad Pixel Correction
- Bad Line Correction
- Image Continuity
- Image Uniformity
- Image Artifact
- Residual Defect
- Local Bright Pixel
- Local Dark Pixel

Defect Template 的准确性直接决定 Defect Correction 的最终效果。

---

# 18. Summary

Defect Calibration 是 Detector Calibration 的最终阶段，也是保证图像完整性的关键环节。

通过分析 Calibration Image、识别异常 Pixel 并生成 Defect Template，系统能够在图像处理过程中对异常 Pixel 和异常 Line 进行补偿，从而提高图像连续性、均匀性及整体质量。

Defect 模块与 Offset 模块、Gain 模块共同构成 Detector Calibration 的完整体系，为后续 Image Processing、Image Diagnosis、Failure Analysis、Decision Tree 及 SOP 提供可靠的数据基础。