# FirmwareUpgradeFailed

Version: V1.0

Case ID: CASE-FW-002

Module: 11_Case / Firmware

Status: Released

Severity: ★★★★☆

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- ../../17_Tools/SDKTool/FirmwareUpgrade.md
- ../../06_Workflow/FirmwareUpgradeWorkflow.md
- ../../07_FailureKnowledge/FirmwareFailure/FirmwareUpgradeFailed.md
- ../../09_DecisionTree/Firmware/FirmwareUpgradeFailed.md

---

# 1. Case Summary

## Case Name

Firmware Upgrade Failed

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto1717

Operation：

Firmware Upgrade

---

# 3. Fault Description

客户反馈：

升级 Firmware 过程中升级失败。

表现为：

- Upgrade Failed
- Detector Offline
- 无法重新连接
- Firmware Version 未更新

客户怀疑 Firmware 已损坏。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector 已损坏（？）
- Firmware 写入失败（√）

FAE Initial Assessment：

确认升级流程及升级包是否正确，再判断是否属于 Firmware 损坏。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Detector Model
- [ ] Current Firmware Version

## Upgrade Information

- [ ] Upgrade Package Version
- [ ] SDK Version
- [ ] Upgrade Log

## Supporting Information

- [ ] Release Note
- [ ] SVN Release Package 路径
- [ ] 操作录像（如有）

---

# 6. FAE Investigation

## Step 1

确认升级包来源。

检查：

Release Package 是否来自正式发布目录。

结果：

确认使用正确版本。

---

## Step 2

确认升级前是否保存出厂参数。

结果：

已完成参数备份。

---

## Step 3

重新执行 Firmware Upgrade。

升级完成后：

按照要求断电 10~20 秒。

重新上电。

---

## Step 4

重新连接 Detector。

确认：

- Firmware Version
- SDK 通信
- 图像采集

结果：

升级恢复正常。

---

# 7. Root Cause

升级流程未完整执行（升级完成后未按要求断电重启），导致 Firmware 未正确初始化。

详细分析请参见：

- ../../07_FailureKnowledge/FirmwareFailure/FirmwareUpgradeFailed.md

---

# 8. Corrective Action

现场采取：

① 保存出厂参数。

② 使用正式 Release Package。

③ 重新执行 Firmware Upgrade。

④ 升级完成后断电 10~20 秒。

⑤ 重新连接并验证 Detector。

---

# 9. Verification

验证结果：

- Firmware Version 更新成功。
- Detector 正常连接。
- SDK 通信正常。
- 图像采集正常。

---

# 10. Preventive Action (CAPA)

建议：

① 升级前必须备份出厂参数。

② 使用正式发布的 Firmware Package。

③ 升级完成后严格执行断电 10~20 秒。

④ 升级后验证 Firmware Version 与 SDK 兼容性。

---

# 11. Lessons Learned

## Technical

Firmware 升级不仅包含写入过程，还包括升级后的初始化。

## Diagnostic

Upgrade Failed 不代表 Firmware 已损坏，应先确认升级流程。

## Operation

升级完成后必须执行完整的断电重启流程。

## Maintenance

建立 Firmware 升级记录，保存升级日志与版本信息。

---

# 12. Field Experience

> **FAE 现场经验**
>
> Firmware 升级标准流程：
>
> 1. 保存出厂参数。
> 2. 使用正式 Release Package。
> 3. 完成升级。
> 4. 断电等待 10~20 秒。
> 5. 重新上电并验证通信及图像采集。
>
> 缺少第 4 步是现场较常见的操作失误之一。

---

# 13. Related Documents

Workflow：

- FirmwareUpgradeWorkflow.md

Failure Knowledge：

- FirmwareUpgradeFailed.md

Tools：

- FirmwareUpgrade.md

Decision Tree：

- FirmwareUpgradeFailed.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Firmware Upgrade Failed 现场案例，整理升级失败排查及恢复流程。 |