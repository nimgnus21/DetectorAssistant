# OQC

Version: V1.0

Case ID: CASE-CUS-002

Module: 11_Case / Customer

Status: Released

Severity: ★★★☆☆

Typical Frequency: ★★★★☆

Applicable Products:

* Pluto Series
* Wired Detector
* Wireless Detector

Related Documents:

* ../../11_Case/Firmware/VersionMismatch.md
* ../../17_Tools/SDKTool/FirmwareUpgrade.md
* ../../10_FAE/OQCWorkflow.md
* ../../09_DecisionTree/Customer/OQC.md

---

# 1. Case Summary

## Case Name

OQC Firmware Version Verification Before Sample Delivery

---

# 2. Customer Information

Customer Type：

OEM Customer

Product：

Pluto1717

Operation：

OQC Inspection / Sample Delivery

---

# 3. Fault Description

客户要求安排样机送样。

在 OQC 检查过程中发现：

* Detector Firmware Version 与项目要求版本不一致。

客户希望直接发货。

---

# 4. Initial Customer Judgment

Customer Judgment：

* Detector 可以正常工作，可直接送样。

FAE Initial Assessment：

送样前必须确认 Firmware Version 是否符合项目要求。

---

# 5. Evidence Collection

## Detector Information

* [ ] Detector SN
* [ ] Detector Model
* [ ] Current Firmware Version
* [ ] FPGA Version（如适用）

## Software Information

* [ ] SDK Version
* [ ] Release Package Version

## OQC Records

* [ ] OQC 检查记录
* [ ] 项目版本要求
* [ ] 研发评审记录（如适用）

---

# 6. FAE Investigation

## Step 1

在 OQC 阶段读取当前 Firmware Version。

结果：

发现与项目要求版本不一致。

---

## Step 2

确认项目要求版本。

核对：

* Firmware
* SDK
* Release Package

---

## Step 3

联系研发确认版本兼容性。

重点确认：

* 是否允许使用当前版本。
* 是否存在已知风险。
* 是否必须统一版本。

---

## Step 4

根据研发意见完成评审。

结果：

当前版本不满足送样要求。

---

## Step 5

升级至指定 Firmware。

升级后重新验证：

* Firmware Version
* Detector Online
* 图像采集

确认正常后放行送样。

---

# 7. Root Cause

OQC 阶段发现 Detector Firmware Version 与项目要求不一致。

属于版本管理问题，而非产品故障。

---

# 8. Corrective Action

现场采取：

1. 确认当前 Firmware Version。
2. 联系研发进行版本评审。
3. 升级至指定版本。
4. 重新验证功能。
5. 更新 OQC 记录。

---

# 9. Verification

验证结果：

* Firmware Version 符合项目要求。
* Detector 通信正常。
* 图像采集正常。
* OQC 审核通过。
* 样机正常发货。

---

# 10. Preventive Action（CAPA）

建议：

1. OQC 增加 Firmware Version 必检项。
2. 建立 Firmware 与 SDK 对照表。
3. 送样前冻结版本。
4. 未经评审禁止使用非指定版本。

---

# 11. Lessons Learned

## Technical

Firmware 与 SDK 必须保持兼容。

## Diagnostic

VersionMismatch 不一定导致故障，但可能影响客户测试结果。

## Operation

OQC 是发现版本问题的最后关口，应在发货前完成确认。

## Maintenance

建立版本追溯记录，减少返工。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 送样前必须在 OQC 阶段确认：
>
> * Firmware Version
> * SDK Version
> * Release Package
>
> 若版本不一致，应联系研发确认并完成评审，不建议未经确认直接发货。

---

# 13. Related Documents

Firmware：

* VersionMismatch.md

Tools：

* FirmwareUpgrade.md

Decision Tree：

* OQC.md

FAE：

* OQCWorkflow.md

---

# 14. Revision History

| Version | Date    | Description                 |
| ------- | ------- | --------------------------- |
| V1.0    | 2026-08 | 建立 OQC 现场案例，规范送样前版本确认及评审流程。 |
