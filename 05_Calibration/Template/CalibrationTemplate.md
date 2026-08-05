# CalibrationTemplate

Version: V2.0

Module: Calibration

Source Level:
- Engineering
- Product Implementation

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- ../CalibrationTheory/CalibrationData.md
- ../CalibrationTheory/CalibrationFlow.md
- ../Offset/README.md
- ../Gain/README.md
- ../Defect/README.md
- TemplateManagement.md
- TemplateVersion.md
- TemplateBackup.md
- TemplateTroubleshooting.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Calibration Template 用于统一管理 Detector Calibration 的全部校准数据。

Calibration Template 是 Detector Calibration 的最终输出，也是 Detector 图像校正的基础数据。

本文件定义 Calibration Template 的组成、生命周期、功能定位及与 Image Processing 的关系。

---

# 2. Definition

Calibration Template 是 Detector 当前所有 Calibration Data 的集合。

Calibration Template 并非单一参数，而是由多个 Calibration 数据共同组成的数据包。

Calibration Template 用于保存 Detector 当前有效的 Calibration 状态。

---

# 3. Composition

Calibration Template 包括以下内容：

- Offset Data
- Gain Data
- Defect Template
- Calibration Metadata

不同产品的软件版本可能包含其它 Calibration 数据，但均属于 Calibration Template 的组成部分。

---

# 4. Calibration Data Structure

Calibration Template 的逻辑结构如下：

```text
Calibration Template

├── Offset Data
│
├── Gain Data
│
├── Defect Template
│
└── Calibration Metadata
```

Calibration Metadata 用于记录 Calibration 相关信息，不参与图像校正计算。

---

# 5. Position in Calibration

Calibration Template 是 Calibration Workflow 的最终输出。

执行流程如下：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Generate Calibration Template

↓

Save Calibration Data

↓

Activate Template
```

Calibration 完成后，Detector 使用当前 Calibration Template 进行图像校正。

---

# 6. Relationship with Image Processing

Calibration Template 在 Image Pipeline 中提供所有校正数据。

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

Offset Correction 使用 Offset Data。

Gain Correction 使用 Gain Data。

Defect Correction 使用 Defect Template。

---

# 7. Template Lifecycle

Calibration Template 生命周期如下：

```text
Create

↓

Generate

↓

Save

↓

Verify

↓

Upload

↓

Download

↓

Activate

↓

Image Processing

↓

Backup

↓

Restore

↓

Update
```

整个生命周期由 Template Management 模块负责管理。

---

# 8. Template Generation

Calibration Template 在以下条件满足后生成：

- Offset Calibration Completed
- Gain Calibration Completed
- Defect Calibration Completed

系统整合全部 Calibration Data，形成新的 Calibration Template。

---

# 9. Template Activation

Calibration Template 保存后不会立即参与图像处理。

只有 Active Template 才参与 Image Pipeline。

Activation 完成后：

- Detector 更新 Calibration Data
- Image Processing 使用新的 Calibration Template
- 后续图像全部采用新的 Calibration 数据

---

# 10. Template Validation

Calibration Template 更新后，应验证：

- Template 完整性
- Calibration Data 完整性
- Version 正确
- Active Template 已更新
- 图像质量正常

验证通过后方可投入使用。

---

# 11. Relationship with Detector

Detector 内部保存当前 Calibration Template。

Detector 初始化时加载：

- Offset Data
- Gain Data
- Defect Template

完成 Calibration Data 初始化后进入 Ready 状态。

---

# 12. Relationship with Calibration Data

Calibration Template 是 Calibration Data 的统一载体。

```text
Calibration Data

↓

Offset Data

↓

Gain Data

↓

Defect Template

↓

Calibration Template
```

Calibration Template 保存 Detector 当前所有有效校准结果。

---

# 13. Relationship with Software

软件负责：

- 创建 Template
- 保存 Template
- 加载 Template
- 上传 Template
- 下载 Template
- 激活 Template
- 校验 Template

软件不负责 Calibration Algorithm。

---

# 14. Common Operations

Calibration Template 常见操作包括：

- Generate
- Save
- Load
- Upload
- Download
- Activate
- Verify
- Backup
- Restore
- Update

详细流程见：

- TemplateManagement.md
- TemplateBackup.md

---

# 15. Typical Failure

Calibration Template 常见异常包括：

- Template Generation Failure
- Template Save Failure
- Template Load Failure
- Template Upload Failure
- Template Download Failure
- Template Activation Failure
- Template Version Mismatch
- Calibration Data Corruption
- Active Template Invalid

详细分析见：

- TemplateTroubleshooting.md

---

# 16. Knowledge Graph

```text
Offset

↓

Gain

↓

Defect

↓

Calibration Data

↓

Calibration Template

↓

Active Template

↓

Image Pipeline

↓

Image Correction
```

---

# 17. Related Documents

Calibration：

- ../Offset/
- ../Gain/
- ../Defect/

Template：

- TemplateManagement.md
- TemplateVersion.md
- TemplateBackup.md
- TemplateTroubleshooting.md

Theory：

- ../CalibrationTheory/CalibrationData.md
- ../CalibrationTheory/CalibrationFlow.md

System：

- ../../02_System/ImagePipeline.md

Software：

- ../../04_Software/iDetector.md

---

# 18. Document Boundary

本文件负责：

- Calibration Template 定义
- Calibration Template 组成
- 生命周期
- Image Processing 关系
- Calibration Data 关系
- Active Template 概念

本文件不负责：

- Template 操作流程
- Template 版本管理
- Backup / Restore
- 故障分析
- 软件界面
- SDK API

上述内容分别由对应文档说明。

---

# 19. Summary

Calibration Template 是 Detector Calibration 的最终成果，也是整个图像校正系统的数据基础。

通过统一管理 Offset Data、Gain Data、Defect Template 及 Calibration Metadata，Calibration Template 为 Detector 提供完整、可验证、可管理的 Calibration 数据，并作为 Image Processing 的唯一校准数据来源。