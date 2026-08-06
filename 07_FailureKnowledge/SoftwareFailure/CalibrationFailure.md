# CalibrationFailure

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- ConfigurationFailure.md
- CommunicationFailure.md
- ../../05_Calibration/CalibrationWorkflow.md
- ../../05_Calibration/OffsetCalibration.md
- ../../05_Calibration/GainCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Calibration Failure 描述数字平板探测器（Flat Panel Detector，FPD）校准（Calibration）过程中常见的软件故障模式、形成机理、图像表现、检测方法及根因分析。

Calibration 是保证 Detector 图像质量的重要软件流程，通过 Offset、Gain、Bad Pixel 等校正消除器件固有误差，提高图像均匀性、灰度一致性及诊断质量。

Calibration Failure 会直接影响图像质量，即使硬件工作正常，也可能产生明显图像异常。

本文件回答的问题：

> **Calibration 为什么会失败？失败后会导致哪些图像异常？**

---

# 2. Scope

适用于：

- Offset Calibration
- Gain Calibration
- Bad Pixel Calibration
- Factory Calibration
- Field Calibration
- Calibration Verification

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

---

# 3. Calibration Overview

Calibration 的主要职责：

- Offset Correction
- Gain Correction
- Bad Pixel Compensation
- Uniformity Optimization
- Gray Level Correction
- Image Quality Improvement

Calibration 流程：

```text
Detector

↓

Acquire Calibration Image

↓

Generate Calibration Data

↓

Verify Calibration Result

↓

Save Calibration File

↓

Image Correction
```

---

# 4. Failure Modes

| Failure Mode | Description |
|--------------|-------------|
| Calibration Start Failure | 校准无法启动 |
| Offset Calibration Failure | Offset 校准失败 |
| Gain Calibration Failure | Gain 校准失败 |
| Bad Pixel Calibration Failure | 坏点校准失败 |
| Calibration Data Generation Failure | 校准数据生成失败 |
| Calibration Verification Failure | 校准验证失败 |
| Calibration Save Failure | 校准数据保存失败 |
| Calibration File Corruption | 校准文件损坏 |
| Invalid Calibration Parameters | 校准参数错误 |
| Calibration Version Mismatch | 校准版本不匹配 |

---

# 5. Failure Mechanisms

## 5.1 Calibration Start Failure

无法进入 Calibration 流程。

影响：

- 无法执行校准

典型表现：

- Calibration Start Failed

---

## 5.2 Offset Calibration Failure

Offset Image 获取失败或计算异常。

影响：

- Offset Correction 无效

典型表现：

- 图像背景不均匀
- Gray Offset 异常

---

## 5.3 Gain Calibration Failure

Gain 数据生成异常。

影响：

- Gain Correction 失效

典型表现：

- 图像亮度不均
- Contrast 异常

---

## 5.4 Bad Pixel Calibration Failure

坏点识别失败。

影响：

- Bad Pixel 无法补偿

典型表现：

- Dead Pixel
- Bright Pixel

---

## 5.5 Calibration Data Generation Failure

校准计算过程中发生异常。

影响：

- Calibration Table 无法生成

---

## 5.6 Calibration Verification Failure

校准结果验证失败。

影响：

- 校准结果不可用

---

## 5.7 Calibration Save Failure

校准文件无法保存。

影响：

- 重启后校准失效

---

## 5.8 Calibration File Corruption

校准文件损坏。

影响：

- 图像恢复到未校准状态

---

## 5.9 Invalid Calibration Parameters

校准参数设置错误。

影响：

- 校准结果失真

---

## 5.10 Calibration Version Mismatch

Calibration 文件与 Firmware 或 SDK 不兼容。

影响：

- Calibration 无法加载

---

# 6. Typical Symptoms

| Symptom | Possible Cause |
|----------|----------------|
| Calibration Failed | Start Failure |
| Image Non-uniformity | Gain Failure |
| Background Offset | Offset Failure |
| Dead Pixel Increase | Bad Pixel Failure |
| Calibration Lost After Restart | Save Failure |
| Calibration File Invalid | File Corruption |
| Calibration Cannot Load | Version Mismatch |

---

# 7. Failure Impact

| Module | Impact |
|---------|--------|
| Image Generation | 图像质量下降 |
| Uniformity | 均匀性下降 |
| Gray Scale | 灰度一致性下降 |
| Detector Performance | 成像质量下降 |

---

# 8. Detection Methods

## Calibration Log

检查：

- Calibration Step
- Error Code
- Verification Result

---

## Calibration File Verification

检查：

- File Exists
- File Size
- Checksum
- Version

---

## Image Comparison

比较：

- Calibration Before
- Calibration After

---

## Uniformity Test

检查：

- Offset Uniformity
- Gain Uniformity

---

## Parameter Verification

确认：

- Exposure
- Temperature
- Calibration Mode

---

# 9. Root Cause Analysis

```text
Calibration Failed

↓

Calibration Started？

↓

NO

↓

Configuration / SDK

↓

YES

↓

Calibration File Generated？

↓

NO

↓

Generation Failure

↓

YES

↓

Verification Passed？

↓

NO

↓

Calibration Invalid

↓

YES

↓

Save Success？

↓

NO

↓

Save Failure

↓

YES

↓

Calibration Complete
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Wrong Exposure Condition | 校准曝光条件错误 |
| Calibration File Deleted | 校准文件丢失 |
| Gain Image Invalid | Gain 图像异常 |
| Offset Image Invalid | Offset 图像异常 |
| Software Upgrade | 校准版本不兼容 |
| File Save Failure | 校准文件保存失败 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 局部校准异常 |
| Moderate | 图像质量下降 |
| Major | 校准无法完成 |
| Critical | Detector 无法正常成像 |

---

# 12. Engineering Recommendations

建议：

- 校准前确认 Detector 工作状态正常。
- 使用标准曝光条件完成 Calibration。
- 校准完成后立即验证图像质量。
- 定期备份 Calibration 文件。
- 软件升级前备份全部 Calibration 数据。
- 排除 Hardware、Configuration 和 SDK 问题后，再确认 Calibration 软件故障。

---

# 13. Relationship with Other Modules

## ConfigurationFailure

Calibration 依赖正确的 Configuration 参数。

---

## SDKFailure

SDK 提供 Calibration 控制接口。

---

## CalibrationWorkflow

Calibration Workflow 定义完整校准流程。

---

## DecisionTree

Calibration Failure 是以下诊断的重要节点：

- Calibration Failed
- Uniformity Poor
- Background Offset
- Bad Pixel Increase
- Calibration File Invalid

---

# 14. Knowledge Graph

```text
Calibration

├── Start Failure
├── Offset Failure
├── Gain Failure
├── Bad Pixel Failure
├── Data Generation Failure
├── Verification Failure
├── Save Failure
├── File Corruption
├── Parameter Error
└── Version Mismatch

↓

Calibration File

↓

Image Correction

↓

Image Quality

↓

DecisionTree
```

---

# 15. Summary

Calibration Failure 是 Flat Panel Detector 软件系统中直接影响图像质量的重要故障类型，其主要表现为 Offset 校准失败、Gain 校准失败、坏点校准失败、校准数据生成异常、校准文件损坏及校准参数错误等。由于 Calibration 决定图像均匀性、灰度一致性及缺陷补偿效果，因此故障通常导致背景不均、亮度异常、坏点增加及整体图像质量下降。故障分析应结合 Calibration Log、Calibration File、图像验证及 Workflow 流程进行综合判断，为 DecisionTree 和现场技术支持提供可靠依据。