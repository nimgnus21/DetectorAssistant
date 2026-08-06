# Ghost

Version: V1.0

Module: 11_Case / Image

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series
- Dynamic Imaging System
- Continuous Acquisition System

Related Documents:

- ../../08_ImageDiagnosis/GhostArtifact/
- ../../05_Calibration/DynamicCalibration.md
- ../../06_Workflow/DynamicCorrectionWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/GhostFailure.md
- ../../09_DecisionTree/Image/Ghost.md
- ../../13_Principles/DynamicDetector/
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Ghost Artifact

## Description

Ghost（残影）是动态平板连续采集过程中最典型的图像异常之一。

表现为上一帧或前几帧曝光区域，在后续图像中仍然保留部分轮廓或灰度信息，即使新的曝光条件已经发生变化，图像仍可观察到历史影像。

Ghost 多发生于动态采集、高频曝光及连续透视等应用场景。

---

# 2. Applicable Products

适用于：

- Dynamic Flat Panel Detector
- Pluto 系列动态探测器
- 支持连续采集的动态 DR

一般静态 DR 不会出现典型 Ghost Artifact。

---

# 3. Environment

典型工作流程：

```text
连续曝光

↓

连续采集

↓

Ghost Correction

↓

动态图像输出
```

Ghost 通常发生于：

- 连续曝光
- 高频采集
- 动态透视
- 长时间连续工作

---

# 4. Fault Phenomenon

现场常见现象：

- 上一帧人体轮廓仍然可见
- 高吸收区域残留
- 图像拖尾
- 曝光目标移动后仍保留旧位置轮廓
- 连续图像存在历史影像

特点：

- 静止观察更容易发现
- 高对比区域最明显
- 连续播放时表现为残留阴影

---

# 5. Root Cause Analysis

## 5.1 Ghost Correction 未执行

未建立 Ghost Template。

导致动态图像未经 Ghost Correction。

---

## 5.2 Ghost Template 异常

包括：

- Template 未生成
- Template 损坏
- Template 未加载
- Template 与当前 Mode 不匹配

---

## 5.3 Mode 配置错误

Ghost Correction 与当前 Mode 配置相关。

包括：

- ROI 修改
- Exposure Mode 修改
- Dynamic Mode 修改

---

## 5.4 Swap Mode 配置异常

根据培训资料：

Ghost Correction 通常结合 **Mode132（Swap Mode）** 使用。

若：

- Pre-offset
- Post-offset

采集异常，

Ghost 校正效果将明显下降。

---

## 5.5 长时间连续曝光

连续高剂量曝光后，

Ghost 现象可能更加明显。

---

# 6. Diagnostic Process

建议按照以下顺序排查：

---

## Step 1

确认是否为动态模式。

Ghost 主要发生于：

- Dynamic Detector
- 连续采集模式

---

## Step 2

确认 Ghost Artifact。

观察：

残影是否来自上一帧。

若上一帧轮廓能够对应当前残留图像，

则可初步判断 Ghost。

---

## Step 3

检查 Ghost Template。

确认：

- 已生成
- 已加载
- 与当前 Mode 匹配

---

## Step 4

检查 Mode Configuration。

确认：

- ROI
- Exposure Mode
- Frame Rate

是否发生修改。

---

## Step 5

检查 Ghost Calibration。

必要时：

重新执行 Ghost Calibration。

---

## Step 6

检查采集过程。

确认：

- 无 Image Loss
- 无 Timeout
- 网络稳定

避免 Ghost Calibration 数据异常。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

动态图像存在人体轮廓残留。

### Cause

Ghost Template 未加载。

### Solution

重新加载 Ghost Template。

恢复正常。

---

## Case 2

### Phenomenon

Ghost Correction 无明显效果。

### Cause

修改 ROI 后继续使用旧 Template。

### Solution

重新执行 Ghost Calibration。

---

## Case 3

### Phenomenon

动态图像持续出现拖尾。

### Cause

Swap Mode 配置异常。

### Solution

检查 Mode132 配置。

重新建立 Ghost Template。

---

## Case 4

### Phenomenon

Ghost 偶尔出现。

### Cause

Ghost Calibration 采集过程中发生 Image Loss。

### Solution

恢复网络通信。

重新执行 Ghost Calibration。

---

# 8. Verification

确认：

- 连续动态图像无明显残影
- Ghost Template 正常加载
- 连续采集稳定
- 图像质量恢复

即可确认问题解决。

---

# 9. Engineering Experience

## Experience 1

Ghost 主要发生于动态平板。

静态 DR 一般无需怀疑 Ghost。

---

## Experience 2

Ghost 与 Lag 极易混淆。

Ghost 通常表现为：

**上一帧图像残留。**

Lag 更多表现为：

**像素响应恢复较慢。**

两者不可混为一类。

---

## Experience 3

Ghost Calibration 后，

建议连续采集多帧动态图像进行验证。

不要仅观察单帧图像。

---

## Experience 4

若修改：

- ROI
- Frame Rate
- Dynamic Mode

建议重新验证 Ghost Template 是否仍适用。

---

# 10. Prevention

建议：

- 动态模式首次部署完成 Ghost Calibration
- 修改关键采集参数后重新验证 Ghost Template
- 定期检查 Ghost 校正效果
- 保持网络通信稳定
- 建立 Ghost Template 版本管理

---

# 11. Related Documents

Image Diagnosis：

- GhostArtifact

Workflow：

- DynamicCorrectionWorkflow.md

Failure Knowledge：

- GhostFailure.md

Decision Tree：

- Ghost.md

Tools：

- CalibrationTools.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Ghost Artifact 现场案例及处理经验。 |