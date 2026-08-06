# BootFailed

Version: V1.0

Case ID: CASE-FW-003

Module: 11_Case / Firmware

Status: Released

Severity: ★★★★★

Typical Frequency: ★★☆☆☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- ../../17_Tools/SDKTool/FirmwareUpgrade.md
- ../../06_Workflow/FirmwareUpgradeWorkflow.md
- ../../07_FailureKnowledge/FirmwareFailure/BootFailed.md
- ../../09_DecisionTree/Firmware/BootFailed.md

---

# 1. Case Summary

## Case Name

Detector Failed to Boot After Firmware Upgrade

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

Firmware 升级完成后，探测器无法正常启动。

现场表现：

- Detector Offline
- SDK 无法发现设备
- Ping 不通
- 无法采图
- 指示灯状态异常（如适用）

升级前设备工作正常。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Firmware 已损坏（√）
- Detector 主板损坏（？）

FAE Initial Assessment：

先确认启动状态及升级过程，再判断是否属于 Firmware 损坏。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Detector Model
- [ ] Firmware Version（升级前）

## Upgrade Information

- [ ] Upgrade Package
- [ ] SDK Version
- [ ] Upgrade Log

## Logs

- [ ] SDK Log
- [ ] Detector Log

## Environment

- [ ] 电源状态
- [ ] 网线连接
- [ ] 网卡配置

---

# 6. FAE Investigation

## Step 1

确认 Detector 是否正常供电。

检查：

- 电源
- 指示灯
- 网口状态

结果：

供电正常。

---

## Step 2

重新断电。

等待 20 秒。

重新上电。

结果：

仍无法连接。

---

## Step 3

确认 Firmware Upgrade 使用的软件包。

检查：

- Firmware Version
- Release Package
- SDK Version

结果：

版本一致。

---

## Step 4

检查网络配置。

确认：

- IP
- Jumbo Frame
- 网卡状态

结果：

网络正常。

---

## Step 5

导出升级日志。

提交研发分析。

根据分析结果重新恢复 Firmware。

设备恢复正常。

---

# 7. Root Cause

Firmware 升级完成后启动过程异常，导致 Detector 无法正常初始化。

详细分析请参见：

- ../../07_FailureKnowledge/FirmwareFailure/BootFailed.md

---

# 8. Corrective Action

现场采取：

① 检查供电状态。

② 完整断电后重新启动。

③ 检查升级包版本。

④ 检查网络配置。

⑤ 导出 Upgrade Log。

⑥ 根据研发建议恢复 Firmware。

---

# 9. Verification

验证结果：

- Detector 正常启动。
- SDK 可正常连接。
- Firmware Version 正确。
- 图像采集恢复正常。

---

# 10. Preventive Action（CAPA）

建议：

① 使用正式 Release Package。

② 升级过程中禁止断电。

③ 升级完成后执行完整重启。

④ 保存升级日志。

⑤ 升级完成立即验证 Detector Online 状态。

---

# 11. Lessons Learned

## Technical

Boot Failed 不一定意味着 Firmware 已损坏，也可能是初始化过程异常。

## Diagnostic

优先确认供电、网络和启动状态，再分析 Firmware。

## Operation

升级后应立即验证 Detector 是否能够正常启动，而不是仅确认升级成功提示。

## Maintenance

建立 Firmware 升级记录，便于后续问题追溯。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 若 Firmware 升级完成后无法连接 Detector：
>
> 1. 先执行完整断电重启。
> 2. 检查 Firmware 与 SDK 是否匹配。
> 3. 导出 Upgrade Log。
> 4. 不要立即重复升级，应先定位失败原因。

---

# 13. Related Documents

Workflow：

- FirmwareUpgradeWorkflow.md

Failure Knowledge：

- BootFailed.md

Tools：

- FirmwareUpgrade.md

Decision Tree：

- BootFailed.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Boot Failed 现场案例，整理 Firmware 升级后无法启动的排查流程。 |