# Case Template

> Use for real customer, field, laboratory, training, or internal verification events.
>
> Before closing the Case, complete [Case Admission Checklist](../../11_Case/CaseAdmissionChecklist.md) and [Knowledge Feedback Record](../../11_Case/KnowledgeFeedbackRecord.md).

---

# 1. 基本信息

- Case ID:
- Case Title:
- 主分类: Communication / Calibration / Image / Firmware / Software / Customer
- Status: `Hypothesis` / `Unresolved` / `Resolved` / `Verified` / `Archived`
- 产品型号:
- SN: （如允许记录）
- 客户 / 项目: （如允许记录）
- 日期:
- 来源: Customer / Field / Lab / Training / Internal Verification
- 软件版本:
- SDK 版本:
- 固件版本:
- 影响范围:

## Status Rule

- `Verified`: 根因或处理机制已验证。
- `Resolved`: 问题恢复，但根因未完全确认。
- `Unresolved`: 已完成实际排查，但问题未解决。
- `Hypothesis`: 仅有推断，不得作为正式技术结论。
- `Archived`: 历史记录，不作为当前优先方案。

---

# 2. 问题现象

- 客户描述:
- 实际现象:
- 首次发生时间:
- 是否稳定复现:
- 影响程度:

---

# 3. 现场环境

- 连接方式:
- 工作模式:
- 网络环境:
- 曝光 / 使用条件:
- 相关配置:
- 已执行操作:

---

# 4. 知识检索记录

在开始排查前记录已检查的知识入口。

- Existing Case:
- FailureKnowledge:
- DecisionTree:
- SOP:
- ErrorCode:
- Tool:

检索结论:

- [ ] 已存在匹配 Case，复用现有经验
- [ ] 未发现匹配 Case，创建新 Case Candidate
- [ ] 存在相关知识，但当前现象/环境存在实质差异

---

# 5. 排查过程

仅记录实际执行过的步骤和观察结果。

| Step | 检查项 / Action | 实际结果 | Evidence | 结论 / 下一分支 |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |

---

# 6. 根因 / 当前结论

## Verified Root Cause

仅在 `Verified` 时填写：

- Root Cause:
- Evidence:
- Reproduction / Confirmation Method:

## If Not Verified

- Root Cause: `Pending Confirmation` or `Not Fully Confirmed`
- Hypothesis:
- Evidence Gap:

不得将推测写为最终结论。

---

# 7. 处理措施

- Action:
- Configuration / File / Version Change:
- Recovery Boundary / Preconditions:

---

# 8. 验证结果

- 验证方法:
- 验证结果:
- 原现象是否消失 / 按预期变化:
- 是否完成受控复测:
- 最终状态:

---

# 9. 关联知识

优先链接到具体文件。

- FailureKnowledge:
- DecisionTree:
- SOP:
- Tool:
- ErrorCode:
- Related Case:

---

# 10. 附件与记录

- RAW Image:
- Corrected Image:
- Dark / Offset / Gain / Defect Evidence:
- Debug / Detector Log:
- Screenshot / Photo:
- Network Capture:
- Version / Configuration Record:

Unavailable evidence:

---

# 11. Knowledge Feedback

按照 [Knowledge Feedback Record](../../11_Case/KnowledgeFeedbackRecord.md) 逐项检查。

| Layer | Checked File | Result | Action / Reason |
|---|---|---|---|
| FailureKnowledge |  | Update / No update required |  |
| DecisionTree |  | Update / No update required |  |
| SOP |  | Update / No update required |  |
| Tools |  | Update / No update required |  |
| ErrorCode |  | Update / No update required |  |
| Glossary |  | Update / No update required |  |
| Index |  | Update / No update required |  |

---

# 12. Case Closure

- [ ] Admission checklist completed
- [ ] Status evidence satisfied
- [ ] Evidence package preserved or absence recorded
- [ ] Knowledge feedback reviewed
- [ ] Required repository updates completed
- [ ] Case Index updated or no-update decision recorded

---

# Revision History

| Version | Date | Description |
|---|---|---|
| V1.1 | 2026-08-10 | Added Case status gate, knowledge retrieval record, evidence discipline and mandatory feedback closure |
| V1.0 | 2026-08 | Initial template |