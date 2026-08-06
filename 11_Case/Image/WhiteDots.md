# WhiteDots

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

- ../../08_ImageDiagnosis/WhiteDotsArtifact/
- ../../07_FailureKnowledge/ImageFailure/PixelFailure.md
- ../../09_DecisionTree/Image/WhiteDots.md
- ../../05_Calibration/DefectCalibration.md
- ../../17_Tools/SDKTool/CalibrationTools.md

---

# 1. Case Summary

## Case Name

Fixed White Dots Appearing in the Image

---

# 2. Customer Information

Customer Type：

Hospital

Product：

Pluto1717

Application：

General Radiography

Detector Status：

In Service

---

# 3. Fault Description

客户反馈：

图像中出现多个固定白点。

异常特点：

- 白点位置固定
- 每次曝光均出现
- 曝光参数改变后无变化
- 更换拍摄对象后仍存在

客户认为：

探测器出现大量坏点，需要返厂维修。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector Hardware Failure（√）
- Calibration Failure（？）
- Network Failure（×）

FAE Initial Assessment：

固定位置异常，更倾向于 Pixel Defect，而非随机噪声。

---

# 5. FAE Investigation

## Step 1

连续采集多张 RAW 图像。

结果：

白点位置完全一致。

---

## Step 2

检查 Offset Template。

结果：

正常。

---

## Step 3

检查 Gain Template。

结果：

正常。

---

## Step 4

检查 Defect Template。

发现：

当前 Template 为旧版本。

近期 Detector 已重新校准，但 Defect Template 未同步更新。

---

## Step 5

重新执行 Defect Calibration。

重新生成 Template。

重新加载。

再次采图。

白点全部消失。

---

# 6. Root Cause

Detector 更换校准数据后仍继续使用旧版 Defect Template，导致固定坏点未被正确补偿。

详细分析请参见：

- ../../07_FailureKnowledge/ImageFailure/PixelFailure.md

---

# 7. Corrective Action

现场处理：

- 重新执行 Defect Calibration
- 更新 Defect Template
- 重新加载 Calibration Data
- 连续采图验证

无需返厂维修。

---

# 8. Verification

验证结果：

- 固定白点消失
- 图像均匀
- 连续曝光正常
- 客户现场确认恢复

---

# 9. Preventive Action (CAPA)

建议：

- 每次重新完成 Defect Calibration 后，立即更新 Template。
- 更换 Firmware、ROI 或 Calibration Data 后，确认 Template 是否同步更新。
- 建立 Calibration Template 版本管理，避免使用历史模板。

---

# 10. Lessons Learned

- 固定白点首先检查 Defect Template，而不是直接判定 Detector 损坏。
- 白点位置固定通常说明属于固定像素异常。
- 随机变化的白点应优先考虑 Noise，而非 Pixel Defect。
- 校准模板版本管理是现场维护的重要环节。

---

# 11. Related Documents

Image Diagnosis：

- WhiteDotsArtifact

Failure Knowledge：

- PixelFailure.md

Decision Tree：

- WhiteDots.md

Calibration：

- DefectCalibration.md

Tools：

- CalibrationTools.md

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 White Dots 图像异常现场案例。 |