# ParameterRecovery

Version: V1.0

Case ID: CASE-FW-004

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
- ../../17_Tools/SDKTool/CalibrationTools.md
- ../../06_Workflow/FirmwareUpgradeWorkflow.md
- ../../07_FailureKnowledge/FirmwareFailure/ParameterRecovery.md
- ../../09_DecisionTree/Firmware/ParameterRecovery.md

---

# 1. Case Summary

## Case Name

Factory Parameter Recovery After Firmware Upgrade

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto1717

Operation：

Firmware Upgrade

Application：

Factory Maintenance / OQC / FAE On-site Support

---

# 3. Fault Description

客户反馈：

Firmware 已成功升级。

Detector 可以正常连接。

但是升级完成后发现：

- Detector 参数恢复默认
- 网络参数异常
- 校准参数失效
- 图像无法正常输出（如适用）
- 与升级前配置不一致

客户认为：

Firmware 升级失败。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Firmware Upgrade Failed（√）
- Detector Hardware Failure（×）

FAE Initial Assessment：

Firmware 已成功升级。

优先检查 Factory Parameter 是否恢复。

---

# 5. Evidence Collection

## Detector Information

- [ ] Detector SN
- [ ] Detector Model
- [ ] Firmware Version
- [ ] FPGA Version（如适用）

## Parameter Backup

- [ ] Factory Parameter Backup
- [ ] Calibration Backup
- [ ] Network Configuration Backup

## Software Information

- [ ] SDK Version
- [ ] Release Package Version

## Verification

- [ ] Detector Communication
- [ ] Image Acquisition
- [ ] Calibration Status

---

# 6. FAE Investigation

## Step 1

确认 Firmware Upgrade 已完成。

检查：

- Firmware Version
- Upgrade Log

结果：

Firmware 升级成功。

---

## Step 2

检查 Detector 参数。

确认：

- Network Configuration
- Detector Configuration
- Calibration Information

结果：

参数恢复为默认值。

---

## Step 3

导入升级前备份的 Factory Parameter。

恢复：

- Detector Configuration
- Network Parameters
- Calibration Parameters（如适用）

---

## Step 4

重新启动 Detector。

等待系统初始化完成。

---

## Step 5

重新连接 SDK。

验证：

- Detector Online
- Image Acquisition
- Parameter Status

确认恢复正常。

---

# 7. Root Cause

Firmware 升级后未恢复 Factory Parameter，导致 Detector 配置恢复默认值。

Firmware 程序正常，但运行参数缺失。

详细分析请参见：

- ../../07_FailureKnowledge/FirmwareFailure/ParameterRecovery.md

---

# 8. Corrective Action

现场采取：

① 导入升级前备份的 Factory Parameter。

② 检查网络配置。

③ 检查 Calibration 数据。

④ 重启 Detector。

⑤ 验证 Detector 通信及采图功能。

---

# 9. Verification

验证结果：

- Detector 正常连接。
- Factory Parameter 恢复。
- Calibration 状态正常。
- 图像采集恢复正常。
- 客户确认功能恢复。

---

# 10. Preventive Action (CAPA)

建议：

① Firmware 升级前必须备份 Factory Parameter。

② Parameter Backup 与 Firmware Package 一并保存。

③ Firmware 升级完成后，立即恢复 Factory Parameter。

④ 建立 Firmware、Parameter、Calibration 三者版本对应关系。

⑤ OQC 增加 Parameter Verification 检查项。

---

# 11. Lessons Learned

## Technical

Firmware 与 Factory Parameter 属于两个独立对象。

升级 Firmware 不会自动恢复原有配置。

## Diagnostic

升级成功但功能异常时，应优先确认 Parameter，而不是重新升级 Firmware。

## Operation

Firmware 升级流程应包含：

- 参数备份
- Firmware Upgrade
- 参数恢复
- 功能验证

缺一不可。

## Maintenance

建议统一管理：

- Firmware
- Factory Parameter
- Calibration Data

确保版本对应、备份完整。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 根据现场维护经验，Firmware 升级前必须先保存 Factory Parameter。
>
> 升级完成后，应恢复备份参数，并验证网络配置、校准状态及图像采集功能。
>
> 若忽略 Parameter Recovery，虽然 Firmware 已升级成功，但 Detector 可能无法按照升级前配置正常工作。

---

# 13. Related Documents

Workflow：

- FirmwareUpgradeWorkflow.md

Failure Knowledge：

- ParameterRecovery.md

Tools：

- FirmwareUpgrade.md
- CalibrationTools.md

Decision Tree：

- ParameterRecovery.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Parameter Recovery 现场案例，规范 Firmware 升级后的参数恢复流程。 |