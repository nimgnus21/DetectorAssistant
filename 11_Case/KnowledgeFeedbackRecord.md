# Case Knowledge Feedback Record

> Module: 11_Case
>
> Purpose: Record how a completed real case changes, or does not change, the knowledge base.

---

# Case Reference

- Case ID:
- Case Title:
- Status:
- Product / Model:
- Date:
- Reviewer:

---

# 1. Verified Facts Extracted from the Case

Record only facts supported by the Case evidence.

- Symptom:
- Environment/version:
- Diagnostic discriminator:
- Verified root cause or verified treatment:
- Verification result:

---

# 2. Knowledge Feedback Review

| Layer | Existing Entry Checked | Finding | Action | Target File |
|---|---|---|---|---|
| FailureKnowledge |  |  | Update / No update required |  |
| DecisionTree |  |  | Update / No update required |  |
| SOP |  |  | Update / No update required |  |
| Tools |  |  | Update / No update required |  |
| ErrorCode |  |  | Update / No update required |  |
| Glossary |  |  | Update / No update required |  |
| Index |  |  | Update / No update required |  |

---

# 3. Update Boundary

Only promote information that meets the evidence threshold of the target layer.

- `Verified` facts may update formal diagnostic knowledge.
- `Resolved` treatment may be added as an operational recovery path, while root cause remains explicitly unconfirmed.
- `Unresolved` and `Hypothesis` information may remain in the Case but must not be promoted as formal conclusions.

---

# 4. Update Execution

For each required update:

- [ ] Target file modified
- [ ] Related links added or updated
- [ ] Index checked
- [ ] Case back-link added where appropriate
- [ ] Product/version scope recorded

For each no-update decision:

- [ ] Existing knowledge was checked
- [ ] Reason for no update recorded

---

# 5. Final Decision

- [ ] Knowledge updated
- [ ] No update required
- [ ] Additional evidence required before promotion

Decision notes:

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.0 | 2026-08-10 | Established standard case-to-knowledge feedback record |