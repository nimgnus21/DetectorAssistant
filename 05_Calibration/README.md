# Calibration

Version: V2.0

Module: Detector Calibration

Status: Released

---

# 1. Purpose

Calibration 模块定义数字平板探测器（Flat Panel Detector, FPD）完整的校准理论、校准流程及校准数据管理体系。

本模块系统介绍：

- Calibration 基础理论
- Calibration Workflow
- Pixel Response 特性
- Offset Calibration
- Gain Calibration
- Defect Calibration
- Calibration Template
- Calibration Data 生命周期

Calibration 是 Detector 图像质量保证（Image Quality Assurance）的核心模块，也是 Image Processing、Image Diagnosis、Failure Analysis、Decision Tree 及 SOP 的基础。

---

# 2. Module Position

Calibration 位于 Detector 工作流程中 Signal Acquisition 与 Image Processing 之间。

整体位置如下：

```text
X-ray Exposure

↓

Scintillator

↓

Photodiode

↓

TFT Array

↓

Readout ASIC

↓

ADC

↓

Raw Image

↓

Calibration

├── Offset Correction
├── Gain Correction
└── Defect Correction

↓

Corrected Image

↓

Image Processing

↓

Display / Storage
```

Calibration 的作用是利用 Calibration Data 对 Raw Image 进行标准化校正，为后续图像处理提供可靠输入。

---

# 3. Module Objectives

Calibration 模块主要实现以下目标：

- 建立 Detector Pixel 响应基准
- 消除电子学 Offset
- 补偿 Pixel Response 差异
- 校正 Bad Pixel 与 Bad Line
- 建立 Calibration Data
- 管理 Calibration Template
- 提高图像一致性、均匀性及稳定性

---

# 4. Knowledge Architecture

```text
05_Calibration

├── CalibrationTheory
│   ├── CalibrationOverview.md
│   ├── CalibrationFlow.md
│   ├── CalibrationData.md
│   ├── PixelResponse.md
│   ├── OffsetTheory.md
│   ├── GainTheory.md
│   ├── DefectTheory.md
│   └── README.md
│
├── Offset
│   ├── OffsetWorkflow.md
│   ├── OffsetParameter.md
│   ├── OffsetFailure.md
│   ├── OffsetTroubleshooting.md
│   ├── OffsetFAQ.md
│   └── README.md
│
├── Gain
│   ├── GainWorkflow.md
│   ├── GainParameter.md
│   ├── GainFailure.md
│   ├── GainTroubleshooting.md
│   ├── GainFAQ.md
│   └── README.md
│
├── Defect
│   ├── DefectWorkflow.md
│   ├── DefectParameter.md
│   ├── DefectTemplate.md
│   ├── DefectFailure.md
│   ├── DefectTroubleshooting.md
│   ├── DefectFAQ.md
│   └── README.md
│
├── Template
│   ├── CalibrationTemplate.md
│   ├── TemplateManagement.md
│   ├── TemplateVersion.md
│   ├── TemplateBackup.md
│   ├── TemplateTroubleshooting.md
│   └── README.md
│
└── README.md
```

---

# 5. Knowledge Dependency

Calibration 模块按照理论、执行及管理三个层次组织。

```text
Calibration Theory

↓

Pixel Response

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Calibration Template

↓

Image Processing
```

其中：

- Offset Calibration 为 Gain Calibration 提供基准。
- Gain Calibration 为 Defect Calibration 提供归一化数据。
- Defect Calibration 建立 Defect Template。
- Calibration Template 统一管理全部 Calibration Data。
- Image Processing 使用 Active Calibration Template 完成图像校正。

---

# 6. Calibration Workflow

完整 Calibration Workflow 如下：

```text
Detector Ready

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Generate Calibration Template

↓

Verify Calibration Data

↓

Activate Template

↓

Image Verification

↓

Normal Clinical Operation
```

Calibration 完成后，应通过测试图像验证校准效果。

---

# 7. Calibration Data Architecture

Calibration Data 包括：

```text
Calibration Data

├── Offset Data
│
├── Gain Data
│
├── Defect Template
│
└── Calibration Metadata
```

上述数据统一封装为 Calibration Template，并由 Active Template 提供给 Image Pipeline 使用。

---

# 8. Relationship with Image Processing

Calibration 是 Image Pipeline 的前置校正模块。

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

↓

Image Enhancement

↓

Display
```

对应关系如下：

| Calibration Data | Image Processing Stage |
|------------------|------------------------|
| Offset Data | Offset Correction |
| Gain Data | Gain Correction |
| Defect Template | Defect Correction |

Calibration 不负责图像增强，仅负责基础校正。

---

# 9. Relationship with Other Modules

## Hardware

提供：

- Detector Hardware
- Pixel Signal
- Raw Data

---

## System

提供：

- Signal Flow
- Image Pipeline
- Communication
- Power Architecture

---

## Software

负责：

- Calibration Execution
- Calibration Data Management
- Template Management
- Detector Communication

---

## Failure Knowledge

基于 Calibration Failure 建立故障知识库。

---

## Decision Tree

基于 Calibration Workflow 建立标准诊断流程。

---

## SOP

定义 Calibration 标准操作规范及现场执行流程。

---

# 10. Learning Path

建议学习顺序如下：

```text
CalibrationTheory

↓

Offset

↓

Gain

↓

Defect

↓

Template

↓

06_ImageProcessing
```

每个模块均遵循：

```text
Theory

↓

Workflow

↓

Parameter

↓

Failure

↓

Troubleshooting

↓

FAQ
```

形成由理论到工程实践的完整知识链。

---

# 11. Failure Scope

Calibration 模块涉及以下主要故障：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Calibration Failure
- Calibration Data Corruption
- Calibration Template Failure
- Version Mismatch
- Template Activation Failure

所有故障均应按照对应模块的 Troubleshooting 文档进行分析。

---

# 12. Document Index

| Module | Description |
|---------|-------------|
| CalibrationTheory | Calibration 理论基础及数据模型 |
| Offset | Offset Calibration 全流程与故障分析 |
| Gain | Gain Calibration 全流程与故障分析 |
| Defect | Defect Calibration、Template 及图像缺陷校正 |
| Template | Calibration Data 生命周期及模板管理 |

---

# 13. Module Boundary

本模块负责：

- Calibration 理论
- Pixel Response
- Offset Calibration
- Gain Calibration
- Defect Calibration
- Calibration Data
- Calibration Template
- Template 生命周期管理

本模块不负责：

- X-ray Physics
- Detector 硬件设计
- Image Enhancement Algorithm
- 图像显示处理
- SDK API
- Detector 硬件维修

上述内容由对应模块负责。

---

# 14. Knowledge Graph

```text
Detector Hardware

↓

Raw Image

↓

Calibration Theory

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Calibration Data

↓

Calibration Template

↓

Active Template

↓

Image Pipeline

↓

Corrected Image

↓

Image Processing

↓

Failure Analysis

↓

Decision Tree

↓

SOP
```

---

# 15. Summary

Calibration 模块是数字平板探测器知识体系中的核心基础模块，也是连接 Detector Hardware 与 Image Processing 的关键桥梁。

本模块以 **Calibration Theory → Offset → Gain → Defect → Template** 为主线，完整覆盖校准理论、校准流程、Calibration Data 建立、Template 生命周期管理及故障分析体系，形成覆盖**理论、工程实现、数据管理、故障诊断及运维支持**的完整知识框架。

完成本模块后，建议继续学习 **06_ImageProcessing**，进一步理解 Calibration Data 如何在图像处理流水线中完成图像校正、增强及最终输出。