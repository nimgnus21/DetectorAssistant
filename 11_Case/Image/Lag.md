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

---

## Experience 02 – Low Gray Value on the First Image

### Source

FAE Pre-sales Weekly Report

### Product

Mercu Series / Venu Series

### Symptom

- Detector communication is normal.
- The first acquired image has a noticeably lower gray value.
- Subsequent images return to normal.
- The issue can be reproduced after restarting the application.

### Investigation

Verified items:

- Detector communication: Normal
- Offset calibration: Passed
- Gain calibration: Passed
- Firmware version: Compatible
- Generator output: Stable

No abnormalities were found in detector hardware or calibration data.

The issue only occurred during the first acquisition after initialization.

### Root Cause

The first-frame gray value was affected by the initialization sequence or exposure synchronization rather than detector hardware.

Possible contributing factors include:

- Detector initialization
- Application startup sequence
- Exposure synchronization timing
- Generator trigger timing

### Solution

1. Verify detector initialization sequence.
2. Perform a warm-up exposure if required.
3. Verify generator trigger timing.
4. Compare acquisition behavior with the official SDK Demo.
5. Repeat acquisition verification.

### Verification

After optimizing the acquisition sequence:

- First-frame gray value returned to normal.
- Continuous acquisition remained stable.
- No detector abnormalities were observed.

### Lessons Learned

If only the first frame is abnormal while subsequent images are normal, priority should be given to checking software initialization and exposure synchronization instead of recalibration or hardware replacement.

---

## Field Experience 03 – Exposure Synchronization Timing

### Source

FAE Pre-sales Weekly Report

### Product

Mercu Series / Pluto Series

### Symptom

- Detector communication is normal.
- Trigger signal is received.
- Image acquisition is unstable.
- First image is abnormal.
- Continuous acquisition becomes normal.

### Investigation

Verified:

- Detector communication: Normal
- Detector firmware: Normal
- Offset calibration: Passed
- Gain calibration: Passed
- Generator output: Stable

Detector hardware showed no abnormalities.

Further analysis focused on generator trigger timing.

### Root Cause

Exposure synchronization between the generator and detector was not properly matched.

The detector entered exposure normally, but the trigger timing was inconsistent with the X-ray output timing.

### Failure Classification

Detector Hardware：No

Detector Firmware：No

Detector Configuration：No

Customer Environment：Yes

Third-party Equipment：Yes

### Solution

1. Verify generator trigger timing.
2. Verify detector exposure mode.
3. Check trigger delay configuration.
4. Repeat exposure synchronization test.
5. Verify continuous acquisition.

### Verification

After adjusting exposure synchronization:

- Image acquisition became stable.
- First-frame abnormality disappeared.
- Continuous acquisition operated normally.

### Lessons Learned

Many first-frame image problems originate from exposure synchronization rather than detector hardware.

Generator timing should always be verified before recalibration or detector replacement.