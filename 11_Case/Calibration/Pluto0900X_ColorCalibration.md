# Pluto0900X_ColorCalibration

Version: V1.0

Module: 11_Case / Calibration

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★☆☆☆

Applicable Products:

- Pluto0900X
- Pluto Series（适用版本）

Related Documents:

- ../../05_Calibration/ColorCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/CalibrationFailure.md
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Pluto0900X Color Calibration

## Description

Pluto0900X 在执行 Color Calibration 时，存在一项容易被忽略但影响校准成功率的特殊操作要求。

若操作不当，可能导致彩图校准失败或生成的 Calibration Template 异常。

本案例记录该型号探测器在现场校准中的实际经验。

---

# 2. Applicable Products

适用于：

- Pluto0900X

其它型号是否适用，应依据对应 SDK Release Note 或研发说明确认。

---

# 3. Environment

校准环境要求：

- Detector 工作正常
- SDK 正常连接
- 网络稳定
- 校准流程正常开始

---

# 4. Fault Phenomenon

现场可能出现：

- Color Calibration Failed
- 彩图模板异常
- 校准中断
- Template 无法正常生成

---

# 5. Root Cause Analysis

根据现场经验，该问题并非 Detector 故障，而是 SDK 在 Color Calibration 过程中存在特定处理流程。

SDK 在采集过程中会进行内部计算与校验，如果提前结束曝光，将导致校准数据不完整。

---

# 6. Diagnostic Process

建议按照以下流程确认：

## Step 1

确认使用正确版本的 SDK。

---

## Step 2

开始 Color Calibration。

观察彩图采集进度。

---

## Step 3

当第三组彩图采集至 **第 63 张** 时：

**不要停止曝光。**

继续保持曝光。

---

## Step 4

等待 SDK 自动完成：

**第 64 张图像采集。**

完成内部处理后，再结束曝光。

---

## Step 5

检查：

- Calibration 是否完成
- Template 是否正常生成

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

第三组彩图采集至第 63 张后停止曝光。

### Cause

SDK 尚未完成最后一次内部计算。

### Solution

重新执行 Color Calibration。

等待第 64 张采集结束后再停止曝光。

恢复正常。

---

# 8. Verification

确认：

- Color Calibration 成功完成
- Template 正常生成
- 图像颜色正常
- 无 Calibration Error

---

# 9. Engineering Experience

## Experience 1

根据现场验证：

**第三组彩图采集至第 63 张时，不要停止曝光。**

---

## Experience 2

必须等待：

**SDK 自动采集第 64 张图像。**

随后再结束曝光。

---

## Experience 3

该要求属于当前 Pluto0900X SDK 的操作特性。

若 SDK 或 Firmware 版本更新，应重新验证该经验是否仍适用。

---

# 10. Prevention

建议：

- 校准前培训操作人员
- 按 SDK 完整流程执行
- 不要依据图像数量提前结束曝光
- 校准完成后立即验证 Template

---

# 11. Related Documents

Workflow：

- CalibrationWorkflow.md

Failure Knowledge：

- CalibrationFailure.md

Tools：

- CalibrationTools.md

---

# 12. Source

本案例来源于现场工程经验，适用于当前验证版本的 Pluto0900X SDK。

若后续 SDK 行为发生变化，应及时更新本文档。

---

# 13. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Pluto0900X Color Calibration 案例，记录 SDK 第 63/64 张彩图采集特殊操作要求。 |