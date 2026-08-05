# OffsetWorkflow

Version: V2.0

Module: Calibration

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- ../CalibrationTheory/CalibrationOverview.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationTiming.md
- ../CalibrationTheory/OffsetTheory.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Offset Workflow 描述 Offset Calibration 的标准执行流程。

Offset Calibration 的目标是在无 X-Ray 曝光条件下采集 Dark Image，建立 Offset Data，为后续图像处理提供 Offset Correction 数据。

本文件说明 Offset Calibration 的执行流程，不涉及具体软件界面及参数设置。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Preconditions

执行 Offset Calibration 前，应确认：

- Detector 工作正常。
- Detector 与主机通信正常。
- 系统初始化完成。
- 当前 Detector 已进入 Ready 状态。
- X-Ray Generator 不进行曝光。
- Detector 前方无遮挡且无杂散 X-Ray。

若上述条件不满足，应停止 Calibration。

---

# 4. Workflow

Offset Calibration 标准流程如下：

```text
Detector Ready

↓

Confirm No X-Ray

↓

Acquire Dark Image

↓

Calculate Offset

↓

Generate Offset Data

↓

Store Calibration Data

↓

Calibration Complete
```

---

# 5. Workflow Description

## Step 1

确认 Detector 已完成初始化。

输出：

Detector Ready。

---

## Step 2

确认当前无 X-Ray 曝光。

目的：

保证采集到纯 Dark Image。

---

## Step 3

系统采集 Dark Image。

采集过程中：

Pixel 完成一次完整读出。

生成 Dark Image。

---

## Step 4

系统计算每个 Pixel 的 Offset。

生成：

Offset Table。

---

## Step 5

Offset Table 写入 Calibration Data。

替换旧 Offset Data。

---

## Step 6

Calibration 完成。

Detector 返回 Ready 状态。

后续所有图像均使用新的 Offset Data。

---

# 6. Workflow Output

完成 Offset Calibration 后生成：

- Offset Data
- Calibration Data Update

后续图像处理开始使用新的 Offset Correction。

---

# 7. Relationship with Calibration

Offset Calibration 是整个 Calibration 的第一步。

执行顺序：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Offset Calibration 未完成时，不建议继续执行后续 Calibration。

---

# 8. Relationship with Image Processing

Offset Workflow 不直接生成诊断图像。

Calibration 完成后：

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

Offset Correction 为第一步图像校正。

---

# 9. Abnormal Workflow

以下情况可能导致 Offset Workflow 中断：

- Detector Offline
- Communication Failure
- Calibration Interrupted
- Detector Busy
- Calibration Data Write Failure

出现异常时，应停止 Calibration，并分析具体故障原因。

---

# 10. Diagnostic Checkpoints

执行 Offset Calibration 时建议确认：

- Detector 是否 Online。
- Detector 是否 Ready。
- 当前是否存在 X-Ray 曝光。
- Dark Image 是否正常采集。
- Offset Data 是否成功生成。
- Calibration Data 是否成功保存。

---

# 11. Related Documents

Theory：

- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationTiming.md

Software：

- ../../04_Software/iDetector.md

System：

- ../../02_System/ImagePipeline.md

---

# 12. Knowledge Graph

```text
Detector Ready

↓

No X-Ray

↓

Dark Image

↓

Offset Calculation

↓

Offset Data

↓

Calibration Data

↓

Image Correction
```

---

# 13. Document Boundary

本文件负责：

- Offset Calibration 执行流程
- Workflow 各阶段说明
- Workflow 输出
- Workflow 检查点

本文件不负责：

- Offset 参数说明
- Offset Failure 分析
- Offset Troubleshooting
- Offset SOP

上述内容分别由对应文档说明。

---

# 14. Reference

## Fact

- 产品培训资料关于 Offset Calibration 执行流程。
- 产品用户手册关于 Calibration 操作流程。

## Theory

- Offset Workflow 是 Offset Calibration 的标准执行过程。
- Offset Calibration 完成后生成新的 Offset Data，并参与后续图像处理。