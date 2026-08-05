# Offset Calibration

Version: V2.0

Module: Calibration

Status: Released

---

# 1. Purpose

Offset 模块描述数字平板探测器 Offset Calibration 的完整知识体系。

包括：

- Offset 理论
- Offset Workflow
- Offset 工程参数
- Offset Failure
- Offset Troubleshooting

本模块用于建立 Offset Calibration 的统一知识入口。

---

# 2. Module Position

Offset Calibration 是整个 Calibration 的第一阶段。

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

Offset Calibration 建立 Detector 的暗场响应模型。

后续 Gain Calibration 与 Defect Calibration 均依赖 Offset Calibration 的结果。

---

# 3. Knowledge Architecture

```text
Offset

├── OffsetWorkflow.md
├── OffsetParameter.md
├── OffsetFailure.md
├── OffsetTroubleshooting.md
└── README.md
```

---

# 4. Knowledge Dependency

Offset 模块依赖以下理论：

```text
CalibrationOverview

↓

PixelResponse

↓

OffsetTheory

↓

OffsetWorkflow

↓

OffsetParameter

↓

OffsetFailure

↓

OffsetTroubleshooting
```

---

# 5. Workflow Summary

Offset Calibration 流程：

```text
Detector Ready

↓

No X-Ray

↓

Acquire Dark Image

↓

Offset Calculation

↓

Generate Offset Data

↓

Update Calibration Data

↓

Image Correction
```

---

# 6. Input

执行 Offset Calibration 前应满足：

- Detector Online
- Detector Ready
- Network Normal
- No X-Ray
- Calibration Command Available

---

# 7. Output

Offset Calibration 完成后生成：

- Offset Data
- Calibration Data Update

输出结果参与所有后续图像处理。

---

# 8. Image Processing Position

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

Offset Correction 为图像校正第一步。

---

# 9. Failure Scope

Offset Calibration Failure 包括：

- Calibration Start Failure
- Detector Failure
- Communication Failure
- Dark Image Failure
- Offset Calculation Failure
- Calibration Data Failure
- Offset Correction Failure

---

# 10. Troubleshooting Principle

建议排查顺序：

```text
Detector

↓

Communication

↓

Calibration Command

↓

Dark Image

↓

Offset Calculation

↓

Calibration Data

↓

Image Verification
```

遵循信号流方向逐级定位问题。

---

# 11. Relationship with Other Modules

Theory：

- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Image：

- ../../08_ImageDiagnosis/

Failure：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 12. Knowledge Graph

```text
Offset Theory

↓

Offset Workflow

↓

Offset Parameters

↓

Offset Failure

↓

Offset Troubleshooting

↓

Decision Tree

↓

SOP
```

---

# 13. Document Index

| Document | Purpose |
|----------|---------|
| OffsetWorkflow.md | Offset Calibration 标准流程 |
| OffsetParameter.md | 工程参数定义 |
| OffsetFailure.md | Failure 分类与影响 |
| OffsetTroubleshooting.md | 标准故障排查流程 |
| README.md | 模块索引 |

---

# 14. Module Boundary

本模块负责：

- Offset Calibration
- Offset Data
- Offset Failure
- Offset Troubleshooting

本模块不负责：

- Gain Calibration
- Defect Calibration
- 图像算法实现
- Firmware 软件实现
- SDK API

上述内容分别由对应模块负责。

---

# 15. Related Documents

Theory：

- ../CalibrationTheory/

Calibration：

- ../Gain/
- ../Defect/

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

SOP：

- ../../11_SOP/

---

# 16. Summary

Offset Calibration 是 Detector Calibration 的基础。

完成 Offset Calibration 后，系统获得稳定的暗场响应数据，为 Gain Calibration、Defect Calibration 及后续图像处理提供基础数据支持。

Offset 模块构成整个 Calibration 知识体系的第一层工程实践内容。