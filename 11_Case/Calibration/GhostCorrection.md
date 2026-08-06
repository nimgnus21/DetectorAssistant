# GhostCorrection

Version: V1.0

Module: 11_Case / Calibration

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series Dynamic Detector
- SDK_AIO Platform

Related Documents:

- ../../05_Calibration/DynamicCalibration.md
- ../../06_Workflow/DynamicCorrectionWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/GhostFailure.md
- ../../08_ImageDiagnosis/GhostArtifact/
- ../../09_DecisionTree/Calibration/GhostCorrection.md
- ../../13_Principles/DynamicDetector/
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Ghost Correction Failed

## Description

执行 Ghost Correction（残影校正）后，图像仍存在上一帧残留影像，或 Ghost Template 无法正常生成，导致动态图像质量下降。

Ghost Correction 是动态平板的重要校准流程，其目的是降低连续曝光过程中残余图像对后续图像的影响。

---

# 2. Applicable Products

适用于：

- Dynamic Flat Panel Detector
- Pluto 系列动态探测器
- 支持 Ghost Correction 的动态模式

---

# 3. Environment

典型流程：

```text
Detector Initialization

↓

Mode Configuration

↓

Offset Calibration

↓

Ghost Calibration

↓

Generate Ghost Template

↓

Dynamic Acquisition

↓

Ghost Correction
```

Ghost Correction 通常应用于连续采集模式。

---

# 4. Fault Phenomenon

现场常见表现：

- 图像存在上一帧残影
- 高密度区域出现轮廓残留
- 连续动态图像拖尾
- Ghost Correction Failed
- Ghost Template 无法生成
- Ghost 校正效果不明显

---

# 5. Root Cause Analysis

## 5.1 Ghost Calibration 未执行

动态模式未建立 Ghost Template。

导致动态图像无法进行 Ghost Correction。

---

## 5.2 Mode 配置错误

Ghost Correction 依赖对应 Mode。

包括：

- Mode 参数错误
- Dynamic Mode 配置错误
- ROI 不一致

---

## 5.3 Swap Mode 配置异常

培训资料指出：

Ghost Correction 通常结合 **132（Swap Mode）** 使用。

Swap Mode 可通过两次曝光采集：

- Pre-offset
- Post-offset

用于降低残影影响。

若 Swap Mode 配置错误：

Ghost 校正效果将明显下降。

---

## 5.4 Detector 工作状态异常

包括：

- Detector Busy
- Detector Reset
- Firmware 异常

导致 Ghost 数据采集失败。

---

## 5.5 图像采集异常

包括：

- Image Loss
- Timeout
- 网络丢包

导致 Ghost Template 数据不完整。

---

# 6. Diagnostic Process

建议按照以下顺序排查：

---

## Step 1

确认 Detector 工作模式。

检查：

- 当前是否为动态模式
- 当前 Mode 是否支持 Ghost Correction

---

## Step 2

检查 Ghost Calibration。

确认：

- Ghost Template 是否生成
- 是否正确加载

---

## Step 3

检查 Mode Configuration。

确认：

- ROI
- Frame Rate
- Exposure Mode
- Trigger 配置

与当前模板一致。

---

## Step 4

检查 Swap Mode。

确认：

- 是否启用 Mode132
- Pre-offset / Post-offset 是否正常执行

---

## Step 5

检查网络状态。

确认：

- 无 Image Loss
- 无 Timeout
- 图像采集完整

---

## Step 6

重新执行 Ghost Calibration。

若仍失败：

导出：

- SDK Log
- Calibration Log
- Dynamic RAW

提交研发分析。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Ghost 校正后仍存在明显残影。

### Cause

Ghost Template 未正确加载。

### Solution

重新加载 Ghost Template。

重新验证动态图像。

---

## Case 2

### Phenomenon

Ghost Correction Failed。

### Cause

Mode 参数修改后仍使用旧 Template。

### Solution

重新执行 Ghost Calibration。

生成新的 Ghost Template。

---

## Case 3

### Phenomenon

动态图像持续拖尾。

### Cause

Swap Mode 未正确配置。

### Solution

重新检查 Mode132 配置。

重新采集 Ghost Calibration 数据。

---

## Case 4

### Phenomenon

Ghost 校正偶尔失效。

### Cause

采集过程中发生 Image Loss。

### Solution

恢复网络通信。

重新执行 Ghost Calibration。

---

# 8. Verification

确认：

- Ghost Template 成功生成
- Template 正常加载
- 连续动态图像无明显残影
- 图像拖尾明显改善
- 连续采集稳定

即可确认问题解决。

---

# 9. Engineering Experience

## Experience 1

Ghost Calibration 仅适用于支持动态校正的产品。

静态探测器通常无需执行该流程。

---

## Experience 2

根据培训资料：

Mode132（Swap Mode）通过两次曝光采集 Pre-offset 或 Post-offset，可有效降低残影影响。

若相关配置异常，应优先检查 Mode 设置，而不是直接判断 Detector 故障。

---

## Experience 3

Ghost 与 Lag 容易混淆。

Ghost Correction 只能降低 Ghost Artifact。

若图像异常由 Lag 引起，应进一步分析读出电路、材料特性或曝光条件，而不能仅依赖 Ghost 校正。

---

## Experience 4

Ghost Calibration 完成后，建议连续采集多组动态图像进行验证。

不要仅依据单帧图像判断 Ghost 校正效果。

---

# 10. Prevention

建议：

- 动态模式首次部署时完成 Ghost Calibration
- 修改 Mode、ROI 或关键采集参数后重新验证 Ghost Template
- 保持网络稳定，避免采集过程中丢帧
- 定期验证 Ghost 校正效果
- 建立 Ghost Template 版本管理

---

# 11. Related Documents

Workflow：

- DynamicCorrectionWorkflow.md

Failure Knowledge：

- GhostFailure.md

Decision Tree：

- GhostCorrection.md

Image Diagnosis：

- GhostArtifact

Principles：

- Dynamic Detector
- Swap Mode

Tools：

- CalibrationTools.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Ghost Correction 现场案例，结合动态平板 Ghost、Swap Mode、Pre-offset、Post-offset 等培训内容。 |