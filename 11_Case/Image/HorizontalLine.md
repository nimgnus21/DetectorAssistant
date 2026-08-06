# HorizontalLine

Version: V1.0

Module: 11_Case / Image

Status: Released

Severity: ★★★★★

Typical Frequency: ★★★★☆

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/HorizontalLineArtifact/
- ../../07_FailureKnowledge/ImageFailure/RowFailure.md
- ../../09_DecisionTree/Image/HorizontalLine.md
- ../../13_Principles/TFTReadout/
- ../../13_Principles/GateDriver/

---

# 1. Case Summary

## Case Name

Horizontal Line Appears Across the Entire Image

---

# 2. Customer Environment

Customer：

- Orthopedic Hospital

Product：

- Pluto1717

Operation：

- Static Radiography

Detector：

- Wired Ethernet Detector

---

# 3. Fault Description

客户反馈：

图像中持续出现一条横贯整个图像宽度的亮线。

异常特点：

- 每次曝光均出现
- 行位置固定
- 更换曝光参数无变化
- 更换被摄体无变化
- 软件重启后仍存在

---

# 4. Initial Customer Judgment

客户初步判断：

- Detector 硬件损坏（√）
- Offset 校准异常（？）
- 网络问题（×）

FAE 初步判断：

- 固定行异常，需要进一步确认是否属于 Row Readout 问题。

---

# 5. Troubleshooting Timeline

## Step 1

检查 Detector 通信状态。

结果：

- Detector Online
- 无 Image Loss
- 无 Timeout

通信正常。

---

## Step 2

重新采集 Offset。

结果：

横线仍存在。

---

## Step 3

重新加载：

- Offset Template
- Gain Template
- Defect Template

结果：

异常无变化。

---

## Step 4

采集暗场图。

观察：

暗场图仍存在相同行位置异常。

排除曝光因素。

---

## Step 5

采集多张 RAW 图像。

结果：

异常始终位于同一行。

判断：

属于固定行异常。

---

## Step 6

结合 TFT Readout 原理分析。

初步判断：

Row Readout 通道异常。

建议进一步进行硬件检测。

---

# 6. Root Cause

固定行读出异常导致整行像素输出异常。

详细机理请参见：

- ../../07_FailureKnowledge/ImageFailure/RowFailure.md

---

# 7. Solution

现场处理：

- 保存 RAW 图像
- 记录异常行坐标
- 验证 Defect Template 是否能够修正

若无法修正：

提交研发进一步分析，并安排返厂检测。

---

# 8. Verification

维修完成后验证：

- 横线消失
- 图像均匀
- 暗场图正常
- 连续曝光验证正常

问题解决。

---

# 9. Lessons Learned

- 固定位置且贯穿整幅图像的横线，应优先怀疑 Row Readout 异常。
- 暗场图仍存在横线，可快速排除曝光条件影响。
- 不建议在未定位异常前反复执行校准，应优先确认是否属于硬件读出问题。
- 记录异常行坐标，有助于研发快速定位故障。

---

# 10. Related Documents

Image Diagnosis：

- HorizontalLineArtifact

Failure Knowledge：

- RowFailure.md

Decision Tree：

- HorizontalLine.md

Principles：

- TFTReadout
- GateDriver

---

# 11. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Horizontal Line 图像异常现场案例。 |