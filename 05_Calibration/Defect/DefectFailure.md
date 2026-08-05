# DefectFailure

Version: V2.0

Module: Calibration

Source Level:
- Fact
- Engineering

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectTroubleshooting.md
- ../CalibrationTheory/DefectTheory.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Defect Failure 描述 Defect Calibration 执行过程中可能发生的故障类型、故障表现、可能原因及影响范围。

本文件建立 Defect Calibration 的故障知识体系，为 Troubleshooting、Decision Tree、Failure Knowledge 及现场技术支持提供统一依据。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Failure Definition

Defect Failure 是指 Defect Calibration 无法正常完成，或生成的 Defect Template 无法正确参与图像校正，导致 Defect Correction 失效或图像质量下降。

Failure 可发生于：

- Calibration 启动阶段
- Calibration Image Acquisition
- Defect Detection
- Defect Template Generation
- Template Management
- Calibration Data Update
- Defect Correction

---

# 4. Failure Classification

Defect Failure 可划分为：

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

# 5. Failure Manifestation

可能表现为：

- Defect Calibration Failed
- Calibration Timeout
- Calibration Interrupted
- Defect Template 未生成
- Defect Template 无法加载
- Template Upload Failed
- Template Download Failed
- Template Overlay Failed
- Active Template 未更新
- Defect Correction 无效
- 图像仍存在坏点
- 图像仍存在坏线
- 新增 Defect 未生效
- 图像出现插值异常

---

# 6. Possible Causes

## Detector

- Detector Offline
- Detector Busy
- Detector Initialization Failure
- Detector Hardware Failure

---

## Communication

- Ethernet Disconnect
- Network Timeout
- SDK Communication Failure
- Calibration Command Lost

---

## Calibration Dependency

- Offset Calibration 未完成
- Gain Calibration 未完成
- Calibration Data 不完整
- Calibration Version 不匹配

---

## Calibration Image

- Calibration Image Acquisition Failure
- Image Incomplete
- Image Saturation
- Image Truncation
- Exposure Nonuniform

---

## Defect Detection

- Detection Algorithm Failure
- Threshold Configuration Error
- Pixel Classification Error
- Defect Identification Failure

---

## Template

- Template Generation Failure
- Template Save Failure
- Template Load Failure
- Template Upload Failure
- Template Download Failure
- Template Overlay Failure
- Template Corruption
- Template Version Mismatch
- Active Template Update Failure

---

## Calibration Data

- Calibration Data Write Failure
- Calibration Data Read Failure
- Calibration Data Corruption
- Data Synchronization Failure

---

## Software

- Firmware Exception
- iDetector Exception
- Calibration Process Interrupted
- Template Management Exception

---

# 7. Image Influence

Defect Failure 可能导致：

- Bad Pixel Visible
- Bad Line Visible
- Image Artifact
- Residual Defect
- Interpolation Error
- Image Discontinuity
- Local Bright Pixel
- Local Dark Pixel
- Image Quality Degradation

严重时影响临床图像质量。

---

# 8. Failure Dependency

Defect Failure 与 Calibration 的关系如下：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Failure

↓

Defect Correction

↓

Image Quality
```

Defect Calibration 未完成时，不应启用新的 Defect Template。

---

# 9. Diagnostic Checkpoints

发生 Defect Failure 时，应检查：

- Detector 是否 Online
- Detector 是否 Ready
- Offset Calibration 是否完成
- Gain Calibration 是否完成
- Calibration Image 是否完整
- Defect Detection 是否完成
- Defect Template 是否生成
- Template 是否成功保存
- Template 是否成功上传
- Template 是否成功下载
- Active Template 是否更新
- Calibration Data 是否更新
- Defect Correction 是否正常执行

---

# 10. Failure Severity

| Failure Type | Severity | Image Impact |
|--------------|----------|--------------|
| Detector Offline | Critical | Calibration 无法开始 |
| Calibration Image Failure | Critical | 无法执行 Defect Detection |
| Defect Detection Failure | Critical | 无法识别异常 Pixel |
| Template Generation Failure | High | 无法生成 Defect Template |
| Template Upload Failure | High | 新模板无法生效 |
| Template Overlay Failure | High | Active Template 错误 |
| Calibration Data Update Failure | High | Defect Data 无法使用 |
| Defect Correction Failure | High | 图像仍存在 Defect |
| Template Version Mismatch | Medium | Template 不一致 |
| Residual Defect | Medium | 图像质量下降 |

---

# 11. Relationship with Decision Tree

建议按照以下顺序分析：

```text
Calibration Start

↓

Detector Status

↓

Communication

↓

Offset Status

↓

Gain Status

↓

Calibration Image

↓

Defect Detection

↓

Template Generation

↓

Template Management

↓

Calibration Data

↓

Defect Correction

↓

Image Verification
```

---

# 12. Related Documents

Calibration：

- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectTroubleshooting.md

Theory：

- ../CalibrationTheory/DefectTheory.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 13. Document Boundary

本文件负责：

- Defect Failure 分类
- Failure 表现
- Failure 原因
- Failure 对图像影响
- Failure 检查项

本文件不负责：

- 故障处理步骤
- 软件操作流程
- 参数配置
- SDK API

上述内容由 DefectTroubleshooting.md 说明。

---

# 14. Knowledge Graph

```text
Defect Calibration

↓

Failure

├── Detector
├── Communication
├── Calibration Image
├── Defect Detection
├── Template Generation
├── Template Management
├── Calibration Data
└── Defect Correction

↓

Image Artifact

↓

Troubleshooting
```

---

# 15. Reference

## Fact

- 产品培训资料关于 Defect Calibration、Correction Template、Template Upload/Download、Template Overlay 及模板管理流程。
- 产品用户手册关于 Defect Calibration Failure 的处理要求。

## Engineering

- Defect Failure 应按照 "Detector → Communication → Calibration Dependency → Calibration Image → Defect Detection → Template Management → Calibration Data → Defect Correction → Image Verification" 的顺序进行分析。
- Template 生命周期中的任何异常均可能导致 Defect Correction 失效，因此应优先确认 Active Template 是否正确更新并参与图像处理。