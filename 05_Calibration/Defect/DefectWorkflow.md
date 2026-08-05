# DefectWorkflow

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
- ../CalibrationTheory/DefectTheory.md
- ../Offset/OffsetWorkflow.md
- ../Gain/GainWorkflow.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Defect Workflow 描述 Defect Calibration 的标准执行流程。

Defect Calibration 的目标是识别 Detector 中响应异常的 Pixel，并建立 Defect Data，为后续图像处理中的 Defect Correction 提供基础数据。

本文件说明 Defect Calibration 的执行流程，不涉及具体软件界面、算法实现及参数配置。

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

执行 Defect Calibration 前，应确认：

- Detector 工作正常。
- Detector 与主机通信正常。
- Detector 已完成 Initialization。
- Detector 已进入 Ready 状态。
- Offset Calibration 已完成。
- Gain Calibration 已完成。
- Calibration Data 正常。
- X-Ray Generator 工作正常。
- 曝光参数符合产品要求。
- Detector 成像区域无遮挡。

若上述条件不满足，应停止 Defect Calibration。

---

# 4. Workflow

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

Detect Defect Pixel

↓

Generate Defect Map

↓

Update Calibration Data

↓

Calibration Complete
```

---

# 5. Workflow Description

## Step 1

确认 Detector 已进入 Ready 状态。

---

## Step 2

确认 Offset Calibration 已完成。

Offset Data 正常可用。

---

## Step 3

确认 Gain Calibration 已完成。

Gain Data 正常可用。

---

## Step 4

系统采集 Calibration Image。

采集图像用于分析 Pixel Response。

---

## Step 5

系统分析所有 Pixel 的响应状态。

识别异常 Pixel。

生成：

- Defect Pixel List
- Defect Map

---

## Step 6

更新 Calibration Data。

写入：

- Defect Data
- Defect Map

替换旧版本数据。

---

## Step 7

Calibration 完成。

Detector 返回 Ready 状态。

后续图像处理开始使用新的 Defect Data。

---

# 6. Workflow Input

Workflow 输入包括：

- Detector Ready
- Offset Data
- Gain Data
- Calibration Image

---

# 7. Workflow Output

Defect Calibration 输出：

- Defect Data
- Defect Map
- Calibration Data Update

上述数据将在 Image Processing 中参与 Defect Correction。

---

# 8. Relationship with Calibration

Defect Calibration 位于 Calibration 最后一阶段。

执行顺序：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Defect Calibration 建立在 Offset 与 Gain Calibration 完成之后。

---

# 9. Relationship with Image Processing

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

Defect Correction 用于补偿异常 Pixel，提高图像连续性。

---

# 10. Abnormal Workflow

以下情况可能导致 Workflow 中断：

- Detector Offline
- Detector Busy
- Offset Calibration Missing
- Gain Calibration Missing
- Calibration Image Acquisition Failure
- Defect Detection Failure
- Defect Map Generation Failure
- Calibration Data Write Failure
- Calibration Interrupted

发生异常时，应停止 Calibration，并分析故障原因。

---

# 11. Diagnostic Checkpoints

执行 Defect Calibration 时建议确认：

- Detector 是否 Online。
- Detector 是否 Ready。
- Offset Calibration 是否完成。
- Gain Calibration 是否完成。
- Calibration Image 是否完整。
- Defect Detection 是否完成。
- Defect Map 是否生成。
- Calibration Data 是否成功更新。

---

# 12. Relationship with Other Documents

Theory：

- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationTiming.md

Calibration：

- ../Offset/OffsetWorkflow.md
- ../Gain/GainWorkflow.md

Software：

- ../../04_Software/iDetector.md

System：

- ../../02_System/ImagePipeline.md

---

# 13. Knowledge Graph

```text
Detector Ready

↓

Offset Completed

↓

Gain Completed

↓

Calibration Image

↓

Defect Detection

↓

Defect Map

↓

Calibration Data

↓

Defect Correction
```

---

# 14. Document Boundary

本文件负责：

- Defect Calibration 执行流程
- Workflow 输入与输出
- Workflow 检查点
- Workflow 执行顺序

本文件不负责：

- Defect 参数说明
- Defect Failure 分析
- Defect Troubleshooting
- Defect SOP
- Defect Detection Algorithm

上述内容分别由对应文档说明。

---

# 15. Reference

## Fact

- 产品培训资料关于 Defect Calibration 执行流程。
- 产品用户手册关于 Calibration 操作流程。

## Theory

- Defect Calibration 用于识别异常 Pixel 并建立 Defect Data。
- Defect Data 在图像处理中用于 Defect Correction，提高图像连续性与完整性。