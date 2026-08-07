# Knowledge Map

> DetectorAssistant Knowledge Architecture Map

Project: DetectorAssistant

Version: v1.0.0

---

# 1. Purpose

This document provides a high-level view of the DetectorAssistant knowledge architecture.

It defines how engineering knowledge is organized, how different knowledge domains interact, and where engineers should locate specific technical information.

This document serves as the primary navigation entry for the entire knowledge base.

---

# 2. Knowledge Architecture

```
                            DetectorAssistant
                                     │
 ┌───────────────────────────────────┼────────────────────────────────────┐
 │                                   │                                    │
Project                        Engineering                         Support Knowledge
Architecture                    Knowledge                              Resources
 │                                   │                                    │
 │                                   │                                    │
00_Project                     01~08 Modules                      09~17 Modules
```

---

# 3. Knowledge Domains

DetectorAssistant is divided into seventeen major knowledge domains.

---

## 00_Project

Project governance and architecture.

Contains:

- Project documentation
- Version management
- Knowledge standards
- Naming conventions
- Knowledge model
- Ontology
- Roadmap

Purpose

Defines **how the knowledge base is built**.

---

## 01_Product

Product knowledge.

Contains

- Product families
- Product specifications
- Product differences
- Product compatibility

Purpose

Defines **what products exist**.

---

## 02_SDK

Software Development Kit documentation.

Contains

- SDK Architecture
- Initialization
- Device
- Acquisition
- Callback
- Configuration
- Image
- Calibration API
- Firmware API
- Generator API
- License API

Purpose

Defines **how software communicates with detectors**.

---

## 03_Hardware

Detector hardware architecture.

Contains

- TFT
- FPGA
- ADC
- Battery
- Ethernet
- Trigger
- Power
- Sensors
- WiFi

Purpose

Defines **how the detector is built**.

---

## 04_Software

Application software.

Contains

- iDetector
- Launcher
- Configuration
- Calibration
- Firmware Upgrade
- Network
- Log
- License
- Workspace

Purpose

Defines **how users operate the detector software**.

---

## 05_Calibration

Detector calibration knowledge.

Contains

- Offset
- Gain
- Defect
- Dynamic Correction
- Hardware Calibration
- Calibration Workflow

Purpose

Defines **how detector calibration works**.

---

## 06_Workflow

Engineering workflows.

Contains

- Installation
- Communication
- Connection
- Calibration
- Firmware Upgrade
- Remote Support
- RMA

Purpose

Defines **how engineers perform operations**.

---

## 07_FailureKnowledge

Failure analysis.

Contains

- Communication Failure
- Image Failure
- Hardware Failure
- Firmware Failure
- Generator Failure
- Calibration Failure

Purpose

Defines **why failures occur**.

---

## 08_ImageDiagnosis

Image analysis.

Contains

- Image Artifacts
- Ghost
- Noise
- Uniformity
- Line Artifacts
- Defect Pixels

Purpose

Defines **how abnormal images are analyzed**.

---

## 09_DecisionTree

Engineering diagnosis.

Purpose

Guides engineers toward the correct troubleshooting path.

---

## 10_SOP

Standard Operating Procedures.

Purpose

Defines standardized engineering operations.

---

## 11_Case

Engineering case library.

Purpose

Stores field experience and actual customer cases.

---

## 12_ErrorCode

Error code library.

Purpose

Provides detailed explanations and handling procedures for SDK and detector error codes.

---

## 13_Template

Engineering templates.

Contains

- Customer Reply
- Remote Support
- RMA
- Log Collection

Purpose

Standardizes engineering communication.

---

## 14_Glossary

Engineering terminology.

Purpose

Provides unified terminology definitions.

---

## 15_Reference

Quick reference center.

Contains

- Command Reference
- SDK Quick Reference
- Image Index
- Calibration Index
- ErrorCode Index

Purpose

Supports rapid engineering lookup.

---

## 16_FAE

Engineering experience.

Purpose

Documents best practices, troubleshooting tips, and field recommendations.

---

## 17_Tools

Engineering utilities.

Contains

- DTDI Tool
- SDK Tool
- Firmware Tool
- License Tool

Purpose

Introduces engineering tools and their usage.

---

# 4. Knowledge Flow

Engineering knowledge flows through the following lifecycle.

```
Product

↓

Hardware

↓

Software

↓

SDK

↓

Workflow

↓

Calibration

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

---

# 5. Troubleshooting Navigation

Recommended navigation path for technical support.

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

Solution
```

---

# 6. Knowledge Dependency

The knowledge domains are not independent.

Example dependencies:

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
FailureKnowledge
        ↓
DecisionTree
        ↓
Case
        ↓
SOP
```

---

# 7. Knowledge Categories

| Category | Modules |
|----------|---------|
| Project Governance | 00 |
| Product Knowledge | 01 |
| Technical Documentation | 02–05 |
| Engineering Process | 06 |
| Troubleshooting | 07–12 |
| Engineering Resources | 13–17 |

---

# 8. Navigation Principles

When using DetectorAssistant:

If the objective is to understand **what something is**, begin with:

- Product
- Hardware
- Software
- SDK

If the objective is to perform **an operation**, begin with:

- Workflow
- SOP

If the objective is to solve **a problem**, begin with:

- FailureKnowledge
- DecisionTree
- ErrorCode
- Case

If the objective is to **look up information quickly**, begin with:

- Glossary
- Reference
- Tools

---

# 9. Related Documents

- KnowledgeRelationship.md
- ObjectModel.md
- Ontology.md
- EngineeringPrinciples.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial knowledge map |