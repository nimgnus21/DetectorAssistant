# GainFailure

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
- GainWorkflow.md
- GainParameter.md
- GainTroubleshooting.md
- ../CalibrationTheory/GainTheory.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Gain Failure 描述 Gain Calibration 执行过程中可能发生的异常类型、故障表现、可能原因及影响范围。

本文件用于建立 Gain Calibration 故障知识体系，为 Troubleshooting、Decision Tree、Failure Knowledge 及现场技术支持提供统一依据。

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

Gain Failure 是指 Gain Calibration 无法正常完成，或生成的 Gain Data 无法满足图像均匀性校正要求。

Failure 可发生于：

- Calibration 启动阶段
- 曝光阶段
- Flat Field Image Acquisition
- Gain Calculation
- Calibration Data Generation
- Calibration Data Storage
- Gain Correction

---

# 4. Failure Classification

Gain Failure 可划分为：

- Calibration Start Failure
- Exposure Failure
- Flat Field Image Acquisition Failure
- Gain Calculation Failure
- Gain Data Generation Failure
- Calibration Data Storage Failure
- Gain Correction Failure

---

# 5. Failure Manifestation

可能表现为：

- Gain Calibration Failed
- Calibration Timeout
- Calibration Interrupted
- Gain Data 未更新
- Calibration Success 但图像异常
- 图像亮度不均
- 局部亮区
- 局部暗区
- Fixed Pattern Noise
- Nonuniform Image

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

## Offset Calibration

- Offset Calibration 未完成
- Offset Data 无效
- Offset Data 与 Detector 不匹配

---

## Exposure

- X-Ray Generator 异常
- 曝光剂量不足
- 曝光剂量过高
- Beam 覆盖不足
- Beam 不均匀

---

## Image Acquisition

- Flat Field Image Acquisition Failure
- Image Data Incomplete
- Image Saturation
- Image Truncation

---

## Calculation

- Gain Calculation Failure
- Gain Table Generation Failure
- Algorithm Exception

---

## Calibration Data

- Gain Data Write Failure
- Gain Data Read Failure
- Calibration Data Corruption
- Calibration Data Version Mismatch

---

## Software

- Firmware Exception
- iDetector Exception
- Calibration Process Interrupted

---

# 7. Image Influence

Gain Failure 可能导致：

- Image Nonuniformity
- Bright Area
- Dark Area
- Response Difference
- Residual Grid Pattern
- Contrast Degradation
- Image Artifact

严重时影响 Defect Calibration。

---

# 8. Failure Dependency

Gain Failure 与 Calibration 的关系如下：

```text
Offset Calibration

↓

Gain Failure

↓

Defect Calibration

↓

Image Quality
```

Gain Calibration 未完成时，不建议继续执行 Defect Calibration。

---

# 9. Diagnostic Checkpoints

发生 Gain Failure 时，应检查：

- Detector 是否 Online
- Detector 是否 Ready
- Offset Calibration 是否成功
- Exposure 是否正常
- Flat Field Image 是否完整
- Gain Calculation 是否完成
- Gain Table 是否生成
- Calibration Data 是否更新

---

# 10. Failure Severity

| Failure Type | Severity | Image Impact |
|--------------|----------|--------------|
| Detector Offline | Critical | Calibration 无法开始 |
| Exposure Failure | Critical | 无法建立 Gain Data |
| Flat Field Acquisition Failure | Critical | 无法完成计算 |
| Gain Calculation Failure | High | Gain Table 无法生成 |
| Calibration Data Write Failure | High | Gain Data 无法使用 |
| Gain Correction Failure | High | 图像均匀性下降 |
| Bright/Dark Area | Medium | 图像质量下降 |

---

# 11. Relationship with Decision Tree

建议按照以下顺序分析：

```text
Calibration Start

↓

Detector Status

↓

Offset Status

↓

Exposure

↓

Flat Field Image

↓

Gain Calculation

↓

Calibration Data

↓

Image Result
```

---

# 12. Related Documents

Calibration：

- GainWorkflow.md
- GainParameter.md
- GainTroubleshooting.md

Theory：

- ../CalibrationTheory/GainTheory.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 13. Document Boundary

本文件负责：

- Gain Failure 分类
- Failure 表现
- Failure 原因
- Failure 对图像影响
- Failure 检查项

本文件不负责：

- 故障处理步骤
- 软件操作流程
- 参数配置
- API 调用

上述内容由 GainTroubleshooting.md 说明。

---

# 14. Knowledge Graph

```text
Gain Calibration

↓

Failure

├── Detector

├── Communication

├── Offset Status

├── Exposure

├── Flat Field Image

├── Calculation

├── Calibration Data

└── Gain Correction

↓

Image Artifact

↓

Troubleshooting
```

---

# 15. Reference

## Fact

- 产品培训资料关于 Gain Calibration 流程及异常处理。
- 产品用户手册关于 Calibration Failure 的处理要求。

## Engineering

- Gain Failure 应按照 Detector → Communication → Offset → Exposure → Image Acquisition → Calculation → Calibration Data → Image Result 的顺序进行分析。