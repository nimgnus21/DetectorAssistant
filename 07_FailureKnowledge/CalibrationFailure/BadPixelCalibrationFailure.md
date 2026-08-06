# BadPixelCalibrationFailure

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
- OffsetCalibrationFailure.md
- GainCalibrationFailure.md
- CalibrationDataFailure.md
- ../ImageFailure/BadPixelArtifact.md
- ../HardwareFailure/TFTFailure.md
- ../HardwareFailure/PhotodiodeFailure.md
- ../HardwareFailure/ADCFailure.md
- ../SoftwareFailure/CalibrationFailure.md
- ../../05_Calibration/BadPixelCalibration.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Bad Pixel Calibration Failure 描述数字平板探测器（Flat Panel Detector，FPD）在 Bad Pixel Calibration（坏点校准）过程中发生的各种异常，包括坏点检测失败、坏点补偿失败、Bad Pixel Map 生成异常及校准后图像仍存在坏点等问题。

Bad Pixel Calibration 用于识别 Detector 中无法正常工作的 Pixel，并建立 Bad Pixel Map，通过插值算法对坏点进行补偿，从而保证图像连续性和诊断质量。

本文件回答的问题：

> **为什么 Bad Pixel Calibration 会失败？为什么校准完成后图像仍然存在坏点？**

---

# 2. Scope

适用于：

- Factory Calibration
- Acceptance Test
- Preventive Maintenance
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Bad Pixel Detection
- Bad Pixel Mapping
- Bad Pixel Compensation
- Bad Pixel Verification

---

# 3. What is Bad Pixel Calibration Failure

Bad Pixel Calibration Failure 指：

**Detector 无法正确识别、保存、加载或应用 Bad Pixel Map，导致坏点补偿失败。**

主要表现：

- Bad Pixel Calibration Failed
- Bad Pixel Detection Failed
- Bad Pixel Map Invalid
- Compensation Failed
- Calibration Passed but Bad Pixels Remain
- Bad Pixel Count Abnormal

---

# 4. Failure Classification

```text
Bad Pixel Calibration Failure

├── Calibration Start Failure
├── Bad Pixel Detection Failure
├── Bad Pixel Map Generation Failure
├── Bad Pixel Map Save Failure
├── Bad Pixel Map Load Failure
├── Compensation Failure
└── Verification Failure
```

---

# 5. Typical Symptoms

## 5.1 Calibration Cannot Start

特点：

- 无法启动 Bad Pixel Calibration
- 软件提示 Calibration Failed

可能原因：

- Detector Offline
- Firmware Failure
- Configuration Error

---

## 5.2 Bad Pixel Detection Failure

特点：

- 无法识别坏点
- Bad Pixel Count = 0 或异常偏大

可能原因：

- Invalid Calibration Image
- Threshold Configuration Error
- Firmware Algorithm Error

---

## 5.3 Bad Pixel Map Generation Failure

特点：

- 无法生成 Bad Pixel Map
- Calibration 中断

可能原因：

- Calculation Failure
- Memory Error

---

## 5.4 Bad Pixel Map Save Failure

特点：

- Calibration 完成
- Bad Pixel Map 未保存

可能原因：

- Storage Failure
- Flash Memory Failure
- File Permission Error

---

## 5.5 Bad Pixel Map Load Failure

特点：

- Detector 未加载 Bad Pixel Map
- 系统使用默认配置

可能原因：

- File Missing
- CRC Error
- Version Mismatch

---

## 5.6 Compensation Failure

特点：

- Bad Pixel 已识别
- 图像仍可见坏点

可能原因：

- Compensation Algorithm Failure
- Firmware Error
- Mapping Error

---

## 5.7 Verification Failure

特点：

- 校准成功
- 图像仍存在大量坏点

可能原因：

