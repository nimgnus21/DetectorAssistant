# DefectTemplate

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
- DefectWorkflow.md
- DefectParameter.md
- DefectFailure.md
- DefectTroubleshooting.md
- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationData.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Defect Template 用于保存 Defect Calibration 的检测结果，并作为 Defect Correction 的输入数据。

本文件描述 Defect Template 的组成、生命周期、生成方式、编辑方式、管理方式及使用流程，为现场维护、售后支持及产品开发提供统一参考。

---

# 2. Definition

Defect Template 是 Defect Calibration 完成后生成的数据文件。

Template 中保存 Detector 当前识别出的异常 Pixel、异常 Line 及相关校正信息。

图像处理过程中，Image Pipeline 根据 Defect Template 对异常 Pixel 进行 Defect Correction。

---

# 3. Template Lifecycle

Defect Template 生命周期如下：

```text
Create

↓

Generate

↓

Save

↓

Load

↓

Overlay

↓

Modify

↓

Upload

↓

Download

↓

Activate

↓

Image Correction

↓

Update
```

---

# 4. Template Generation

Defect Template 由 Defect Calibration 自动生成。

标准流程：

```text
Detector Ready

↓

Verify Offset Calibration

↓

Verify Gain Calibration

↓

Acquire Calibration Images

↓

Defect Detection

↓

Generate Defect Template

↓

Save Calibration Data
```

生成完成后，Template 保存至 Calibration Data。

---

# 5. Template Composition

Defect Template 包括：

- Defect Pixel Information
- Defect Line Information
- Defect Map
- Defect Count
- Calibration Metadata
- Template Version

Template 内容用于 Defect Correction。

---

# 6. Template Types

系统支持以下 Template：

## Factory Template

Factory Calibration 生成。

记录出厂时确认的 Defect 信息。

通常不允许修改。

---

## User Template

用户重新 Calibration 或人工编辑后生成。

保存现场新增 Defect。

可根据维护需求更新。

---

## Active Template

当前参与图像校正的 Template。

Image Pipeline 使用 Active Template 执行 Defect Correction。

---

# 7. Template Overlay

系统支持 Template Overlay。

多个 Template 可按照规则组合生成最终 Active Template。

典型关系：

```text
Factory Template

+

User Template

↓

Overlay

↓

Active Template
```

Overlay 后生成新的 Defect Map。

---

# 8. Template Modification

支持人工编辑 Template。

包括：

- Add Defect Pixel
- Delete Defect Pixel
- Add Defect Line
- Delete Defect Line

编辑完成后应重新保存 Template。

---

# 9. Template Upload

Template 可上传至 Detector。

上传内容包括：

- Defect Template
- Calibration Data

上传完成后应验证 Template 是否生效。

---

# 10. Template Download

Template 可从 Detector 下载。

下载目的包括：

- 数据备份
- 数据恢复
- 技术分析
- 故障定位

下载后应确认版本一致性。

---

# 11. Template Validation

Template 更新后应确认：

- Upload Success
- Download Success
- Version Correct
- Active Template Updated
- Image Quality Improved

验证完成后方可投入使用。

---

# 12. Relationship with Calibration

Defect Template 建立于 Calibration 之后。

执行顺序：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Generate Defect Template

↓

Image Processing
```

---

# 13. Relationship with Image Processing

Defect Template 在 Image Pipeline 中的位置：

```text
Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Template

↓

Defect Correction

↓

Corrected Image
```

Defect Correction 根据 Template 对异常 Pixel 进行补偿。

---

# 14. Relationship with Calibration Data

Defect Template 属于 Calibration Data 的组成部分。

Calibration Data 包括：

- Offset Data
- Gain Data
- Defect Template

上述数据共同参与图像校正。

---

# 15. Common Operations

常见操作包括：

- Generate Template
- Load Template
- Save Template
- Upload Template
- Download Template
- Modify Template
- Overlay Template
- Activate Template
- Verify Template

---

# 16. Common Failure

Template 相关异常包括：

- Template Generation Failure
- Template Save Failure
- Template Upload Failure
- Template Download Failure
- Template Overlay Failure
- Template Version Mismatch
- Active Template Not Updated
- Template Corruption

详细处理流程见：

DefectFailure.md

DefectTroubleshooting.md

---

# 17. Diagnostic Checkpoints

维护过程中建议确认：

- Template 是否生成
- Template 是否完整
- Template Version 是否正确
- Upload 是否成功
- Download 是否成功
- Overlay 是否完成
- Active Template 是否更新
- Defect Correction 是否正常

---

# 18. Knowledge Graph

```text
Defect Calibration

↓

Defect Detection

↓

Defect Template

├── Factory Template
├── User Template
└── Active Template

↓

Template Overlay

↓

Calibration Data

↓

Defect Correction

↓

Corrected Image
```

---

# 19. Related Documents

Calibration：

- DefectWorkflow.md
- DefectParameter.md
- DefectFailure.md
- DefectTroubleshooting.md

Theory：

- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationData.md

Software：

- ../../04_Software/iDetector.md

System：

- ../../02_System/ImagePipeline.md

---

# 20. Document Boundary

本文件负责：

- Defect Template 定义
- 生命周期
- Template 分类
- Template 管理
- Upload / Download
- Overlay
- Template 与 Calibration Data 的关系

本文件不负责：

- Defect Detection Algorithm
- 图像插值算法
- SDK API
- 软件界面操作
- 硬件维修

上述内容分别由对应文档说明。

---

# 21. Reference

## Product

- 产品培训资料关于 Defect Template 的生成、查看、修改、上传、下载及管理流程。
- 产品培训资料关于 HW Defect、SW Defect 及 Template Overlay 的实现机制。

## Engineering

- Defect Template 是 Defect Calibration 的核心输出，也是 Defect Correction 的唯一数据来源。
- Template 更新后，应完成版本验证、激活确认及图像验证，确保新的 Calibration Data 已正确生效。