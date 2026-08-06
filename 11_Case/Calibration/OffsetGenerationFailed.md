# OffsetGenerationFailed

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

- ../../05_Calibration/OffsetCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/OffsetFailure.md
- ../../09_DecisionTree/Calibration/OffsetFailure.md
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Offset Generation Failed

## Description

在执行 Offset Calibration 时，SDK 无法正常生成 Offset Template，导致校准流程终止或模板无效。

Offset Generation Failed 是现场较常见的校准类问题，其原因既可能来自探测器状态，也可能来自采集环境、网络通信或配置错误。

---

# 2. Applicable Products

适用于：

- 静态平板探测器
- 动态平板探测器
- Pluto 系列
- 使用 SDK_AIO 的产品

---

# 3. Environment

典型校准流程：

```text
Detector

↓

Dark Image Acquisition

↓

Offset Calculation

↓

Offset Template

↓

Save
```

Offset 校准要求：

- 无 X-Ray 曝光
- 环境稳定
- Detector 正常工作
- 网络通信稳定

---

# 4. Fault Phenomenon

现场常见表现：

- Offset Generation Failed
- Generate Offset Failed
- Offset Template Save Failed
- Calibration Failed
- SDK 提示 Offset Error
- Offset Template 无法加载

部分情况下还可能伴随：

- Image Loss
- Timeout
- Acquisition Failed

---

# 5. Root Cause Analysis

## 5.1 Detector 状态异常

包括：

- Detector 未完成初始化
- Detector Busy
- Detector 通信异常

---

## 5.2 网络传输异常

包括：

- Image Loss
- Timeout
- 网络丢包

导致 Offset 图像采集不完整。

---

## 5.3 环境条件不满足

包括：

- 存在 X-Ray 曝光
- 环境光干扰（适用于特定产品）
- Detector 温度不稳定

导致暗场数据异常。

---

## 5.4 校准参数配置错误

包括：

- ROI 配置错误
- Mode 配置错误
- PGA 配置不匹配

导致 Offset 无法正常生成。

---

## 5.5 存储异常

包括：

- 保存路径无权限
- 存储空间不足
- Template 文件损坏

导致生成完成但无法保存。

---

# 6. Diagnostic Process

建议按照以下顺序排查：

---

## Step 1

确认 Detector 状态。

检查：

- Detector Online
- Firmware 正常
- SDK 已连接

---

## Step 2

确认采集环境。

检查：

- 无 X-Ray 曝光
- 环境稳定
- Detector 已预热（如产品要求）

---

## Step 3

检查网络状态。

重点确认：

- 是否出现 Image Loss
- 是否存在 Timeout
- 网络是否稳定

---

## Step 4

检查校准参数。

确认：

- ROI
- Mode
- PGA

是否符合当前 Detector 配置。

---

## Step 5

检查存储位置。

确认：

- Template 保存路径有效
- 磁盘空间充足
- 文件权限正常

---

## Step 6

重新执行 Offset Calibration。

若仍失败：

导出 SDK Log，并记录：

- Firmware Version
- SDK Version
- Detector SN
- 操作步骤

提交研发分析。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Offset Generation Failed。

### Cause

采集过程中发生 Image Loss。

### Solution

恢复网络配置。

重新执行 Offset Calibration。

恢复正常。

---

## Case 2

### Phenomenon

Offset Template 无法生成。

### Cause

ROI 配置错误。

### Solution

恢复正确 ROI。

重新校准。

---

## Case 3

### Phenomenon

Offset Save Failed。

### Cause

Template 保存路径异常。

### Solution

修改保存路径。

重新生成 Template。

---

# 8. Verification

满足以下条件：

- Offset Template 成功生成
- Template 可正常加载
- 图像采集正常
- 无 Offset Error
- 后续 Gain Calibration 可继续执行

即可确认问题解决。

---

# 9. Engineering Experience

## Experience 1

Offset Generation Failed 时，不要立即怀疑 Detector。

优先检查：

- 网络状态
- Image Loss
- Timeout

因为采集过程中任何丢帧都可能导致 Offset 失败。

---

## Experience 2

若同时出现：

- Offset Generation Failed
- Image Loss

建议首先恢复网络通信，再重新执行校准。

---

## Experience 3

修改 ROI、Mode 或 PGA 后，应重新验证 Offset Template 是否仍然适用。

不要直接复用旧模板。

---

## Experience 4

重新校准成功后，建议立即备份 Offset Template，避免后续模板损坏或误覆盖。

---

# 10. Prevention

建议：

- 校准前确认 Detector 状态正常
- 校准期间保持网络稳定
- 避免任何曝光干扰
- 修改参数后重新执行 Offset Calibration
- 定期备份 Offset Template

---

# 11. Related Documents

Workflow：

- CalibrationWorkflow.md

Failure Knowledge：

- OffsetFailure.md

Decision Tree：

- OffsetFailure.md

Tools：

- CalibrationTools.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Offset Generation Failed 现场案例及排查经验。 |