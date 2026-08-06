# BlackDots

Version: V1.0

Case ID: CASE-IMG-007

Module: 11_Case / Image

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/BlackDotsArtifact/
- ../../07_FailureKnowledge/ImageFailure/PixelFailure.md
- ../../09_DecisionTree/Image/BlackDots.md
- ../../05_Calibration/DefectCalibration.md

---

# 1. Case Summary

## Case Name

Fixed Black Dots Appearing in the Image

---

# 2. Customer Information

Customer Type：

Hospital

Product：

Pluto1717

Detector：

Ethernet Detector

Working Mode：

Static Imaging

---

# 3. Fault Description

客户反馈：

图像中出现多个固定黑点。

异常特点：

- 黑点位置固定
- 每次曝光均一致
- 不随曝光参数变化
- 不随被摄物变化

客户认为：

探测器内部像素已经损坏。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector Damage（√）
- Calibration Failure（？）
- Software Issue（×）

FAE Initial Assessment：

优先确认是否属于固定坏点，而不是随机噪声。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Firmware Version
- [ ] Calibration Version

## Image Evidence

- [ ] RAW Image（至少3张）
- [ ] Offset Image
- [ ] Gain Image
- [ ] Defect Template

## Software Information

- [ ] SDK Version
- [ ] License Version

## Logs

- [ ] SDK Log

---

# 6. FAE Investigation

## Step 1

连续采集 RAW 图像。

结果：

黑点位置完全一致。

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

Template 未包含当前坏点。

---

## Step 5

重新执行 Defect Calibration。

生成新的 Defect Template。

重新加载。

再次采图。

异常消失。

---

# 7. Root Cause

固定坏点未被 Defect Template 补偿。

属于校准数据问题，并非 Detector 硬件损坏。

---

# 8. Corrective Action

现场采取：

① 重新执行 Defect Calibration。

② 更新 Defect Template。

③ 重新加载校准文件。

④ 连续采图确认。

---

# 9. Verification

验证结果：

- 黑点消失
- RAW 图像正常
- 连续曝光正常
- 客户确认恢复

---

# 10. Preventive Action（CAPA）

建议：

① 每次完成 Defect Calibration 后同步更新 Template。

② Firmware 升级后确认 Calibration 数据是否一致。

③ 建立 Defect Template 版本管理。

---

# 11. Lessons Learned

## Technical

固定黑点多数属于固定像素异常。

## Diagnostic

固定位置异常首先检查 Defect Template。

## Operation

不要直接判定 Detector 损坏。

应优先验证校准数据。

## Maintenance

建议定期更新 Defect Template。

---

# 12. Related Documents

Image Diagnosis：

- BlackDotsArtifact

Failure Knowledge：

- PixelFailure.md

Decision Tree：

- BlackDots.md

Calibration：

- DefectCalibration.md

---

# 13. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Black Dots 图像异常案例。 |