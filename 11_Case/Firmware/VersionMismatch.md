# VersionMismatch

Version: V1.0

Case ID: CASE-FW-001

Module: 11_Case / Firmware

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- ../../17_Tools/SDKTool/FirmwareUpgrade.md
- ../../06_Workflow/FirmwareUpgradeWorkflow.md
- ../../07_FailureKnowledge/FirmwareFailure/VersionMismatch.md
- ../../09_DecisionTree/Firmware/VersionMismatch.md

---

# 1. Case Summary

## Case Name

Firmware Version Mismatch

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto1717

Detector Status：

OQC Inspection

Application：

Sample Delivery

---

# 3. Fault Description

客户反馈：

探测器能够正常连接并完成采图。

在 OQC 检查过程中发现：

当前 Detector Firmware Version 与送样要求版本不一致。

客户希望直接送样。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Firmware 不影响测试（√）
- 可以直接送样（√）

FAE Initial Assessment：

需要先确认版本差异是否影响当前测试项目，不建议直接送样。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Detector Model
- [ ] Firmware Version
- [ ] FPGA Version（如适用）

## Software Information

- [ ] SDK Version
- [ ] Release Package Version

## Supporting Documents

- [ ] OQC 检查记录
- [ ] Release Note
- [ ] 客户测试要求

---

# 6. FAE Investigation

## Step 1

在 OQC 阶段确认当前 Firmware Version。

结果：

发现与送样要求版本不一致。

---

## Step 2

确认版本差异。

检查：

- Firmware Version
- SDK Version
- Release Package

确认是否属于同一发布版本。

---

## Step 3

联系研发确认。

重点确认：

- 当前 Firmware 是否支持本次测试项目。
- 是否存在已知 Bug。
- 是否要求统一 Firmware。

---

## Step 4

根据研发意见进行评审。

结果：

当前版本不满足送样要求。

需要升级至指定 Firmware。

---

## Step 5

完成 Firmware 升级。

重新确认：

- Firmware Version
- SDK 通信
- 图像采集

确认正常后安排送样。

---

# 7. Root Cause

Detector Firmware Version 与项目要求版本不一致。

属于版本管理问题，并非 Detector 硬件故障。

详细分析请参见：

- ../../07_FailureKnowledge/FirmwareFailure/VersionMismatch.md

---

# 8. Corrective Action

现场采取：

① 在 OQC 阶段确认 Firmware Version。

② 联系研发确认版本兼容性。

③ 根据评审结果升级 Firmware。

④ 升级后重新验证通信及采图功能。

⑤ 更新 OQC 记录后安排送样。

---

# 9. Verification

验证结果：

- Firmware Version 符合项目要求。
- SDK 通信正常。
- 图像采集正常。
- OQC 审核通过。
- 样机正常送样。

---

# 10. Preventive Action (CAPA)

建议：

① OQC 必须检查 Firmware Version。

② 建立 Firmware Version 与 SDK Version 对照表。

③ 送样前确认 Release Package 一致。

④ 禁止未经确认使用非指定 Firmware。

---

# 11. Lessons Learned

## Technical

Firmware 与 SDK 应保持兼容版本。

## Diagnostic

VersionMismatch 不一定导致故障，但可能影响测试结果或功能验证。

## Operation

OQC 是发现版本问题的最佳阶段，应在送样前完成确认。

## Maintenance

建立 Firmware、SDK、Release Package 的版本对应关系，减少因版本不一致导致的返工。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 根据现场送样流程：
>
> 在 OQC 阶段必须确认当前探测器 Firmware Version。
>
> 若与项目要求版本不一致，应联系研发确认并完成评审，不建议未经确认直接送样。

---

# 13. Related Documents

Workflow：

- FirmwareUpgradeWorkflow.md

Failure Knowledge：

- VersionMismatch.md

Tools：

- FirmwareUpgrade.md

Decision Tree：

- VersionMismatch.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Firmware Version Mismatch 现场案例，整理 OQC 版本确认及送样流程。 |