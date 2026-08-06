# Noise

Version: V1.0

Module: 11_Case / Image

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/NoiseArtifact/
- ../../07_FailureKnowledge/ImageFailure/NoiseFailure.md
- ../../09_DecisionTree/Image/Noise.md
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Excessive Image Noise After Calibration

---

# 2. Customer Environment

Product：

- Pluto1717

Detector Status：

- New Installation

Operation：

- Offset Calibration Completed
- Gain Calibration Completed

Environment：

- Hospital DR Room

---

# 3. Fault Description

客户反馈：

探测器能够正常采图。

图像整体存在大量随机噪点。

没有固定位置。

重新曝光后：

噪点位置不断变化。

客户怀疑：

Detector 出现大量坏点。

---

# 4. Troubleshooting Timeline

## Step 1

确认 Detector 通信状态。

结果：

正常。

---

## Step 2

检查 Defect Template。

结果：

正常加载。

坏点数量正常。

排除 Defect Template 异常。

---

## Step 3

连续采集暗场图。

观察发现：

随机噪点位置不断变化。

并非固定像素异常。

---

## Step 4

检查 Offset Calibration。

发现：

Offset Calibration 执行时环境存在异常干扰。

---

## Step 5

重新完成：

- Offset Calibration
- Gain Calibration

再次采图。

图像恢复正常。

---

# 5. Root Cause

Offset Calibration 数据异常，导致后续图像噪声增加。

详细分析参见：

- ../../07_FailureKnowledge/ImageFailure/NoiseFailure.md

---

# 6. Solution

处理措施：

- 排除环境干扰
- 重新执行 Offset Calibration
- 重新执行 Gain Calibration
- 验证图像质量

无需更换 Detector。

---

# 7. Verification

验证结果：

- 图像噪声恢复正常
- 无随机异常
- 图像均匀性正常
- 客户连续采图验证通过

---

# 8. Lessons Learned

- 随机噪点通常不是坏点。
- Noise 与 Defect 应首先区分。
- 校准环境异常可能直接导致 Noise 增加。
- 不建议在未确认原因前直接重新生成 Defect Template。

---

# 9. Related Documents

Image Diagnosis：

- NoiseArtifact

Failure Knowledge：

- NoiseFailure.md

Decision Tree：

- Noise.md

Tools：

- CalibrationTools.md

---

# 10. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Noise 现场案例。 |

---

## Case 03 – Grid Installed in Wrong Direction

### Product

Mercu1724

### Customer

OEM Customer

### Symptom

- Image shows obvious non-uniformity.
- Brightness is inconsistent across the image.
- Detector communication is normal.
- Calibration has been completed.
- Recalibration does not improve the image.

### Investigation

The following items were verified:

- Detector communication: Normal
- Firmware version: Normal
- Offset calibration: Passed
- Gain calibration: Passed
- Ghost correction: Passed

No abnormalities were found in the detector.

Further inspection revealed that the anti-scatter grid was installed in the wrong orientation.

### Root Cause

Incorrect grid installation introduced additional X-ray attenuation, resulting in image non-uniformity.

The detector was operating normally.

### Corrective Action

1. Confirm the installation direction of the grid.
2. Reinstall the grid according to the manufacturer's specification.
3. Repeat image acquisition.
4. Compare the image before and after correction.

### Verification

After correcting the grid orientation:

- Image uniformity returned to normal.
- No additional calibration was required.
- Detector function remained normal.

### Lessons Learned

Image non-uniformity is not always caused by detector failure.

Before repeating calibration or replacing hardware, verify external imaging components such as the grid and X-ray generator.

---

## Field Experience 01 – Image Non-uniformity Caused by Incorrect Grid Installation

### Source

FAE Pre-sales Weekly Report

### Product

Mercu1724

### Symptom

- Image shows obvious brightness non-uniformity.
- Local contrast is inconsistent.
- Detector communication is normal.
- Offset, Gain and Ghost calibration have all passed.
- Recalibration does not improve image quality.

### Investigation

The following items were verified:

- Detector communication: Normal
- Firmware version: Compatible
- Offset calibration: Passed
- Gain calibration: Passed
- Ghost correction: Passed

No abnormalities were found in the detector.

Further inspection of the imaging system found that the anti-scatter grid had been installed in the wrong orientation.

### Root Cause

The image artifact was caused by incorrect installation of the anti-scatter grid.

The detector hardware, firmware and calibration data were all functioning normally.

### Failure Classification

- Detector Hardware：No
- Detector Firmware：No
- Detector Configuration：No
- Customer Environment：Yes
- Third-party Equipment：Yes

### Solution

1. Confirm the installation direction of the anti-scatter grid.
2. Reinstall the grid according to the manufacturer's specification.
3. Repeat image acquisition.
4. Compare image uniformity before and after correction.

### Verification

After reinstalling the grid correctly:

- Image uniformity returned to normal.
- No recalibration was required.
- Detector performance remained normal.

### Lessons Learned

Image non-uniformity is not always caused by detector defects.

When calibration results are normal but image quality remains abnormal, external imaging components such as the anti-scatter grid should be inspected before replacing detector hardware.