# OffsetFailure

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
- OffsetWorkflow.md
- OffsetParameter.md
- OffsetTroubleshooting.md
- ../CalibrationTheory/OffsetTheory.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Offset Failure 描述 Offset Calibration 执行过程中可能发生的异常类型、故障表现、可能原因及影响范围。

本文件用于建立 Offset Calibration 故障知识体系，为 Troubleshooting、Decision Tree 及现场售后提供技术依据。

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

Offset Failure 是指 Offset Calibration 无法正常完成，或生成的 Offset Data 无法满足图像校正要求。

Failure 可发生于：

- Calibration 启动阶段
- 图像采集阶段
- 数据计算阶段
- 数据保存阶段
- 图像校正阶段

---

# 4. Failure Classification

Offset Failure 可划分为：

- Calibration Start Failure
- Dark Image Acquisition Failure
- Offset Calculation Failure
- Calibration Data Generation Failure
- Calibration Data Storage Failure
- Offset Correction Failure

---

# 5. Failure Manifestation

可能表现为：

- Offset Calibration Failed
- Calibration 中断
- Calibration 超时
- Calibration Success 但图像异常
- Offset Data 未更新
- 图像背景异常
- 固定纹理
- 图像整体偏亮
- 图像整体偏暗

---

# 6. Possible Causes

## Detector

- Detector 未完成初始化
- Detector Busy
- Detector Offline
- Detector 内部异常

---

## Communication

- Network Disconnect
- Command Transmission Failure
- Calibration Command Lost

---

## Exposure Condition

- Offset Calibration 过程中存在 X-Ray 曝光
- 杂散射线进入 Detector
- Detector 前方存在遮挡

---

## Image Acquisition

- Dark Image Acquisition Failure
- Image Data Incomplete
- Acquisition Interrupted

---

## Calculation

- Offset Calculation Failure
- Pixel Offset Calculation Error
- Calibration Algorithm Execution Failure

---

## Data

- Offset Table Generation Failure
- Calibration Data Write Failure
- Calibration Data Read Failure
- Calibration Data Corruption

---

## Software

- Software Exception
- Firmware Exception
- Calibration Process Interrupted

---

# 7. Image Influence

Offset Failure 可能导致：

- Fixed Pattern Noise
- Background Offset
- Background Nonuniformity
- Bright Background
- Dark Background
- Contrast Reduction

严重时影响后续 Gain Calibration 与 Defect Calibration。

---

# 8. Failure Dependency

Offset Failure 会影响：

```text
Offset Failure

↓

Gain Calibration

↓

Defect Calibration

↓

Image Quality
```

Offset Calibration 未成功完成时，不建议继续执行后续 Calibration。

---

# 9. Diagnostic Checkpoints

发生 Offset Failure 时，应检查：

- Detector 是否 Online
- Detector 是否 Ready
- 是否存在 X-Ray 曝光
- Dark Image 是否采集成功
- Offset Calculation 是否完成
- Offset Table 是否生成
- Calibration Data 是否写入成功
- Calibration 是否正常结束

---

# 10. Failure Severity

| Failure Type | Severity | Image Impact |
|--------------|----------|--------------|
| Detector Offline | Critical | Calibration 无法开始 |
| Dark Image Acquisition Failure | Critical | 无法计算 Offset |
| Offset Calculation Failure | High | Offset Data 无法生成 |
| Calibration Data Write Failure | High | 新数据无法使用 |
| Offset Correction Failure | High | 图像背景异常 |
| Background Nonuniformity | Medium | 图像质量下降 |

---

# 11. Relationship with Decision Tree

Decision Tree 推荐排查顺序：

```text
Calibration Start

↓

Detector Status

↓

Communication

↓

Dark Image

↓

Offset Calculation

↓

Calibration Data

↓

Image Result
```

---

# 12. Related Documents

Calibration：

- OffsetWorkflow.md
- OffsetParameter.md
- OffsetTroubleshooting.md

Theory：

- ../CalibrationTheory/OffsetTheory.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 13. Document Boundary

本文件负责：

- Offset Failure 分类
- Failure 表现
- Failure 原因
- Failure 对图像影响
- Failure 检查项

本文件不负责：

- 故障处理步骤
- SOP
- 软件操作
- 参数配置
- API 调用

上述内容由 OffsetTroubleshooting.md 进行说明。

---

# 14. Knowledge Graph

```text
Offset Calibration

↓

Failure

├── Detector

├── Communication

├── Dark Image

├── Calculation

├── Calibration Data

└── Correction

↓

Image Artifact

↓

Troubleshooting
```

---

# 15. Reference

## Fact

- 产品培训资料关于 Offset Calibration 流程及异常处理。
- 产品用户手册关于 Calibration Failure 的基本处理要求。

## Engineering

- Offset Failure 应按照 Detector → Communication → Image Acquisition → Calculation → Data → Image Result 的顺序进行分析。