# ImageShift

Version: V1.0

Case ID: CASE-IMG-008

Module: 11_Case / Image

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★☆☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/ImageShiftArtifact/
- ../../07_FailureKnowledge/ImageFailure/ImageShift.md
- ../../09_DecisionTree/Image/ImageShift.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../17_Tools/SDKTool/ModeConfiguration.md

---

# 1. Case Summary

## Case Name

Image Position Shift During Acquisition

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto0900X

Detector：

Dynamic Detector

Working Mode：

Continuous Acquisition

---

# 3. Fault Description

客户反馈：

连续采图过程中，图像整体向左（或向右）发生偏移。

异常特点：

- 图像内容完整，但位置发生偏移
- 偏移量基本固定
- 连续采图过程中持续出现
- 静态模式正常，动态模式异常

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector Hardware Failure（？）
- SDK Software Issue（？）
- Trigger Timing Failure（√）

FAE Initial Assessment：

优先检查同步时序及 Mode 配置。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Firmware Version
- [ ] FPGA Version

## Configuration

- [ ] Mode Configuration
- [ ] ROI Configuration
- [ ] Trigger Configuration
- [ ] Frame Rate

## Image Evidence

- [ ] RAW Image（连续采集）
- [ ] Offset
- [ ] Gain

## Logs

- [ ] SDK Log
- [ ] Detector Log

---

# 6. FAE Investigation

## Step 1

确认异常仅发生于动态模式。

结果：

静态模式正常。

---

## Step 2

检查 ROI 配置。

确认：

- ROI 是否满足 8 对齐要求。
- ROI 是否发生修改。

结果：

配置正常。

---

## Step 3

检查 Mode Configuration。

重点确认：

- Frame Rate
- Exposure Mode
- Readout Timing

结果：

Frame 配置与客户软件不一致。

---

## Step 4

检查 Trigger Timing。

确认：

- Acquire
- Enable
- X-Ray
- FrameReq

时序是否一致。

结果：

Trigger 提前到达，导致图像读出位置发生偏移。

---

## Step 5

重新配置 Mode。

重新采图。

结果：

图像恢复正常。

---

# 7. Root Cause

Trigger 时序与 Detector 当前 Mode 不匹配，导致图像采集起始位置错误，引起整体偏移。

---

# 8. Corrective Action

现场采取：

① 检查 ROI 配置。

② 检查 Trigger 时序。

③ 重新配置 Mode。

④ 重新启动 Detector。

⑤ 连续采图验证。

---

# 9. Verification

验证结果：

- 图像位置恢复正常
- 连续采集稳定
- 无再次偏移
- 客户确认问题解决

---

# 10. Preventive Action（CAPA）

建议：

① 修改 ROI 后重新验证 Mode。

② 修改帧率后重新验证 Trigger Timing。

③ SDK 升级后重新验证连续采图。

④ 保存现场 Mode Configuration。

---

# 11. Lessons Learned

## Technical

Image Shift 通常与同步时序有关，而不是图像校准问题。

## Diagnostic

优先检查 Trigger、ROI、Mode，再考虑硬件。

## Operation

修改 ROI 后应同步验证动态模式。

## Maintenance

保留现场 Mode Configuration，便于快速恢复。

---

# 12. Related Documents

Image Diagnosis：

- ImageShiftArtifact

Failure Knowledge：

- ImageShift.md

Workflow：

- ImageGenerationWorkflow.md
- ReadoutWorkflow.md

Tools：

- ModeConfiguration.md

Decision Tree：

- ImageShift.md

---

# 13. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Image Shift 图像异常案例。 |# ImageShift

Version: V1.0

Case ID: CASE-IMG-008

Module: 11_Case / Image

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★☆☆☆

Applicable Products:

- Dynamic Flat Panel Detector
- Pluto Series

Related Documents:

- ../../08_ImageDiagnosis/ImageShiftArtifact/
- ../../07_FailureKnowledge/ImageFailure/ImageShift.md
- ../../09_DecisionTree/Image/ImageShift.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../17_Tools/SDKTool/ModeConfiguration.md

---

# 1. Case Summary

## Case Name

Image Position Shift During Acquisition

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto0900X

Detector：

Dynamic Detector

Working Mode：

Continuous Acquisition

---

# 3. Fault Description

客户反馈：

连续采图过程中，图像整体向左（或向右）发生偏移。

异常特点：

- 图像内容完整，但位置发生偏移
- 偏移量基本固定
- 连续采图过程中持续出现
- 静态模式正常，动态模式异常

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector Hardware Failure（？）
- SDK Software Issue（？）
- Trigger Timing Failure（√）

FAE Initial Assessment：

优先检查同步时序及 Mode 配置。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Firmware Version
- [ ] FPGA Version

## Configuration

- [ ] Mode Configuration
- [ ] ROI Configuration
- [ ] Trigger Configuration
- [ ] Frame Rate

## Image Evidence

- [ ] RAW Image（连续采集）
- [ ] Offset
- [ ] Gain

## Logs

- [ ] SDK Log
- [ ] Detector Log

---

# 6. FAE Investigation

## Step 1

确认异常仅发生于动态模式。

结果：

静态模式正常。

---

## Step 2

检查 ROI 配置。

确认：

- ROI 是否满足 8 对齐要求。
- ROI 是否发生修改。

结果：

配置正常。

---

## Step 3

检查 Mode Configuration。

重点确认：

- Frame Rate
- Exposure Mode
- Readout Timing

结果：

Frame 配置与客户软件不一致。

---

## Step 4

检查 Trigger Timing。

确认：

- Acquire
- Enable
- X-Ray
- FrameReq

时序是否一致。

结果：

Trigger 提前到达，导致图像读出位置发生偏移。

---

## Step 5

重新配置 Mode。

重新采图。

结果：

图像恢复正常。

---

# 7. Root Cause

Trigger 时序与 Detector 当前 Mode 不匹配，导致图像采集起始位置错误，引起整体偏移。

---

# 8. Corrective Action

现场采取：

① 检查 ROI 配置。

② 检查 Trigger 时序。

③ 重新配置 Mode。

④ 重新启动 Detector。

⑤ 连续采图验证。

---

# 9. Verification

验证结果：

- 图像位置恢复正常
- 连续采集稳定
- 无再次偏移
- 客户确认问题解决

---

# 10. Preventive Action（CAPA）

建议：

① 修改 ROI 后重新验证 Mode。

② 修改帧率后重新验证 Trigger Timing。

③ SDK 升级后重新验证连续采图。

④ 保存现场 Mode Configuration。

---

# 11. Lessons Learned

## Technical

Image Shift 通常与同步时序有关，而不是图像校准问题。

## Diagnostic

优先检查 Trigger、ROI、Mode，再考虑硬件。

## Operation

修改 ROI 后应同步验证动态模式。

## Maintenance

保留现场 Mode Configuration，便于快速恢复。

---

# 12. Related Documents

Image Diagnosis：

- ImageShiftArtifact

Failure Knowledge：

- ImageShift.md

Workflow：

- ImageGenerationWorkflow.md
- ReadoutWorkflow.md

Tools：

- ModeConfiguration.md

Decision Tree：

- ImageShift.md

---

# 13. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Image Shift 图像异常案例。 |