- TFT Failure
- Photodiode Failure
- Detector Aging

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Calibration Cannot Start | Firmware / Configuration |
| Detection Failure | Threshold Error |
| Map Generation Failure | Algorithm / Memory |
| Save Failure | Storage Failure |
| Load Failure | File Corruption |
| Compensation Failure | Firmware Mapping |
| Verification Failure | Hardware Failure |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| TFT | Dead Pixel |
| Photodiode | Bright / Dark Pixel |
| ADC | Pixel Gray Error |
| FPGA | Compensation Processing Failure |
| Flash Memory | Map Storage Failure |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Detection / Compensation Failure |
| Configuration | Wrong Threshold |
| Driver | Calibration Communication Failure |
| SDK | Bad Pixel Map Loading Failure |

---

# 9. Relationship with Image Failure

Bad Pixel Calibration Failure 可能导致：

- BadPixelArtifact
- Dead Pixel
- Bright Pixel
- Hot Pixel
- Pixel Cluster
- Image Quality Degradation

---

# 10. Diagnostic Workflow

```text
Bad Pixel Calibration Failed

↓

Calibration Started？

↓

NO

↓

Firmware / Configuration

↓

YES

↓

Bad Pixel Detected？

↓

NO

↓

Threshold / Algorithm

↓

YES

↓

Map Generated？

↓

NO

↓

Memory

↓

YES

↓

Map Saved？

↓

NO

↓

Storage

↓

YES

↓

Compensation Effective？

↓

NO

↓

FPGA / Firmware

↓

Image Normal？

↓

NO

↓

TFT / Photodiode

↓

Calibration Passed
```

---

# 11. Detection Methods

## Dark Image Test

检查：

- Bright Pixel
- Hot Pixel

---

## Flat Field Test

检查：

- Dead Pixel
- Cold Pixel

---

## Bad Pixel Map Verification

检查：

- Bad Pixel Count
- Bad Pixel Position
- Map Integrity
- CRC

---

## Compensation Verification

比较：

- Calibration Before
- Calibration After

确认坏点是否被补偿。

---

## Log Analysis

检查：

- Calibration Log
- Firmware Log
- Error Code
- Bad Pixel Count

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Calibration Timeout | Communication Failure |
| Bad Pixel Count = 0 | Detection Failure |
| Bad Pixel Count Too High | Threshold Error |
| Bad Pixels Still Visible | Compensation Failure |
| Map Missing | Storage Failure |
| Increasing Bad Pixels | Detector Aging |

---

# 13. Engineering Recommendations

建议：

- 使用标准 Dark Image 与 Flat Field Image 执行 Bad Pixel Calibration。
- 检查坏点检测阈值配置是否正确。
- 校准完成后验证 Bad Pixel Map 是否正确保存及加载。
- 比较校准前后坏点数量变化。
- 若坏点持续增加，应检查 TFT、Photodiode 及 Detector 老化情况。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## BadPixelCalibration

说明 Bad Pixel Calibration 标准流程。

---

## BadPixelArtifact

说明坏点补偿失败后的图像表现。

---

## TFTFailure

Dead Pixel 的主要硬件来源。

---

## PhotodiodeFailure

Bright Pixel、Hot Pixel 的主要来源。

---

## DecisionTree

Bad Pixel Calibration Failure 是坏点诊断的重要入口。

---

# 15. Knowledge Graph

```text
Bad Pixel Calibration Failure

├── Start Failure
├── Detection Failure
├── Map Generation Failure
├── Save Failure
├── Load Failure
├── Compensation Failure
└── Verification Failure

↓

Bad Pixel Calibration Workflow

↓

Bad Pixel Verification

↓

Hardware Analysis

├── TFT
├── Photodiode
├── ADC
├── FPGA
└── Flash Memory

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Bad Pixel Calibration Failure 是 Flat Panel Detector 坏点校准过程中常见的故障类型，涉及坏点检测、Bad Pixel Map 生成、数据保存、数据加载及坏点补偿等多个环节。其根因通常包括检测阈值配置错误、Firmware 算法异常、Flash 存储故障、TFT/Photodiode 硬件损坏及探测器老化等。通过 Dark Image、Flat Field、Bad Pixel Map 验证及日志分析，可快速定位坏点校准异常，并结合 Image Failure、Hardware Failure 与 DecisionTree 建立完整的坏点故障分析体系。