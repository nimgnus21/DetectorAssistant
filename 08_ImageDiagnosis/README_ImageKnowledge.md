# Image Knowledge Workflow

异常图像进入知识库时，按以下闭环执行：

```text
异常图像
→ Phenomenon
→ Feature Extraction
→ Candidate Causes
→ Evidence Collection
→ Verification
→ Root Cause
→ Resolution
→ Knowledge Feedback
```

## 重要规则

- 单图只确认现象，不直接确认根因。
- `Read Channel / Gate Channel / Channel / Hardware` 必须有证据后才能升级。
- RAW 是判断 Detector-side 与后处理/显示侧问题的重要分界证据。
- 新图片必须与现有现象条目匹配；如果现象无法匹配，先新增现象，不要强行归类。
- 已验证 Case 才能成为 Confirmed Knowledge。
- 新知识必须反哺 FailureKnowledge、DecisionTree 或 Case。
