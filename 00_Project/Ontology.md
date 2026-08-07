# Ontology

> DetectorAssistant Engineering Ontology

Project: DetectorAssistant

Version: v1.0.0

---

# 1. Purpose

This document defines the engineering ontology of DetectorAssistant.

The ontology establishes a common semantic model for all engineering knowledge within the project.

It provides standardized definitions for:

- Entities
- Attributes
- Relationships
- States
- Events
- Engineering concepts

The ontology ensures that every document describes the same concepts using consistent terminology and relationships.

---

# 2. Ontology Layers

DetectorAssistant organizes engineering knowledge into five semantic layers.

```
Concept Layer

↓

Entity Layer

↓

Relationship Layer

↓

Event Layer

↓

Document Layer
```

---

# 3. Entity Types

Entities represent real engineering objects.

---

## Product

Represents a detector product family.

Examples

- Pluto0001X
- Pluto0002X
- Pluto0900X
- Mercu

---

## Detector

Represents one physical detector.

Examples

- Detector SN
- Wireless Detector
- Wired Detector

---

## Hardware

Represents physical hardware components.

Examples

- TFT
- FPGA
- ADC
- Battery
- Ethernet
- Trigger
- Sensor
- WiFi

---

## Software

Represents application software.

Examples

- iDetector
- Launcher
- Configuration Tool
- DTDI Tool

---

## SDK

Represents software interfaces controlling the detector.

Examples

- Device API
- Acquisition API
- Callback API
- Firmware API
- License API

---

## Calibration

Represents detector calibration objects.

Examples

- Offset
- Gain
- Defect
- Dynamic Correction

---

## Image

Represents detector image data.

Examples

- Raw Image
- Corrected Image
- Preview Image

---

## Failure

Represents engineering failures.

Examples

- Communication Failure
- Calibration Failure
- Firmware Failure
- Hardware Failure
- SDK Failure
- Image Failure

---

## Workflow

Represents engineering processes.

Examples

- Installation
- Calibration
- Firmware Upgrade
- Remote Support

---

## SOP

Represents executable engineering procedures.

---

## Case

Represents engineering experience.

---

## ErrorCode

Represents standardized error identifiers.

---

## Tool

Represents engineering utilities.

---

# 4. Entity Attributes

Each entity is described by attributes.

Example

Detector

Attributes

- Serial Number
- Model
- Product Family
- Firmware Version
- Hardware Revision
- MAC Address
- IP Address
- Detector State

---

Image

Attributes

- Width
- Height
- Bit Depth
- Exposure Time
- Timestamp
- Calibration Status

---

Failure

Attributes

- Failure Type
- Root Cause
- Severity
- Symptoms
- Resolution

---

# 5. Relationship Types

DetectorAssistant uses standardized relationships.

| Relationship | Meaning |
|--------------|---------|
| contains | Parent contains child |
| belongsTo | Entity belongs to another entity |
| uses | Uses another object |
| communicatesWith | Exchanges data |
| controls | Controls another object |
| generates | Produces data |
| produces | Produces a physical or logical result |
| dependsOn | Requires another entity |
| affects | Influences another entity |
| diagnoses | Identifies a failure |
| resolves | Eliminates a failure |
| verifies | Confirms correctness |
| references | References another document |
| implements | Implements a workflow |
| records | Stores engineering evidence |

---

# 6. Detector Ontology

```
Product

contains

Detector

contains

Hardware

runs

Firmware

controlled by

SDK

used by

Software
```

---

# 7. Image Ontology

```
Detector

generates

Raw Image

↓

Calibration

↓

Corrected Image

↓

Image Diagnosis

↓

Failure

↓

DecisionTree
```

---

# 8. Calibration Ontology

```
Detector

↓

Offset

↓

Gain

↓

Defect

↓

Dynamic Correction

↓

Image Quality
```

Calibration improves image quality and directly affects image interpretation.

---

# 9. Failure Ontology

```
Failure

↓

Symptoms

↓

DecisionTree

↓

Workflow

↓

Case

↓

SOP

↓

Verification
```

Every failure should be diagnosable and traceable through this chain.

---

# 10. Event Types

Events represent actions occurring during detector operation.

Examples

Communication Events

- Connect
- Disconnect
- Timeout
- Reconnect

Calibration Events

- Offset Generation
- Gain Generation
- Defect Generation
- Calibration Loading

Acquisition Events

- Exposure Start
- Exposure End
- Image Receive
- Image Save

Firmware Events

- Upgrade
- Verification
- Recovery

Maintenance Events

- Installation
- Replacement
- Preventive Maintenance
- RMA

---

# 11. Detector States

Detector state describes the operational condition of the detector.

Typical states

```
Power Off

↓

Power On

↓

Initializing

↓

Ready

↓

Acquiring

↓

Busy

↓

Completed

↓

Idle
```

Abnormal states

- Disconnected
- Timeout
- Error
- Upgrade
- Recovery

---

# 12. Engineering Knowledge Model

Engineering knowledge follows this semantic model.

```
Entity

↓

Attribute

↓

State

↓

Event

↓

Failure

↓

Solution

↓

Verification

↓

Knowledge
```

---

# 13. Document Mapping

| Document Module | Primary Ontology |
|-----------------|------------------|
| Product | Product |
| Hardware | Hardware |
| Software | Software |
| SDK | SDK |
| Calibration | Calibration |
| Workflow | Workflow |
| FailureKnowledge | Failure |
| ImageDiagnosis | Image |
| DecisionTree | Failure + Workflow |
| SOP | Workflow |
| Case | Failure + Solution |
| ErrorCode | ErrorCode |
| Glossary | Concept |
| Tools | Tool |

---

# 14. Naming Principles

Each ontology entity shall:

- Have a unique name.
- Have one semantic meaning.
- Be reusable.
- Avoid synonyms where possible.
- Use English as the canonical identifier.

Preferred examples

- Detector
- Firmware
- Offset
- Gain
- Defect
- Exposure
- Callback
- Trigger

Avoid using multiple names for the same concept across different documents.

---

# 15. Future Extension

New ontology entities should:

- Extend existing entity types whenever possible.
- Reuse defined relationship types.
- Preserve semantic consistency.
- Maintain backward compatibility.

The ontology should evolve without changing existing core concepts.

---

# Related Documents

- KnowledgeMap.md
- KnowledgeRelationship.md
- ObjectModel.md
- KnowledgeStandard.md
- EngineeringPrinciples.md
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial engineering ontology |