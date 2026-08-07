# DetectorAssistant

> Enterprise Knowledge Base for Flat Panel Detector Technical Support

Version: v1.0  
Status: Development Completed (Core Knowledge Base)

---

# 1. Project Overview

DetectorAssistant is an enterprise knowledge base designed for Flat Panel Detector (FPD) technical support.

It provides standardized technical documentation, troubleshooting workflows, decision trees, SOPs, case studies, error code references, and engineering knowledge to support installation, maintenance, calibration, diagnostics, and after-sales service.

The project aims to standardize technical knowledge, improve troubleshooting efficiency, reduce repetitive experience accumulation, and provide a unified technical reference platform for engineers.

---

# 2. Project Objectives

The objectives of DetectorAssistant are:

- Standardize detector technical documentation.
- Establish a unified troubleshooting methodology.
- Build reusable engineering knowledge.
- Reduce troubleshooting time.
- Improve first-time issue resolution rate.
- Preserve engineering experience.
- Support technical training.
- Provide AI-friendly structured knowledge.

---

# 3. Applicable Products

Current supported products include:

## Dental Series

- Pluto0001X
- Pluto0002X
- Pluto0900X

## Dynamic Detector Series

- Dynamic Medical Detector

## Mercu Series

- Mercu Detector Family

Future product families can be added without changing the project architecture.

---

# 4. Intended Users

This knowledge base is intended for:

- FAE (Field Application Engineers)
- Technical Support Engineers
- R&D Engineers
- Quality Engineers
- Manufacturing Engineers
- Service Engineers
- Internal Training Personnel

---

# 5. Knowledge Architecture

```
DetectorAssistant

├── 00_Project
├── 01_Product
├── 02_SDK
├── 03_Hardware
├── 04_Software
├── 05_Calibration
├── 06_Workflow
├── 07_FailureKnowledge
├── 08_ImageDiagnosis
├── 09_DecisionTree
├── 10_SOP
├── 11_Case
├── 12_ErrorCode
├── 13_Template
├── 14_Glossary
├── 15_Reference
├── 16_FAE
└── 17_Tools
```

---

# 6. Knowledge Organization

The knowledge base follows a layered architecture.

## Product Layer

Defines detector products and product-specific information.

## SDK Layer

Documents SDK architecture, APIs, initialization, acquisition, callbacks, licensing, and development interfaces.

## Hardware Layer

Describes detector hardware architecture, power systems, communication interfaces, TFT structure, generators, batteries, and sensors.

## Software Layer

Documents end-user software including iDetector, configuration tools, firmware utilities, licensing, networking, and application settings.

## Workflow Layer

Defines standardized engineering workflows.

## Failure Layer

Documents detector failures and troubleshooting knowledge.

## Decision Layer

Provides decision trees for rapid diagnosis.

## SOP Layer

Defines standardized operating procedures.

## Case Layer

Stores engineering case studies and field experience.

## Reference Layer

Provides quick-reference material for engineers.

---

# 7. Knowledge Relationships

Typical troubleshooting flow:

```
Problem

↓

Failure Knowledge

↓

Decision Tree

↓

Workflow

↓

Error Code

↓

Case

↓

Solution

↓

Verification
```

---

# 8. Document Standards

All documents follow unified standards:

- Markdown format
- English filenames
- One topic per document
- Cross-reference related documents
- Version controlled
- Structured headings
- Reusable content
- Traceable revisions

---

# 9. Naming Rules

General naming principles:

- Use PascalCase for filenames.
- Use English filenames.
- One document = one subject.
- Avoid abbreviations unless industry-standard.
- Keep naming consistent across modules.

Detailed rules are defined in:

- NamingConvention.md

---

# 10. Version Management

Project versions are managed using Semantic Versioning.

Example:

```
v1.0.0

Major.Minor.Patch
```

---

# 11. Maintenance Principles

Knowledge should be:

- Accurate
- Verifiable
- Reproducible
- Maintainable
- Traceable
- Consistent

Engineering experience should be documented as Case documents rather than modifying SOPs directly.

---

# 12. Related Documents

- VERSION.md
- ROADMAP.md
- CHANGELOG.md
- ProjectScope.md
- KnowledgeMap.md
- KnowledgeRelationship.md
- ObjectModel.md
- Ontology.md
- KnowledgeStandard.md
- NamingConvention.md
- EngineeringPrinciples.md

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| v1.0 | 2026-08-07 | Initial project documentation |