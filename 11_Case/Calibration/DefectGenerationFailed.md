# DefectGenerationFailed

Version: V1.0

Module: 11_Case / Calibration

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series
- SDK_AIO Platform

Related Documents:

- ../../05_Calibration/DefectCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/DefectFailure.md
- ../../09_DecisionTree/Calibration/DefectFailure.md
- ../../17_Tools/SDKTool/CalibrationTools.md
- ../../17_Tools/SDKTool/DTDITool.md

---

# 1. Case Summary

## Case Name

Defect Generation Failed

## Description

执行 Defect Calibration 时，SDK 无法正常生成 Defect Template，或生成后的 Template 无法正常使用，导致坏点校正失败。

Defect Calibration 是校准流程的最后一步，其结果直接影响图像中的坏点、坏线及异常像素修正效果。

---

# 2. Applicable Products

适用于：

- Static Detector
- Dynamic Detector
- Pluto Series
- SDK_AIO Platform

---

# 3. Environment

典型流程：

```text
Offset Template

↓

Gain Template

↓

Acquire Image

↓

Defect Detection

↓

Generate Defect Template

↓

Save
```

Defect Calibration 前提：

- Offset 已完成
- Gain 已完成
- Detector 工作正常
- 图像采集正常

---

# 4. Fault Phenomenon

现场常见表现：

- Defect Generation Failed
- Generate Defect Failed
- Defect Template Invalid
- Template Save Failed
- Defect Correction Failed

同时可能出现：

- Image Loss
- Offset Generation Failed
- Gain Generation Failed
- 图像坏点数量异常
- 图像存在坏线

---

# 5. Root Cause Analysis

## 5.1 Offset / Gain Template 异常

包括：

- Offset 未完成
- Gain 未完成
- Template 已损坏
- Template 与当前 Mode 不匹配

Defect Calibration 建立在 Offset 与 Gain 校准基础之上，前置模板异常将直接影响 Defect 结果。

---

## 5.2 图像质量异常

包括：

- Image Loss
- Noise 过高
- 曝光异常
- 图像存在拖影

导致坏点识别结果失真。

---

## 5.3 Detector 状态异常

包括：

- Detector Busy
- 通信异常
- Firmware 异常

导致采图失败或数据异常。

---

## 5.4 参数配置错误

包括：

- ROI 配置错误
- Mode 配置错误
- PGA 配置不一致

导致 Template 不可用。

---

## 5.5 Template 保存失败

包括：

- 保存路径错误
- 权限不足
- 存储空间不足

---

# 6. Diagnostic Process

建议按照以下顺序排查：

---

## Step 1

确认 Offset Calibration 已完成。

检查：

- Offset Template 存在
- Offset Template 已加载

---

## Step 2

确认 Gain Calibration 已完成。

检查：

- Gain Template 存在
- Gain Template 已加载

---

## Step 3

检查图像质量。

确认：

- 无明显 Noise
- 无 Image Loss
- 无 Timeout
- 图像完整

---

## Step 4

检查 Detector 状态。

确认：

- Detector Online
- Firmware 正常
- SDK 正常通信

---

## Step 5

检查配置参数。

确认：

- ROI
- Mode
- PGA

与当前 Detector 一致。

---

## Step 6

重新执行 Defect Calibration。

若仍失败：

导出：

- SDK Log
- Calibration Log
- 原始 RAW

提交研发分析。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Defect Generation Failed。

### Cause

Gain Template 未正确加载。

### Solution

重新加载 Gain Template。

重新执行 Defect Calibration。

---

## Case 2

### Phenomenon

生成大量坏点。

### Cause

采集图像 Noise 过高。

### Solution

排除噪声来源。

重新采集。

重新生成 Template。

---

## Case 3

### Phenomenon

Defect Template 无法保存。

### Cause

保存路径权限不足。

### Solution

修改保存路径。

重新生成。

---

## Case 4

### Phenomenon

动态图像仍存在坏线。

### Cause

Defect Template 未更新。

### Solution

重新执行 Defect Calibration。

必要时使用工具手动添加坏点或换线信息。

---

# 8. Verification

确认：

- Defect Template 成功生成
- Template 可正常加载
- 图像坏点得到修正
- 无明显坏线
- 图像质量符合要求

即可确认问题解决。

---

# 9. Engineering Experience

## Experience 1

Defect Calibration 必须建立在有效的 Offset 与 Gain Template 基础上。

不要跳过前置校准。

---

## Experience 2

现场培训经验：

多个 Mode 在 **ROI、PGA、Binning 等参数一致**时，可共用同一份 Gain 与 Defect Template。

更换上述参数后，应重新验证模板适用性。

---

## Experience 3

对于少量新增坏点或坏线，

可使用软件工具**手动添加坏点/换线信息**到 Defect Template，而无需重新进行完整校准。

---

## Experience 4

动态平板使用 DTDITool 处理图像时，应优先确认使用的是当前版本对应的 Defect Template，避免因模板版本不一致造成图像异常。

---

# 10. Prevention

建议：

- 严格按照 Offset → Gain → Defect 顺序执行校准
- 保持采集环境稳定
- 使用正确版本的 Template
- 定期备份 Defect Template
- Detector 更换 Firmware 或关键参数后重新验证 Template

---

# 11. Related Documents

Workflow：

- CalibrationWorkflow.md

Failure Knowledge：

- DefectFailure.md

Decision Tree：

- DefectFailure.md

Tools：

- CalibrationTools.md
- DTDITool.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Defect Generation Failed 现场案例及排查经验。 |