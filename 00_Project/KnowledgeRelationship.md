# Knowledge Relationship

> DetectorAssistant Knowledge Architecture Specification

Project: DetectorAssistant

Version: v1.0.0

---

# 1. Purpose

This document defines the relationships between all knowledge domains within DetectorAssistant.

Unlike the directory structure, this document describes how knowledge flows, how documents depend on each other, how engineering activities are connected, and how information should be organized throughout the project.

The purpose is to ensure:

- Consistent knowledge organization
- Clear document dependencies
- Standardized cross-references
- Efficient engineering navigation
- AI-friendly knowledge retrieval

---

# 2. Knowledge Relationship Principles

Every document belongs to one primary Knowledge Domain.

Knowledge domains interact through standardized relationships.

DetectorAssistant defines the following relationship types.

| Relationship | Meaning |
|--------------|---------|
| Depends On | Requires another knowledge domain as a prerequisite |
| References | Uses another document as supporting information |
| Implements | Describes the implementation of another concept |
| Diagnoses | Identifies the cause of a problem |
| Resolves | Provides the solution to a problem |
| Verifies | Confirms whether a solution is successful |
| Generates | Produces data, logs, images or results |
| Describes | Defines concepts or structures |

Every relationship should be directional.

Example:

```
Calibration

Depends On

SDK
```

---

# 3. Overall Knowledge Dependency

The core engineering knowledge follows the dependency chain below.

```
Product

↓

Hardware

↓

Software

↓

SDK

↓

Calibration

↓

Workflow

↓

Failure Knowledge

↓

Decision Tree

↓

Case

↓

SOP

↓

Reference
```

Each module builds upon the previous layer.

---

# 4. Knowledge Domains

The knowledge base consists of seventeen domains.

| Module | Primary Responsibility |
|---------|------------------------|
| 00_Project | Project governance |
| 01_Product | Product knowledge |
| 02_SDK | Software interface |
| 03_Hardware | Detector hardware |
| 04_Software | Application software |
| 05_Calibration | Calibration principles |
| 06_Workflow | Engineering workflow |
| 07_FailureKnowledge | Failure mechanisms |
| 08_ImageDiagnosis | Image analysis |
| 09_DecisionTree | Troubleshooting path |
| 10_SOP | Standard operations |
| 11_Case | Engineering experience |
| 12_ErrorCode | Error interpretation |
| 13_Template | Standard templates |
| 14_Glossary | Terminology |
| 15_Reference | Quick reference |
| 16_FAE | Engineering experience |
| 17_Tools | Engineering utilities |

---

# 5. Module Dependency Matrix

| Module | Depends On | Referenced By |
|---------|------------|---------------|
| Product | — | Hardware, Workflow |
| Hardware | Product | SDK, FailureKnowledge |
| Software | Hardware | SDK, Workflow |
| SDK | Software | Calibration, Workflow, ErrorCode |
| Calibration | SDK | Workflow, SOP |
| Workflow | SDK, Calibration | SOP, Case |
| FailureKnowledge | Hardware, Workflow | DecisionTree |
| ImageDiagnosis | Hardware, Calibration | FailureKnowledge, Case |
| DecisionTree | FailureKnowledge | SOP, Case |
| SOP | Workflow, DecisionTree | FAE |
| Case | DecisionTree, SOP | FAE |
| ErrorCode | SDK | DecisionTree, SOP |
| Reference | All Modules | Engineers |

---

# 6. Engineering Knowledge Flow

DetectorAssistant organizes engineering knowledge according to the engineering lifecycle.

```
Product

↓

Installation

↓

Configuration

↓

Communication

↓

Calibration

↓

Image Acquisition

↓

Failure

↓

Diagnosis

↓

Repair

↓

Verification

↓

Maintenance
```

Knowledge is organized according to this sequence.

---

# 7. Troubleshooting Relationship

Standard troubleshooting follows this path.

```
Customer Problem

↓

FailureKnowledge

↓

DecisionTree

↓

Workflow

↓

ErrorCode

↓

Case

↓

SOP

↓

Verification
```

This is the recommended navigation path for all technical support activities.

---

# 8. Image Troubleshooting Relationship

For image-related issues, the recommended knowledge path is:

```
Image Abnormality

↓

ImageDiagnosis

↓

FailureKnowledge

↓

Hardware

↓

Calibration

↓

DecisionTree

↓

Case

↓

SOP

↓

Verification
```

---

# 9. Communication Troubleshooting Relationship

Communication issues follow the relationship below.

```
Communication Failure

↓

Hardware

↓

Software

↓

SDK

↓

DecisionTree

↓

Workflow

↓

Case

↓

Resolution
```

---

# 10. Calibration Relationship

Calibration knowledge is organized as follows.

```
SDK

↓

Calibration

↓

Workflow

↓

ErrorCode

↓

Case

↓

SOP
```

---

# 11. Engineering Document Relationships

Every engineering document should follow the relationship below.

```
Concept

↓

Workflow

↓

Failure

↓

DecisionTree

↓

Case

↓

SOP

↓

Reference
```

Documents should not exist independently.

---

# 12. Cross-Reference Rules

Each document should:

- Belong to exactly one primary module.
- Reference related documents instead of duplicating content.
- Include a Related Documents section.
- Maintain one authoritative source for each topic.

Duplicate knowledge should be avoided.

---

# 13. AI Retrieval Relationships

DetectorAssistant is designed to support AI-assisted retrieval.

Example:

User asks:

```
Detector cannot connect.
```

Recommended retrieval sequence:

```
Communication

↓

SDK

↓

ErrorCode

↓

DecisionTree

↓

Case

↓

SOP
```

---

User asks:

```
Vertical line artifact
```

Recommended retrieval sequence:

```
ImageDiagnosis

↓

FailureKnowledge

↓

Hardware

↓

Calibration

↓

Case

↓

SOP
```

---

User asks:

```
Calibration failed
```

Recommended retrieval sequence:

```
Calibration

↓

Workflow

↓

ErrorCode

↓

DecisionTree

↓

Case
```

---

# 14. Knowledge Maintenance Rules

Every new document shall:

- Belong to one knowledge domain.
- Have a single primary topic.
- Reference related documents.
- Be referenced by at least one higher-level document.
- Avoid circular references.
- Avoid duplicated content.

---

# 15. Future Expansion

Future detector products, SDK versions, software modules, and engineering knowledge shall extend the existing relationship model rather than introducing new relationship types whenever possible.

The knowledge architecture should remain stable across future versions.

---

# Related Documents

- KnowledgeMap.md
- ObjectModel.md
- Ontology.md
- EngineeringPrinciples.md
- KnowledgeStandard.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial knowledge relationship architecture |