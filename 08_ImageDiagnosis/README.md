# Image Diagnosis

> DetectorAssistant image-symptom knowledge entry point
>
> Purpose: classify the observed image phenomenon, preserve the correct evidence, and route the engineer to the appropriate diagnostic and support knowledge.

---

# Overview

`08_ImageDiagnosis` is the phenomenon-oriented image knowledge layer of DetectorAssistant.

Use this module when the primary field input is an **observed image abnormality** and the first task is to answer:

- What image phenomenon is actually being observed?
- Is the pattern fixed, intermittent, or exposure / acquisition dependent?
- What evidence is required before assigning a likely cause?
- Which diagnosis, mechanism, solution, case, or downstream DecisionTree should be used next?

This module does not replace `09_DecisionTree`, `10_SOP`, `17_Tools`, or `11_Case`.

```text
Observed Image
      ↓
08_ImageDiagnosis
      ↓
Phenomenon Classification
      ↓
Symptoms / Definition / Diagnosis / Mechanism / Solution
      ↓
09_DecisionTree
      ↓
10_SOP + 17_Tools
      ↓
Evidence Verification
      ↓
11_Case / Knowledge Feedback
```

---

# Current Image Phenomenon Categories

The following entries reflect the current repository structure. No additional categories are implied by this README.

| Image Phenomenon | Entry | Typical Next Question |
|---|---|---|
| Bad Column | [BadColumn](BadColumn/) | Is the abnormality confined to a fixed column? |
| Bad Row | [BadRow](BadRow/) | Is the abnormality confined to a fixed row? |
| Banding | [Banding](Banding/) | Is the pattern a regular band / stripe phenomenon? |
| Dead Pixel | [DeadPixel](DeadPixel/) | Is the defect fixed at the same pixel coordinate? |
| Ghost | [Ghost](Ghost/) | Is residual image information related to a previous exposure? |
| Lag | [Lag](Lag/) | Does the previous frame persist across continuous acquisition? |
| Noise | [Noise](Noise/) | Is the abnormality random, fixed-pattern, or condition dependent? |
| Non-Uniformity | [NonUniformity](NonUniformity/) | Is the signal distribution spatially uneven across the image? |

---

# Standard Knowledge Structure

Each current image phenomenon directory follows the same six-document structure:

```text
<Image Phenomenon>/
├── Symptoms.md
├── Definition.md
├── Diagnosis.md
├── Mechanism.md
├── Solution.md
└── Case.md
```

Recommended reading sequence:

1. `Symptoms.md` — identify whether the observed pattern matches the phenomenon.
2. `Definition.md` — confirm terminology and classification boundaries.
3. `Diagnosis.md` — determine the next diagnostic branch.
4. `Mechanism.md` — understand the suspected failure mechanism.
5. `Solution.md` — perform the corresponding corrective action.
6. `Case.md` — check whether the phenomenon has a documented case-level conclusion.

Do not treat a phenomenon label alone as a confirmed root cause.

---

# Quick Field Entry

## Fixed Row / Column / Pixel Pattern

Start with:

- [Bad Row](BadRow/)
- [Bad Column](BadColumn/)
- [Dead Pixel](DeadPixel/)

Primary evidence to preserve:

- RAW image
- Processed image
- Repeated acquisition results
- Fixed coordinate or row / column position
- Offset / Gain / Defect template context

Then continue to the relevant Image or Calibration DecisionTree.

---

## Residual Image / Frame Persistence

Start with:

- [Ghost](Ghost/)
- [Lag](Lag/)

First distinguish whether the artifact is an exposure-related residual phenomenon or persistence across continuous acquisition. Preserve acquisition sequence and frame-order evidence before recalibration.

---

## Stripe / Band / Structured Pattern

Start with:

- [Banding](Banding/)
- [Bad Row](BadRow/)
- [Bad Column](BadColumn/)

Record orientation, periodicity, fixed position, and whether the same pattern exists in RAW output.

---

## Noise / Non-Uniform Signal

Start with:

- [Noise](Noise/)
- [Non-Uniformity](NonUniformity/)

Record exposure conditions, repeated acquisition behavior, dark / RAW comparison, and calibration context before assigning a root cause.

---

# Evidence-First Rules

Before modifying firmware, calibration files, or hardware configuration, preserve the evidence needed to reproduce the diagnosis.

Recommended minimum evidence:

- Detector model and SN
- Firmware version
- SDK version
- Exposure parameters
- RAW image where available
- Processed image
- Repeated image samples
- Detector status screenshot
- Relevant calibration status or files
- Log files when software or communication behavior is involved

For fixed-pattern defects, always record whether the abnormality remains at the same coordinate after repeated acquisition and recalibration.

---

# Relationship with Other Modules

## Diagnostic Routing

- [Image DecisionTree](../09_DecisionTree/Image/)
- [Calibration DecisionTree](../09_DecisionTree/Calibration/)

## Standard Procedures

- [Image Troubleshooting SOP](../10_SOP/ImageTroubleshooting.md)
- [Calibration SOP](../10_SOP/Calibration.md)

## Workflow

- [Image Generation Workflow](../06_Workflow/ImageGenerationWorkflow.md)
- [Calibration Workflow](../06_Workflow/CalibrationWorkflow.md)
- [Dynamic Correction Workflow](../06_Workflow/DynamicCorrectionWorkflow.md)

## Tools

- [ImageJ](../17_Tools/ImageJ/README.md)
- [Offset Viewer](../17_Tools/OffsetViewer/README.md)
- [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md)
- [Log Viewer](../17_Tools/Log/README.md)

## Cases

- [Image Case Directory](../11_Case/Image/)

---

# Boundary with FailureKnowledge

`08_ImageDiagnosis` answers primarily:

> **What is the observed image phenomenon, and what should be checked next?**

`07_FailureKnowledge` answers primarily:

> **What failure mechanism or root-cause class can explain the confirmed behavior?**

The two modules should not duplicate each other.

Use the image diagnosis layer for symptom classification and evidence routing. Move to FailureKnowledge when evidence supports a mechanism-level analysis.

---

# Case and Knowledge Feedback

When a real field issue is resolved:

```text
Observed Phenomenon
        ↓
ImageDiagnosis Classification
        ↓
DecisionTree + SOP + Tool
        ↓
Evidence Confirms Cause
        ↓
Existing Case?
   ├── Yes → Update only if new verified knowledge exists
   └── No  → Create / admit a new Case
        ↓
Feed verified knowledge back to
ImageDiagnosis / DecisionTree / SOP / FailureKnowledge
```

A Case must contain verified evidence and a traceable conclusion. Do not promote an unverified symptom hypothesis into a reusable root-cause rule.

---

# Maintenance Rules

1. Do not add a new image category unless the corresponding directory and knowledge files actually exist.
2. Keep the six-document structure consistent for current phenomenon directories.
3. Use concrete Markdown links to existing downstream modules.
4. Remove obsolete links rather than replacing them with guessed paths.
5. Keep phenomenon description separate from root-cause conclusion.
6. When a verified field case changes the diagnostic boundary, update the relevant phenomenon knowledge and its DecisionTree together.

---

# Related Modules

- [Project README](../README.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [SOP](../10_SOP/README.md)
- [Case](../11_Case/README.md)
- [Tools](../17_Tools/README.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.0 | 2026-08-10 | Rebuilt root entry from the current repository structure without adding new image categories or files |