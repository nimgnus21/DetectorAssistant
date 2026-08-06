# VerticalLine

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

- ../../08_ImageDiagnosis/VerticalLineArtifact/
- ../../07_FailureKnowledge/ImageFailure/ColumnFailure.md
- ../../09_DecisionTree/Image/VerticalLine.md
- ../../13_Principles/TFTReadout/
- ../../13_Principles/GateDriver/

---

# 1. Case Summary

## Case Name

Vertical Line Appears Across the Entire Image

---

# 2. Customer Environment

Customer：

- Hospital DR Department

Product：

- Pluto1717

Operation：

- Static Radiography

Detector：

- Wired Ethernet Detector

---

# 3. Fault Description

客户反馈：

图像中始终存在一条贯穿整个图像高度的亮线。

特点：

- 每次曝光位置固定
- 与曝光条件无关
- 重启软件后仍然存在
- 更换被摄体后位置不变

客户怀疑探测器已经损坏。

---

# 4. Troubleshooting Timeline

## Step 1

检查网络通信状态。

确认：

- Detector Online
- 无 Image Loss
- 无 Timeout

结果：

通信正常。

---

## Step 2

重新采集 Offset。

结果：

异常仍存在。

---

## Step 3

重新加载：

- Offset Template
- Gain Template
- Defect Template

结果：

无改善。

---

## Step 4

采集暗场图。

观察：

亮线仍然存在。

排除曝光因素。

---

## Step 5

比较多张 RAW 图像。

发现：

异常始终位于相同列坐标。

判断：

属于固定列异常。

---

## Step 6

结合读出结构分析。

怀疑：

列读出通道异常。

建议进一步进行硬件检测。

---

# 5. Root Cause

固定列读出异常导致整列像素输出异常。

详细形成机理请参见：

- ../../07_FailureKnowledge/ImageFailure/ColumnFailure.md

---

# 6. Solution

处理措施：

- 导出 RAW 图像
- 记录异常列位置
- 检查 Defect Template 是否可修正
- 若无法修正，提交硬件检测

必要时返厂维修。

---

# 7. Verification

维修后验证：

- 连续采图正常
- 固定亮线消失
- 图像均匀
- 多次曝光结果一致

问题解决。

---

# 8. Lessons Learned

- 固定位置且贯穿整幅图像的竖线，应优先怀疑列读出异常。
- 若暗场图中同样存在该异常，可基本排除曝光因素。
- 不建议反复重新校准，应先确认异常是否属于硬件读出问题。

---

# 9. Related Documents

Image Diagnosis：

- VerticalLineArtifact

Failure Knowledge：

- ColumnFailure.md

Decision Tree：

- VerticalLine.md

Principles：

- TFTReadout
- GateDriver

---

# 10. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Vertical Line 图像异常现场案例。 |