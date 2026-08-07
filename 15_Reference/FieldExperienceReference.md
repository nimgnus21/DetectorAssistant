# Field Experience Reference

> Version: v1.0
>
> Status: Draft
>
> Last Updated: 2026-08-06

---

# 1. Purpose

This document defines how field engineering experience is collected, classified, and incorporated into the DetectorAssistant knowledge base.

Field experience complements official documentation by recording real customer issues, engineering investigations, and validated solutions.

---

# 2. Experience Sources

Field experience may originate from:

- FAE Pre-sales Support
- FAE After-sales Support
- Customer On-site Service
- Remote Technical Support
- Factory Verification
- Internal Engineering Discussion

---

# 3. Knowledge Mapping

| Experience Type | Knowledge Base Module |
|-----------------|-----------------------|
| Communication Issue | 11_Case/Communication |
| Calibration Issue | 11_Case/Calibration |
| Firmware Issue | 11_Case/Firmware |
| Image Issue | 11_Case/Image |
| Customer Configuration | 11_Case/Customer |
| SDK Integration | 17_Tools |

---

# 4. Experience Record Standard

Every engineering experience should include:

- Product
- Firmware Version
- SDK Version (if applicable)
- Customer Environment
- Symptom
- Investigation
- Root Cause
- Corrective Action
- Verification Result
- Lessons Learned

---

# 5. Failure Classification

Each field experience should identify the primary failure category.

| Category | Description |
|----------|-------------|
| Detector Hardware | Internal hardware failure |
| Detector Firmware | Firmware issue |
| Detector Configuration | Detector parameter/configuration |
| SDK / Software | SDK or application issue |
| Customer Environment | Network, PC, OS, etc. |
| Third-party Equipment | Generator, Grid, Switch, Trigger, etc. |

---

# 6. Integration Rules

A field experience should not become a new document automatically.

Recommended integration priority:

1. Append to an existing Case document.
2. Update the corresponding Decision Tree if a new diagnostic path is identified.
3. Supplement Failure Knowledge if a new mechanism is confirmed.
4. Update Workflow if operating procedures change.
5. Add a Reply Template if a reusable customer response is formed.

---

# 7. Experience Quality Requirements

A field experience should:

- Be based on a real engineering case.
- Be technically verified.
- Avoid unsupported assumptions.
- Clearly distinguish observed facts from engineering conclusions.
- Be reusable for future troubleshooting.

---

# 8. Maintenance Rules

Review this reference when:

- New field experience categories emerge.
- Engineering troubleshooting methods change.
- Knowledge-base integration rules are updated.

---

# 9. Related Documents

- 11_Case/
- 09_DecisionTree/
- 07_FailureKnowledge/
- 06_Workflow/
- 13_Template/
- 16_KnowledgeAssets/FieldRecord/