# Naming Convention

> DetectorAssistant Naming Convention Specification

Project: DetectorAssistant

Version: v1.0.0

---

# 1. Purpose

This document defines the naming conventions used throughout DetectorAssistant.

The objectives are to:

- Ensure consistency across all documentation.
- Improve readability and maintainability.
- Simplify navigation and search.
- Support AI-based semantic retrieval.
- Prevent duplicate or ambiguous naming.

All project modules shall comply with this specification.

---

# 2. General Naming Principles

DetectorAssistant follows these principles:

- Use English for all filenames.
- Use descriptive names.
- One name represents one concept.
- Avoid abbreviations unless they are industry-standard.
- Use consistent terminology throughout the project.

Examples:

Correct

```
DetectorConnection
```

Incorrect

```
Connection1
Conn
DetectorConnect
```

---

# 3. File Naming Convention

Markdown filenames shall use:

- PascalCase
- No spaces
- No special characters
- No version numbers in filenames

Format

```
PascalCase.md
```

Examples

```
OffsetCalibration.md
FirmwareUpgrade.md
DetectorConnection.md
ImageUniformity.md
```

Incorrect

```
offset.md
offset_calibration.md
Firmware Upgrade.md
FirmwareUpgrade_v2.md
```

---

# 4. Directory Naming Convention

Top-level directories follow the format:

```
NN_ModuleName
```

Examples

```
00_Project
01_Product
02_SDK
03_Hardware
04_Software
05_Calibration
06_Workflow
07_FailureKnowledge
08_ImageDiagnosis
09_DecisionTree
10_SOP
11_Case
12_ErrorCode
13_Template
14_Glossary
15_Reference
16_FAE
17_Tools
```

Rules

- Two-digit numeric prefix.
- English module name.
- No spaces.
- Stable across versions.

---

# 5. Document Naming Rules

Each document shall describe a single engineering topic.

Preferred patterns:

```
<Device><Action>

DetectorConnection

FirmwareUpgrade

ImageAcquisition
```

or

```
<Concept><Type>

OffsetCalibration

CommunicationFailure

LicenseError
```

Avoid vague names such as:

```
General.md
Other.md
Notes.md
Document.md
```

---

# 6. Module Naming

Modules represent engineering domains.

Naming should use singular nouns whenever practical.

Examples

```
Hardware
Software
Workflow
Calibration
Reference
Glossary
```

Avoid plural forms unless they represent collections.

---

# 7. Workflow Naming

Workflow documents shall use:

```
<Action>Workflow
```

Examples

```
PowerOnWorkflow
ConnectionWorkflow
CalibrationWorkflow
FirmwareUpgradeWorkflow
RemoteSupportWorkflow
```

---

# 8. SOP Naming

SOP documents shall describe one standardized engineering procedure.

Examples

```
DetectorInstallation
Calibration
FirmwareUpgrade
RemoteSupport
PreventiveMaintenance
RMA
```

Do not include "SOP" in the filename.

---

# 9. Decision Tree Naming

DecisionTree documents describe one troubleshooting scenario.

Naming pattern:

```
<ProblemDescription>
```

Examples

```
DetectorNotFound
DetectorOffline
SDKInitializationFailed
AcquisitionTimeout
LicenseFailure
```

Avoid generic names.

---

# 10. Failure Knowledge Naming

Failure documents shall use:

```
<FailureType>
```

Examples

```
CommunicationFailure
CalibrationFailure
GeneratorFailure
ImageFailure
FirmwareFailure
```

---

# 11. Case Naming

Case documents shall describe one engineering case.

Recommended patterns:

```
<ProblemDescription>

VersionMismatch

OffsetGenerationFailed

DetectorConnectionFailed
```

or

```
<CustomerIssue>

GhostArtifact

ImageNoise

CommunicationTimeout
```

---

# 12. ErrorCode Naming

ErrorCode documents shall correspond to one logical category or one error.

Category examples:

```
Communication
Calibration
Generator
SDK
Firmware
Image
License
System
```

Individual error examples:

```
ERR001
GEN002
SDK015
```

Project-wide usage should remain consistent.

---

# 13. Template Naming

Template documents should describe their intended use.

Examples

```
CustomerReply
RemoteSupport
RMA
LogCollection
FirmwareUpgrade
```

---

# 14. Glossary Naming

Glossary documents shall use engineering concepts.

Examples

```
Detector
Offset
Gain
Defect
Exposure
Trigger
Firmware
SDK
```

Each glossary entry represents one concept.

---

# 15. Image Naming

Engineering images should follow:

```
<Category>_<Description>

Detector_Front

Detector_Back

Offset_Image

Gain_Result

Ghost_Example
```

Avoid:

```
Image1.png
Picture.png
NewImage.jpg
```

---

# 16. Diagram Naming

Engineering diagrams should describe their function.

Examples

```
DetectorArchitecture.drawio
SignalFlow.drawio
CalibrationFlow.drawio
Workflow.drawio
DecisionTree.drawio
```

---

# 17. Table Naming

Tables should have descriptive titles.

Examples

```
Firmware Compatibility Matrix

Detector State Table

ErrorCode Mapping Table

Calibration Parameter Table
```

---

# 18. Terminology Rules

Each engineering concept shall have one canonical name.

Preferred terms

```
Detector
Firmware
SDK
Offset
Gain
Defect
Exposure
Trigger
Callback
Generator
Calibration
```

Avoid using multiple names for the same concept.

---

# 19. Reserved Words

The following terms are reserved and should be used consistently.

```
Detector
SDK
Hardware
Software
Calibration
Workflow
Failure
DecisionTree
Case
Reference
Glossary
Template
Tool
ErrorCode
Firmware
License
```

---

# 20. Naming Validation Checklist

Before creating a new document, verify:

- [ ] English filename
- [ ] PascalCase
- [ ] One topic only
- [ ] No abbreviations (unless standard)
- [ ] No duplicate filename
- [ ] Consistent with existing terminology
- [ ] Appropriate module placement

---

# 21. Related Documents

- KnowledgeStandard.md
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
| v1.0 | 2026-08-07 | Initial naming convention specification |