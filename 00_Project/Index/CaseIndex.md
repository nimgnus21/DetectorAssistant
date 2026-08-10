# Case Index

> 本索引用于定位已确认并完成验证的真实现场案例。

---

# Case Usage Rule

Case 必须记录真实问题处理过程。

通用故障现象、排查思路和未确认根因不应伪装成已解决 Case，应优先进入：

- `07_FailureKnowledge`
- `09_DecisionTree`
- `10_SOP`

只有在至少具备“现象 + 排查过程 + 最终处理或确认结果 + 验证结果”时，才建立正式 Case。

---

# Image Cases

入口目录：`11_Case/Image/`

与图像横纹相关时，先检查：

- `09_DecisionTree/Image/HorizontalLine.md`
- `07_FailureKnowledge/ImageFailure/InterferenceStripe.md`
- `07_FailureKnowledge/ImageFailure/PacketLoss.md`
- `07_FailureKnowledge/ImageFailure/CalibrationStripe.md`
- `07_FailureKnowledge/ImageFailure/DefectiveBar.md`

---

# Case Closure Checklist

新增 Case 前确认：

- [ ] 探测器型号
- [ ] 现场现象
- [ ] 复现条件
- [ ] 已执行排查
- [ ] 最终根因或最终处理结果
- [ ] 修复验证结果
- [ ] 必要的图像 / RAW / Log / 版本信息

---

# Knowledge Feedback

每个新 Case 完成后检查是否需要同步更新：

- `07_FailureKnowledge`
- `09_DecisionTree`
- `10_SOP`
- `12_ErrorCode`
- `14_Glossary`
