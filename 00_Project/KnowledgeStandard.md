# Knowledge Standard

> DetectorAssistant Knowledge Documentation Standard

Project: DetectorAssistant

Version: v1.0.0

---

# 1. Purpose

This document defines the documentation standards for DetectorAssistant.

The objective is to ensure that all engineering knowledge is:

- Consistent
- Accurate
- Reusable
- Maintainable
- Traceable
- AI-readable

Every document included in DetectorAssistant shall comply with this standard.

---

# 2. Design Principles

DetectorAssistant follows the following knowledge principles.

- Single Source of Truth (SSOT)
- One Document, One Topic
- Layered Knowledge Architecture
- Modular Documentation
- Reusable Content
- Cross-Referenced Knowledge
- Version Controlled Documentation

---

# 3. Knowledge Classification

Engineering knowledge is classified into the following categories.

| Category | Description |
|----------|-------------|
| Project | Project governance |
| Product | Product information |
| Hardware | Hardware architecture |
| Software | Software operation |
| SDK | Development interfaces |
| Calibration | Calibration principles |
| Workflow | Engineering processes |
| Failure | Failure analysis |
| Image | Image diagnosis |
| DecisionTree | Troubleshooting logic |
| SOP | Standard procedures |
| Case | Engineering cases |
| ErrorCode | Error definitions |
| Template | Standard templates |
| Glossary | Engineering terminology |
| Reference | Quick references |
| Tool | Engineering utilities |

Every document shall belong to one primary category.

---

# 4. One Document, One Topic

Each Markdown document shall describe one primary engineering topic.

Correct examples:

- Offset Calibration
- Detector Connection
- Firmware Upgrade
- Detector Busy
- Image Noise

Incorrect examples:

- Calibration and Firmware
- SDK + Image + Network
- Installation and Troubleshooting

A document should answer one engineering question.

---

# 5. Knowledge Granularity

Documentation should be written at a consistent level of detail.

Each document should:

- Focus on one concept.
- Avoid excessive fragmentation.
- Avoid combining unrelated subjects.
- Be reusable by other documents.

---

# 6. Standard Document Structure

Unless otherwise required, documents should follow the structure below.

```
Title

↓

Purpose

↓

Scope

↓

Description

↓

Procedure / Explanation

↓

Notes

↓

Related Documents

↓

Revision History
```

Specialized modules (SOP, Case, ErrorCode, Template) may extend this structure while preserving consistency.

---

# 7. Writing Style

Documents shall be:

- Technical
- Objective
- Concise
- Consistent
- Action-oriented

Avoid:

- Personal opinions
- Marketing language
- Ambiguous wording
- Informal expressions

Preferred wording:

- Verify
- Configure
- Initialize
- Generate
- Acquire
- Connect
- Calibrate

---

# 8. Terminology Standard

Engineering terminology shall:

- Use English as the canonical identifier.
- Be defined in the Glossary.
- Have one semantic meaning.
- Remain consistent across all modules.

Preferred example:

```
Offset
```

Do not alternate between:

```
Offset Image
Offset File
Offset Calibration
```

unless they represent different engineering concepts.

---

# 9. Cross-Reference Rules

Documents should reference related documents instead of duplicating information.

Each document should include a **Related Documents** section.

Recommended references:

- Upstream knowledge
- Downstream procedures
- Related workflows
- Relevant cases
- Applicable SOPs

---

# 10. Duplication Policy

Duplicate technical content is prohibited.

If multiple documents require the same explanation:

- Keep one authoritative source.
- Reference the original document.
- Do not copy content.

---

# 11. File Organization

Each document shall:

- Belong to one module.
- Have one owner.
- Have one primary purpose.

Documents shall not exist outside the defined project architecture.

---

# 12. Version Control

Every document shall contain:

- Revision History
- Version
- Update Date

Major technical revisions should also be recorded in `CHANGELOG.md`.

---

# 13. Quality Requirements

Before a document is considered complete, it shall satisfy the following requirements.

| Requirement | Description |
|-------------|-------------|
| Accuracy | Technically correct |
| Completeness | Covers the intended topic |
| Consistency | Matches project standards |
| Traceability | Version and history recorded |
| Reusability | Can be referenced by other documents |
| Maintainability | Easy to update |
| Readability | Clear structure and terminology |

---

# 14. AI Compatibility

Documents should be optimized for AI-assisted retrieval.

Recommendations:

- One topic per document.
- Descriptive headings.
- Consistent terminology.
- Clear hierarchical structure.
- Explicit relationships.
- Minimal ambiguity.

Avoid relying on context that exists only in another document without providing a reference.

---

# 15. Review Process

Engineering documents should be reviewed in the following order.

```
Author

↓

Technical Review

↓

Consistency Review

↓

Knowledge Integration

↓

Release
```

---

# 16. Maintenance Rules

When updating existing documents:

- Preserve document purpose.
- Avoid breaking existing references.
- Update the revision history.
- Review related documents if terminology changes.
- Record significant project-wide changes in `CHANGELOG.md`.

---

# 17. Document Completion Checklist

A document is considered complete when:

- [ ] The scope is clearly defined.
- [ ] The content focuses on one topic.
- [ ] Terminology follows the Glossary.
- [ ] Related Documents are included.
- [ ] Revision History is updated.
- [ ] Duplicate content has been avoided.
- [ ] Formatting complies with project standards.

---

# Related Documents

- NamingConvention.md
- EngineeringPrinciples.md
- KnowledgeMap.md
- KnowledgeRelationship.md
- ObjectModel.md
- Ontology.md
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial documentation standard established |