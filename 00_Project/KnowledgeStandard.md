# Knowledge Standard

> Version: v2.0
>
> Status: Active
>
> Scope: Entire DetectorAssistant Knowledge Base

---

# 1. Purpose

This document defines the governance rules for the DetectorAssistant knowledge base.

Its objectives are to:

- Ensure document consistency.
- Improve maintainability.
- Establish knowledge traceability.
- Standardize engineering documentation.
- Prevent duplicated knowledge.

This document is the highest-level writing and maintenance standard within DetectorAssistant.

---

# 2. Knowledge Architecture

DetectorAssistant adopts a layered knowledge architecture.

```
Project Governance

↓

Product Knowledge

↓

Workflow

↓

Failure Knowledge

↓

Image Diagnosis

↓

Decision Tree

↓

Case

↓

Tool

↓

Reference

↓

Knowledge Assets
```

Each layer has a unique responsibility.

Knowledge duplication between layers should be avoided.

---

# 3. Document Responsibility

Each document shall answer only one primary question.

| Module | Primary Responsibility |
|---------|------------------------|
| Product | What is it? |
| Hardware | How is it built? |
| Workflow | How to perform it? |
| Failure Knowledge | Why does it happen? |
| Image Diagnosis | What does it look like? |
| Decision Tree | How to troubleshoot it? |
| Case | What happened in the field? |
| Tool | How to use the tool? |
| Reference | Where is the source? |
| Template | How to write it? |

---

# 4. Knowledge Lifecycle

Every document follows the same lifecycle.

```
Create

↓

Review

↓

Release

↓

Maintain

↓

Archive

↓

Retire
```

Documents shall never skip the review process.

---

# 5. Document Classification

Knowledge is classified into:

- Official Knowledge
- Engineering Knowledge
- Field Experience
- Reference Information
- Supporting Assets

Each document shall belong to only one primary category.

---

# 6. Naming Rules

Document names shall:

- Use PascalCase.
- Be concise.
- Represent one concept only.
- Avoid abbreviations unless officially defined.

Examples:

ConnectionFailed.md

GhostCorrection.md

CalibrationWorkflow.md

SDKReference.md

---

# 7. Source Traceability

Every engineering conclusion should be traceable.

Recommended source priority:

1. Official Documentation
2. Internal Training
3. Engineering Verification
4. Field Experience

Unsupported assumptions shall not be recorded as engineering facts.

---

# 8. Related Documents

Documents should reference related knowledge instead of duplicating content.

Recommended relationship:

Case

↓

Decision Tree

↓

Workflow

↓

Failure Knowledge

↓

Tool

↓

Reference

Cross-module navigation should always use references rather than repeated explanations.

---

# 9. Field Experience Rules

Field Experience should:

- Originate from real engineering activities.
- Be technically verified.
- Record facts before conclusions.
- Distinguish symptoms from root causes.
- Be appended to existing Case documents whenever possible.

Creating a new Case document should be the exception rather than the default.

---

# 10. Review Rules

Documents should be reviewed when:

- SDK version changes.
- Firmware version changes.
- Product specification changes.
- Workflow changes.
- New engineering experience is accumulated.

---

# 11. Version Management

Every document should include:

- Version
- Status
- Last Updated

Major revisions should be recorded in CHANGELOG.md.

---

# 12. Maintenance Principles

DetectorAssistant follows the following principles:

- Single Source of Truth
- Minimum Duplication
- Engineering First
- Traceable Knowledge
- Continuous Improvement
- Reusable Experience

---

# 13. Quality Checklist

Before publishing, verify:

□ Scope is clear.

□ No duplicated knowledge.

□ Terminology is consistent.

□ Related documents are linked.

□ Sources are traceable.

□ Engineering conclusions are verified.

□ Formatting follows the template.

---

# 14. Governance

Knowledge ownership belongs to the engineering team.

Knowledge contributors should:

- Follow the standard.
- Maintain consistency.
- Update references.
- Preserve engineering traceability.

Knowledge governance takes precedence over document quantity.

---

# 15. Related Documents

- SystemWritingStandard.md
- NamingConvention.md
- KnowledgeRelationship.md
- Ontology.md
- ProjectScope.md
- CHANGELOG.md