# SampleDelivery

Version: V1.0

Case ID: CASE-CUS-003

Module: 11_Case / Customer

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★★★☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- ../../06_Workflow/SampleDeliveryWorkflow.md
- ../../09_DecisionTree/Customer/SampleDelivery.md
- ../../17_Tools/SDKTool/README.md

---

# 1. Case Summary

## Case Name

Incomplete Sample Information Delayed Failure Analysis

---

# 2. Customer Information

Customer Type：

OEM Customer

Service Type：

Failure Sample Submission

Product：

Pluto Series Detector

---

# 3. Fault Description

客户反馈：

设备存在异常，需要送回研发分析。

样品寄回后发现：

- 无法确认异常环境
- 无法复现问题
- 缺少关键现场资料

研发要求重新补充资料，导致分析周期延长。

---

# 4. Initial Customer Judgment

Customer Judgment：

只需寄回 Detector 即可。

FAE Initial Assessment：

送样资料不完整，无法满足故障分析要求。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Detector Model
- [ ] Firmware Version
- [ ] SDK Version

## Required Photos

- [ ] Detector 信息界面
- [ ] 图像采集界面
- [ ] 探测器正面照片
- [ ] 探测器背面照片
- [ ] 装箱照片

## Supporting Files

- [ ] RAW Image
- [ ] Log File
- [ ] Calibration Information（如适用）
- [ ] License（如适用）

---

# 6. FAE Investigation

## Step 1

确认客户送样原因。

记录：

- 故障现象
- 发生频率
- 是否可稳定复现

---

## Step 2

收集送样资料。

现场确认：

- Detector 信息界面
- 图像采集界面
- 探测器正反面照片
- 装箱照片

---

## Step 3

确认版本信息。

检查：

- Firmware Version
- SDK Version

必要时与 OQC 记录进行比对。

---

## Step 4

确认附件完整。

包括：

- RAW Image
- Log
- License（如适用）

确认后安排送样。

---

# 7. Root Cause

送样资料不完整，导致研发无法快速定位问题。

属于送样准备不充分，而非产品故障。

---

# 8. Corrective Action

现场采取：

① 收集完整送样资料。

② 确认 Firmware 与 SDK 版本。

③ 上传日志及 RAW 图像。

④ 检查包装状态。

⑤ 再安排送样。

---

# 9. Verification

确认：

- 样品信息完整。
- 研发可正常接收。
- 无需二次补充资料。

---

# 10. Preventive Action（CAPA）

建议：

① 建立送样 Checklist。

② 所有送样统一收集 Detector 信息。

③ 每次送样附带 Firmware Version。

④ 保留装箱照片。

---

# 11. Lessons Learned

## Technical

完整资料能够显著提高故障分析效率。

## Diagnostic

RAW 图像、Log 与版本信息缺一不可。

## Operation

送样前必须逐项确认 Checklist。

## Maintenance

建议建立统一送样模板，避免遗漏资料。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 根据现场送样规范，每次送样建议至少提供以下资料：
>
> - Detector 信息界面截图
> - 图像采集界面截图
> - 探测器正面照片
> - 探测器背面照片
> - 装箱照片
>
> 如涉及图像异常，还应补充 RAW 图像、日志文件及相关校准信息，以便研发快速复现和定位问题。

---

# 13. Related Documents

Workflow：

- SampleDeliveryWorkflow.md

Decision Tree：

- SampleDelivery.md

Tools：

- SDKTool/README.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Sample Delivery 现场案例，规范送样资料准备及检查要求。 |