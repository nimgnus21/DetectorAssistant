# Case Index

> 本索引用于定位真实现场、实验室、培训或内部验证案例，并区分已验证结论与未确认记录。

---

# Case Usage Rule

Case 必须记录真实问题处理过程。

通用故障现象、排查思路和未确认根因不应伪装成已解决 Case，应优先进入：

- `07_FailureKnowledge`
- `09_DecisionTree`
- `10_SOP`

只有在至少具备“现象 + 实际排查过程 + 当前处理或确认结果 + 验证结果”时，才建立正式 Case Record。

Case 状态使用：

- `Verified`
- `Resolved`
- `Unresolved`
- `Hypothesis`
- `Archived`

详细准入规则见：[Case Admission Checklist](../../11_Case/CaseAdmissionChecklist.md)。

---

# Search Before Create

新增 Case 前按以下顺序检索：

```text
Symptom / Model / ErrorCode / Version
        ↓
Existing Case
        ↓
FailureKnowledge
        ↓
DecisionTree
        ↓
SOP / Tool
```

检索结果：

- 已有同一根因和处理路径 → 优先更新已有 Case；
- 同一现象但环境/版本/根因不同 → 创建新 Case 并互相链接；
- 没有匹配 Case → 创建 `Case Candidate`，状态不得自动设为 `Verified`。

---

# Case Closure Checklist

新增或关闭 Case 前确认：

- [ ] Case ID 和主分类
- [ ] 探测器型号
- [ ] 现场现象
- [ ] 复现条件或发生条件
- [ ] 已执行实际排查
- [ ] 每一步的实际结果
- [ ] 当前状态证据
- [ ] 最终根因或最终处理结果
- [ ] 修复 / 变化验证结果
- [ ] 必要的图像 / RAW / Log / 版本信息或不可用说明
- [ ] Knowledge Feedback Review 完成

---

# Image Cases

入口目录：`11_Case/Image/`

与图像横纹相关时，先检查：

- `09_DecisionTree/Image/HorizontalLine.md`
- `07_FailureKnowledge/ImageFailure/InterferenceStripe.md`
- `07_FailureKnowledge/ImageFailure/PacketLoss.md`
- `07_FailureKnowledge/ImageFailure/CalibrationStripe.md`
- `07_FailureKnowledge/ImageFailure/DefectiveBar.md`

如果没有真实现场验证结果，只创建 `Case Candidate` 或 `Unresolved` 记录，不建立虚构的 Verified Case。

---

# Knowledge Feedback

每个 `Verified` 或 `Resolved` Case 必须完成一次：

[Case Knowledge Feedback Record](../../11_Case/KnowledgeFeedbackRecord.md)

检查：

- `07_FailureKnowledge`
- `09_DecisionTree`
- `10_SOP`
- `12_ErrorCode`
- `14_Glossary`
- `17_Tools`
- `00_Project/Index`

每项都必须记录：

- `Update`
- 或 `No update required`

`Hypothesis` 和 `Unresolved` 不得直接反向升级为正式根因知识。

---

# Case Index Maintenance

新增 `Verified`、`Resolved` 或具有长期参考价值的 `Unresolved` Case 时，在对应分类下增加索引条目。

每个索引条目建议包含：

```text
Case ID | Product | Symptom | Status | Version Scope | Link
```

避免复制 Case 内容；Index 仅作为检索入口。

---

# References

- [Case Admission Checklist](../../11_Case/CaseAdmissionChecklist.md)
- [Knowledge Feedback Record](../../11_Case/KnowledgeFeedbackRecord.md)
- [Case Template](../Templates/CaseTemplate.md)
- [11_Case README](../../11_Case/README.md)
