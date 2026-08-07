# Image Troubleshooting

> Module: Standard Operating Procedure
>
> SOP ID: SOP-005
>
> Category: Image Troubleshooting

---

# Scope

This SOP describes the standard troubleshooting procedure for detector image abnormalities.

This procedure applies to:

- Image artifacts
- Image quality degradation
- Calibration-related image issues
- Communication-related image abnormalities
- Hardware-related image abnormalities

---

# Objective

Quickly identify the root cause of image abnormalities using a standardized troubleshooting process while minimizing unnecessary detector replacement.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Perform on-site troubleshooting |
| Technical Support Engineer | Analyze logs and support remotely |
| R&D Engineer | Analyze unresolved image abnormalities |

---

# Preconditions

Before troubleshooting, confirm:

- Detector communication is normal.
- Detector status is Ready.
- SDK version is confirmed.
- Firmware version is confirmed.
- Generator operates normally.
- Detector has completed initialization.

---

# Required Tools

Hardware

- Detector
- Host Computer
- X-ray Generator
- Network Cable (if applicable)

Software

- SDK Tool
- DTDI Tool
- Image Viewer

---

# Required Files

- Detector.log
- Test Images
- Calibration Templates (if applicable)

---

# Safety Precautions

Before troubleshooting:

- Preserve the original image.
- Do not overwrite calibration templates.
- Save Detector.log before restarting the detector.
- Record detector firmware and SDK version.

---

# Troubleshooting Workflow

```text
Receive Image

↓

Identify Image Symptom

↓

Classify Image Abnormality

↓

Check Detector Status

↓

Check Communication

↓

Check Generator

↓

Check Calibration

↓

Acquire Verification Image

↓

Issue Resolved?

↓

YES → Record Result

NO

↓

DecisionTree

↓

Case Reference

↓

Escalate to R&D
```

---

# Procedure

## Step 1 – Collect Information

### Process

Record:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Customer Description
- Detector.log

Collect:

- Original Image
- Test Image
- Error Screenshot (if available)

### Acceptance Criteria

Required information collected.

---

## Step 2 – Identify Image Symptom

### Process

Determine the primary symptom.

Typical categories include:

- No Image
- Black Image
- White Image
- Noise
- Lines
- Banding
- Ghost
- Defect Pixels
- Image Shift
- Image Distortion
- Low Contrast
- Uniformity Issue

### Acceptance Criteria

Symptom classified.

---

## Step 3 – Verify Detector Status

### Process

Verify:

- Detector Ready
- Detector Temperature
- Detector Communication

### Acceptance Criteria

Detector operates normally.

### Exception Handling

Refer to:

- DecisionTree/Device

---

## Step 4 – Verify Communication

### Process

Check:

- Ethernet
- SDK Connection
- Packet Loss
- Detector Response

### Acceptance Criteria

Communication stable.

### Exception Handling

Refer to:

- DecisionTree/Connection
- ErrorCode/Communication

---

## Step 5 – Verify Generator

### Process

Check:

- Exposure
- Trigger
- Generator Ready
- Exposure Timing

### Acceptance Criteria

Generator operates normally.

### Exception Handling

Refer to:

- DecisionTree/Generator

---

## Step 6 – Verify Calibration

### Process

Check:

- Offset
- Gain
- Defect
- Selected SubSet
- Calibration Version

### Acceptance Criteria

Calibration valid.

### Exception Handling

Repeat calibration if required.

---

## Step 7 – Acquire Verification Image

### Process

Acquire a new test image using standard exposure conditions.

Compare:

- Original Image
- Verification Image

### Acceptance Criteria

Image quality verified.

---

## Step 8 – Determine Root Cause

### Process

Determine whether the issue is related to:

- Detector Hardware
- Calibration
- Communication
- Generator
- SDK
- Firmware
- Environment

### Acceptance Criteria

Root cause identified.

---

## Step 9 – Complete Troubleshooting

### Process

Record:

- Cause
- Solution
- Verification Result
- Attached Images
- Detector.log

---

# Image Classification Guide

| Symptom | Primary Inspection |
|----------|--------------------|
| No Image | Communication / Exposure |
| Black Image | Generator / Exposure |
| White Image | Calibration / Exposure |
| Horizontal Line | Gate Driver / Readout |
| Vertical Line | Readout Circuit |
| Banding | Calibration / Readout |
| Ghost | Offset / Ghost Correction |
| Dead Pixels | Defect Template |
| Noise | Offset / Exposure |
| Uniformity | Gain Template |
| Image Shift | Synchronization |
| Distortion | Communication / Firmware |

---

# Acceptance Checklist

- Root cause identified.
- Image verified.
- Detector.log archived.
- Verification image saved.
- Customer issue reproduced or resolved.
- Troubleshooting record completed.

---

# Records

Record:

- Customer
- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Detector.log
- Original Image
- Verification Image
- Root Cause
- Corrective Action
- Operator
- Date

---

# Notes

- Always preserve the original image before applying corrective actions.
- If recalibration is required, back up existing calibration templates.
- When troubleshooting communication-related image issues, verify the network before replacing hardware.
- Use the DecisionTree to avoid skipping standard diagnostic steps.
- Escalate to R&D only after completing the standard troubleshooting workflow and collecting all required evidence.

---

# Related Documents

- 05_Calibration
- 06_Workflow/ImageGenerationWorkflow
- 07_FailureKnowledge
- 08_ImageDiagnosis
- 09_DecisionTree/Image
- 11_Case/Image
- 12_ErrorCode/Image
- 14_Glossary/Image
- SOP/Calibration

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |