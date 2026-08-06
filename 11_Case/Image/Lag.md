# Lag

Version: V1.0

Module: 11_Case / Image

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Static Flat Panel Detector（高剂量曝光后）
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/LagArtifact/
- ../../07_FailureKnowledge/ImageFailure/LagFailure.md
- ../../09_DecisionTree/Image/Lag.md

---

# 1. Case Summary

## Case Name

Lag Artifact After High Dose Exposure

---

# 2. Customer Environment

Product：

- Pluto Dynamic Detector

Application：

- Dynamic Fluoroscopy

Exposure：

- Long Continuous Exposure

SDK：

- SDK_AIO

---

# 3. Fault Description

客户反馈：

连续曝光结束后，即使停止 X-Ray，图像仍需要数秒才能恢复正常。

高灰度区域恢复速度明显慢于其它区域。

客户误认为：

Detector 出现 Ghost。

---

# 4. Troubleshooting Timeline

## Step 1

检查 Detector 通信状态。

结果：

正常。

---

## Step 2

检查：

- Image Loss
- Timeout

结果：

未发现异常。

---

## Step 3

检查 Ghost Template。

结果：

Ghost Template 已正常加载。

Ghost Calibration 正常。

---

## Step 4

连续采集动态图像。

观察发现：

停止曝光后，

残留图像逐渐减弱。

并非固定保留上一帧图像。

---

## Step 5

结合图像表现，

判断：

该异常符合 Lag 特征。

---

# 5. Root Cause

高剂量连续曝光导致像素响应恢复速度下降，形成 Lag Artifact。

详细机理参见：

- ../../07_FailureKnowledge/ImageFailure/LagFailure.md

---

# 6. Solution

建议：

- 停止连续曝光
- 等待 Detector 完全恢复
- 调整曝光参数
- 必要时重新执行动态校正验证

本案例无需重新执行 Ghost Calibration。

---

# 7. Verification

验证结果：

- 图像逐渐恢复正常
- 无固定残影
- 后续采集正常
- Detector 工作正常

问题解决。

---

# 8. Lessons Learned

- Lag 与 Ghost 极易混淆。
- 若残影随时间逐渐衰减，应优先考虑 Lag，而不是 Ghost。
- 不要因为出现残影立即重新执行 Ghost Calibration，应先确认异常类型。

---

# 9. Related Documents

Image Diagnosis：

- LagArtifact

Failure Knowledge：

- LagFailure.md

Decision Tree：

- Lag.md

---

# 10. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Lag Artifact 现场案例。 |