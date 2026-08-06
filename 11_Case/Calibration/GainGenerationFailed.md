# GainGenerationFailed

Version: V1.0

Module: 11_Case / Calibration

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series
- SDK_AIO Platform

Related Documents:

- ../../05_Calibration/GainCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/GainFailure.md
- ../../09_DecisionTree/Calibration/GainFailure.md
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Gain Generation Failed

## Description

在执行 Gain Calibration 时，SDK 无法正常生成 Gain Template，导致平场校准失败或模板无法使用。

Gain Calibration 用于补偿各像素响应一致性，是保证图像均匀性的关键步骤。

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
X-Ray

↓

Flat Field Image

↓

Gain Calculation

↓

Gain Template

↓

Save
```

Gain 校准要求：

- X-Ray 输出稳定
- 平场均匀
- Detector 状态正常
- Offset 已完成

---

# 4. Fault Phenomenon

现场常见表现：

- Gain Generation Failed
- Generate Gain Failed
- Gain Template Save Failed
- Calibration Failed
- Gain Template Invalid
- 图像亮度不均匀

部分情况下还可能伴随：

- Image Loss
- Offset Generation Failed
- Defect Generation Failed

---

# 5. Root Cause Analysis

## 5.1 Flat Field 不均匀

包括：

- 射线照射不均
- 遮挡
- SID 不符合要求
- 准直器未完全打开

导致 Gain 计算异常。

---

## 5.2 X-Ray 输出不稳定

包括：

- 剂量波动
- 曝光时间不稳定
- 管电压异常

导致 Gain 数据不一致。

---

## 5.3 Detector 状态异常

包括：

- Detector Busy
- Detector 未初始化
- 通信异常

---

## 5.4 网络异常

包括：

- Image Loss
- Timeout
- 丢包

导致 Gain 图像采集不完整。

---

## 5.5 参数配置错误

包括：

- ROI
- PGA
- Mode

与当前 Detector 配置不一致。

---

## 5.6 Offset 未完成

若 Offset Template 无效或未加载：

可能直接导致 Gain Generation Failed。

---

# 6. Diagnostic Process

建议按照以下顺序排查：

---

## Step 1

确认 Offset Calibration 已成功完成。

检查：

- Offset Template 是否存在
- 是否正确加载

---

## Step 2

检查 Flat Field。

确认：

- 无遮挡
- 光场均匀
- Detector 完全覆盖照射区域

---

## Step 3

检查 X-Ray 输出。

确认：

- kV、mA、ms 稳定
- 曝光重复性良好

---

## Step 4

检查 Detector 状态。

确认：

- Detector Online
- SDK 正常连接

---

## Step 5

检查网络状态。

重点确认：

- 是否发生 Image Loss
- 是否存在 Timeout

---

## Step 6

检查参数配置。

确认：

- ROI
- PGA
- Mode

与当前校准要求一致。

---

## Step 7

重新执行 Gain Calibration。

若仍失败：

导出：

- SDK Log
- Calibration Log

提交研发分析。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Gain Generation Failed。

### Cause

Flat Field 存在遮挡。

### Solution

重新布置平场。

重新校准。

---

## Case 2

### Phenomenon

Gain Template 无法生成。

### Cause

Offset Template 未正确加载。

### Solution

重新执行 Offset Calibration。

随后重新生成 Gain。

---

## Case 3

### Phenomenon

Gain 校准过程中中断。

### Cause

Image Loss。

### Solution

恢复网络配置。

重新执行 Gain Calibration。

---

# 8. Verification

确认：

- Gain Template 成功生成
- 图像均匀性恢复
- 无 Gain Error
- 后续 Defect Calibration 可正常进行

---

# 9. Engineering Experience

## Experience 1

Gain 校准前必须确认 Offset 已完成且模板有效。

---

## Experience 2

Gain Calibration 对 Flat Field 要求极高。

即使轻微遮挡，也可能导致模板失效。

---

## Experience 3

若 ROI、PGA、Binning 保持一致，

多个 Mode 通常可以共用 Gain Template。

（适用性需结合具体产品验证。）

---

## Experience 4

Gain 校准完成后，建议立即进行图像均匀性验证，而不要直接交付使用。

---

# 10. Prevention

建议：

- 使用稳定 X-Ray 输出
- 保持 Flat Field 均匀
- 校准前完成 Offset
- 修改 ROI、PGA 或 Mode 后重新验证 Gain
- 定期备份 Gain Template

---

# 11. Related Documents

Workflow：

- CalibrationWorkflow.md

Failure Knowledge：

- GainFailure.md

Decision Tree：

- GainFailure.md

Tools：

- CalibrationTools.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Gain Generation Failed 现场案例及排查经验。 |