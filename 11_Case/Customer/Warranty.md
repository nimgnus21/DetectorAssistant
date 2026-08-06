# Warranty

Version: V1.0

Case ID: CASE-CUS-001

Module: 11_Case / Customer

Status: Released

Severity: ★★☆☆☆

Typical Frequency: ★★★★☆

Applicable Products:

- Pluto Series
- Wired Detector
- Wireless Detector

Related Documents:

- ../../10_FAE/CustomerCommunication/
- ../../09_DecisionTree/Customer/Warranty.md
- ../../12_FAQ/Warranty.md

---

# 1. Case Summary

## Case Name

Warranty Status Confirmation Before RMA

---

# 2. Customer Information

Customer Type：

Hospital / Dealer / OEM

Product：

Pluto Series Detector

Service Request：

Detector Repair

---

# 3. Fault Description

客户反馈：

Detector 出现异常，希望安排返厂维修。

在确认维修方案前，需要判断：

- 是否仍在保修期内。
- 是否符合保修条件。

---

# 4. Initial Customer Judgment

Customer Judgment：

- 设备仍在保修期，应免费维修。

FAE Initial Assessment：

先确认保修状态，再检查是否存在人为损坏。

---

# 5. Evidence Collection

## Device Information

- [ ] Detector SN
- [ ] Product Model
- [ ] Purchase Date（如适用）

## Appearance Inspection

- [ ] 外观照片（正面）
- [ ] 外观照片（背面）
- [ ] 边框照片
- [ ] 接口照片

## Damage Inspection

- [ ] 跌落痕迹
- [ ] 磕碰
- [ ] 外壳裂纹
- [ ] 拆机痕迹
- [ ] 液体侵入

---

# 6. FAE Investigation

## Step 1

确认 Detector SN。

查询 Warranty Information。

---

## Step 2

检查 Warranty Status。

判断：

- In Warranty
- Out of Warranty

---

## Step 3

检查外观。

重点确认：

- 人为损坏
- 跌落
- 拆机
- 液体损坏

---

## Step 4

综合判断。

若：

符合 Warranty 条件。

安排返厂。

否则：

按照 Out of Warranty 流程处理。

---

# 7. Root Cause

本案例属于 Warranty Status 判断，并非产品技术故障。

---

# 8. Corrective Action

现场采取：

① 查询 Warranty。

② 检查外观。

③ 收集照片。

④ 确认是否符合 Warranty。

⑤ 回复客户处理方案。

---

# 9. Verification

确认：

- Warranty Status 正确。
- 外观检查完成。
- 客户接受处理方案。

---

# 10. Preventive Action (CAPA)

建议：

① RMA 前必须确认 Warranty。

② 保留完整外观照片。

③ 明确记录人为损坏情况。

---

# 11. Lessons Learned

## Technical

Warranty 判断独立于技术故障分析。

## Diagnostic

不要仅依据客户描述判断 Warranty。

## Operation

先确认 Warranty，再安排返厂。

## Maintenance

保存外观照片，作为后续维修依据。

---

# 12. Field Experience

> **FAE 现场经验**
>
> 若设备仍处于保修期，可安排返厂检测。
>
> 但前提必须确认：
>
> - 外观无明显异常。
> - 无磕碰。
> - 无人为损坏。
> - 无拆机痕迹。
>
> 若存在上述情况，即使设备仍在保修期，也可能影响最终处理方案。
>
> 若设备已过保，一般建议客户更换新机或按售后维修流程处理。

---

# 13. Related Documents

Decision Tree：

- Warranty.md

FAE：

- CustomerCommunication

FAQ：

- Warranty.md

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Warranty 现场案例，规范保修状态确认及返厂流程。 |