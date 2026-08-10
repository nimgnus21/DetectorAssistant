# Case Admission Checklist

> Module: 11_Case
>
> Purpose: Prevent theoretical troubleshooting records from being published as verified field cases.

---

# 1. When to Create a Case Candidate

Create a Case Candidate when all of the following are true:

- an actual customer, field, laboratory, training, or internal verification event occurred;
- the problem can be identified by a concrete symptom or event;
- at least one real diagnostic action or observation exists;
- the record may be useful for future technical support.

A Case Candidate may be `Unresolved`, `Hypothesis`, `Resolved`, or `Verified`.

Do not wait until the root cause is known before recording a real support event.

---

# 2. Admission Checklist

## Identity

- [ ] Case ID assigned
- [ ] Main category selected
- [ ] Product model recorded
- [ ] Date/source recorded
- [ ] SN/customer/project recorded when permitted

## Symptom

- [ ] Customer/laboratory description preserved
- [ ] Actual observed phenomenon recorded
- [ ] First occurrence or reproduction condition recorded when known
- [ ] Impact recorded

## Environment

- [ ] SDK version recorded when relevant
- [ ] Firmware version recorded when relevant
- [ ] Connection/mode/configuration recorded when relevant
- [ ] Exposure/use condition recorded when relevant

## Diagnostic Evidence

- [ ] Actual diagnostic steps recorded in chronological order
- [ ] Each step has an observed result
- [ ] Logs/images/RAW/screenshots preserved or explicitly unavailable
- [ ] Unsupported assumptions separated from verified facts

## Outcome

- [ ] Current status selected: `Hypothesis` / `Unresolved` / `Resolved` / `Verified` / `Archived`
- [ ] Root cause marked only if verified
- [ ] Treatment recorded if applied
- [ ] Objective verification result recorded

---

# 3. Status Gate

## Hypothesis

Use when a possible cause exists but has not been verified.

Required wording:

```text
Root Cause: Pending Confirmation
Hypothesis: <candidate cause>
Evidence Gap: <what is still required>
```

Do not use this status as a source for formal FailureKnowledge, DecisionTree, SOP, or ErrorCode conclusions.

## Unresolved

Use when real troubleshooting was performed but the problem remains unresolved.

Required additions:

- completed diagnostic branches;
- evidence collected;
- next diagnostic action;
- escalation requirement if applicable.

## Resolved

Use when the symptom was removed or operation recovered, but the root cause remains uncertain.

Required wording:

```text
Treatment: <what restored operation>
Root Cause: Not fully confirmed
Verification: <objective result>
```

## Verified

Use only when the root cause or treatment mechanism has been demonstrated through reproducible field/laboratory evidence.

Minimum verification:

- correction applied;
- original symptom removed or changed as expected;
- controlled retest completed where practical;
- evidence recorded.

## Archived

Use for obsolete historical cases. The reason for archival must be recorded.

---

# 4. Duplicate Check

Before creating a new Case, search:

1. `11_Case` for the same model/symptom/error code;
2. `00_Project/Index/CaseIndex.md`;
3. related `07_FailureKnowledge` and `09_DecisionTree` entries.

If a matching Case exists:

- update the existing Case when the same root cause and treatment are confirmed;
- create a separate Case when environment, version, root cause, or treatment materially differs;
- link related Cases instead of copying the same narrative.

---

# 5. Knowledge Feedback Gate

For every `Verified` or `Resolved` Case, review each item explicitly:

| Knowledge Layer | Review Question | Result |
|---|---|---|
| FailureKnowledge | Is there a new symptom or failure mechanism? | Update / No update required |
| DecisionTree | Is there a new diagnostic branch or discriminator? | Update / No update required |
| SOP | Does the standard procedure need a new step or evidence rule? | Update / No update required |
| Tools | Is a tool newly required or missing usage guidance? | Update / No update required |
| ErrorCode | Is there a useful error/event/version mapping? | Update / No update required |
| Glossary | Is a new term or definition required? | Update / No update required |
| Index | Is a new search entry required? | Update / No update required |

A result of `No update required` is valid but must be recorded.

---

# 6. Case Closure Output

A closed Case should leave four outputs:

```text
Case Record
    +
Evidence Package
    +
Knowledge Feedback Record
    +
Index Update or No-Update Record
```

If any output is missing, the Case may be resolved operationally but is not yet a complete knowledge-base feedback item.

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.0 | 2026-08-10 | Established executable Case admission and knowledge feedback gates |