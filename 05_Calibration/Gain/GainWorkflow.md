# GainWorkflow

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
- ../CalibrationTheory/GainTheory.md
- ../Offset/OffsetWorkflow.md
- ../../02_System/ImagePipeline.md
- ../../04_Software/iDetector.md

---

# 1. Purpose

Gain Workflow 描述 Gain Calibration 的标准执行流程。

Gain Calibration 的目标是在均匀 X-Ray 曝光条件下采集 Flat Field Image，建立 Gain Data，对各 Pixel 的响应差异进行补偿，提高图像均匀性。

本文件说明 Gain Calibration 的执行流程，不涉及具体软件界面、算法实现及参数配置。

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

执行 Gain Calibration 前，应确认：

- Detector 工作正常。
- Detector 与主机通信正常。
- Detector 已完成 Initialization。
- Detector 已进入 Ready 状态。
- Offset Calibration 已成功完成。
- X-Ray Generator 工作正常。
- 曝光参数符合产品校准要求。
- Detector 前方无遮挡物。
- X-Ray Beam 能够均匀覆盖整个成像区域。

若上述条件不满足，应停止 Gain Calibration。

---

# 4. Workflow

Gain Calibration 标准流程如下：

```text
Detector Ready

↓

Verify Offset Calibration

↓

Prepare Uniform X-Ray Exposure

↓

Acquire Flat Field Image

↓

Calculate Gain

↓

Generate Gain Data

↓

Store Calibration Data

↓

Calibration Complete
```

---

# 5. Workflow Description

## Step 1

确认 Detector 已进入 Ready 状态。

输出：

Detector Ready。

---

## Step 2

确认 Offset Calibration 已完成。

确认当前 Calibration Data 可正常使用。

---

## Step 3

配置 X-Ray Generator。

保证：

- 曝光参数符合要求。
- X-Ray 覆盖整个 Detector。
- Exposure Field 均匀。

---

## Step 4

执行 Flat Field Exposure。

Detector 采集 Uniform Image。

生成：

Flat Field Image。

---

## Step 5

系统计算每个 Pixel 的 Gain。

生成：

Gain Table。

---

## Step 6

Gain Table 写入 Calibration Data。

替换旧 Gain Data。

---

## Step 7

Calibration 完成。

Detector 返回 Ready 状态。

后续图像均采用新的 Gain Data 进行 Gain Correction。

---

# 6. Workflow Input

Workflow 输入包括：

- Detector Ready
- Offset Data
- Uniform X-Ray
- Flat Field Image

---

# 7. Workflow Output

完成 Gain Calibration 后生成：

- Gain Data
- Gain Table
- Calibration Data Update

上述数据将在图像处理中参与 Gain Correction。

---

# 8. Relationship with Calibration

Gain Calibration 位于 Offset Calibration 之后。

标准执行顺序：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Gain Calibration 不应在 Offset Calibration 未完成时执行。

---

# 9. Relationship with Image Processing

Gain Calibration 不直接生成诊断图像。

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

Gain Correction 用于补偿 Pixel Response 差异，提高图像均匀性。

---

# 10. Abnormal Workflow

以下情况可能导致 Workflow 中断：

- Detector Offline
- Detector Busy
- Offset Calibration Missing
- Exposure Failure
- Flat Field Image Acquisition Failure
- Gain Calculation Failure
- Calibration Data Write Failure
- Calibration Interrupted

发生异常时，应停止 Calibration，并分析故障原因。

---

# 11. Diagnostic Checkpoints

执行 Gain Calibration 时建议确认：

- Detector 是否 Online。
- Detector 是否 Ready。
- Offset Calibration 是否完成。
- 曝光参数是否正确。
- X-Ray 是否均匀覆盖 Detector。
- Flat Field Image 是否正常采集。
- Gain Table 是否成功生成。
- Calibration Data 是否成功更新。

---

# 12. Relationship with Other Documents

Theory：

- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../CalibrationTheory/CalibrationTiming.md

Calibration：

- ../Offset/OffsetWorkflow.md

Software：

- ../../04_Software/iDetector.md

System：

- ../../02_System/ImagePipeline.md

---

# 13. Knowledge Graph

```text
Detector Ready

↓

Offset Calibration Completed

↓

Uniform X-Ray

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Table

↓

Calibration Data

↓

Gain Correction
```

---

# 14. Document Boundary

本文件负责：

- Gain Calibration 执行流程
- Workflow 输入与输出
- Workflow 检查点
- Workflow 执行顺序

本文件不负责：

- Gain 参数说明
- Gain Failure 分析
- Gain Troubleshooting
- Gain SOP
- Gain Algorithm

上述内容分别由对应文档说明。

---

# 15. Reference

## Fact

- 产品培训资料关于 Gain Calibration 执行流程。
- 产品用户手册关于 Calibration 操作流程。

## Theory

- Gain Calibration 在均匀 X-Ray 曝光条件下建立 Gain Data。
- Gain Data 用于补偿 Pixel Response 差异，提高图像均匀性。