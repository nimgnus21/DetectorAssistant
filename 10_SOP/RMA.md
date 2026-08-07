# Return Material Authorization (RMA)

> Module: Standard Operating Procedure
>
> SOP ID: SOP-009
>
> Category: Return Material Authorization (RMA)

---

# Scope

This SOP defines the standard procedure for evaluating, approving, processing, and tracking detector Return Material Authorization (RMA).

This procedure applies to:

- Hardware failure
- Detector replacement
- Factory repair
- Customer return
- Warranty evaluation
- Engineering analysis

---

# Objective

Ensure every returned detector contains sufficient technical evidence and complete records to support failure analysis, repair, quality improvement, and traceability.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Initial diagnosis, evidence collection, RMA application |
| Technical Support Engineer | Remote diagnosis and technical review |
| Quality Engineer | Failure confirmation and quality evaluation |
| Repair Engineer | Detector inspection and repair |
| R&D Engineer | Root cause analysis for complex failures |

---

# Preconditions

Before initiating an RMA:

- Standard troubleshooting has been completed.
- DecisionTree has been followed.
- Remote support has been completed (if applicable).
- Detector replacement is required or repair has been approved.
- Customer agrees to return the detector.

---

# Required Tools

## Hardware

- Detector
- Host Computer
- Network Cable
- Packaging Materials

## Software

- SDK Tool
- DTDI Tool
- Image Viewer

---

# Required Files

The following files should be collected before shipment:

- Detector.log
- Original Images
- Test Images
- Firmware Version Information
- SDK Version Information
- Configuration Files
- Calibration Information (if applicable)
- Error Screenshots
- Customer Description

---

# Safety Precautions

- Preserve detector status before powering off.
- Do not overwrite logs before collection.
- Back up configuration files if available.
- Use anti-static packaging.
- Protect detector from vibration and impact during transportation.

---

# RMA Workflow

```text
Problem Report

↓

Standard Troubleshooting

↓

Remote Support

↓

Issue Resolved?

↓

YES

Close Case

↓

NO

↓

Collect Evidence

↓

Technical Review

↓

Approve RMA

↓

Backup Configuration

↓

Package Detector

↓

Ship Detector

↓

Factory Inspection

↓

Failure Analysis

↓

Repair / Replacement

↓

Return Detector

↓

Customer Verification

↓

Close RMA
```

---

# Procedure

## Step 1 – Confirm RMA Requirement

### Process

Verify that:

- Standard troubleshooting has been completed.
- Image verification has been performed.
- Calibration verification has been completed.
- Firmware verification has been completed.

### Acceptance Criteria

RMA is technically justified.

---

## Step 2 – Collect Technical Evidence

### Process

Collect:

- Detector.log
- Detector SN
- Firmware Version
- SDK Version
- Test Images
- Error Screenshots
- Customer Description

### Acceptance Criteria

Complete evidence package prepared.

---

## Step 3 – Technical Review

### Process

Review:

- Failure history
- DecisionTree results
- ErrorCode
- Previous repair records
- Case history

Determine whether repair is required.

### Acceptance Criteria

Technical review completed.

---

## Step 4 – Backup Information

### Process

Archive:

- Detector configuration
- Calibration information
- Firmware information
- Detector.log

### Acceptance Criteria

Required information preserved.

---

## Step 5 – Prepare Detector

### Process

- Power off detector.
- Disconnect cables.
- Remove accessories if required.
- Clean detector surface.

### Acceptance Criteria

Detector ready for shipment.

---

## Step 6 – Package Detector

### Process

Use:

- Anti-static bag
- Shock-absorbing foam
- Original packaging (preferred)

Attach:

- RMA Form
- Failure Description
- Shipping Label

### Acceptance Criteria

Detector packaged securely.

---

## Step 7 – Factory Inspection

### Process

Factory performs:

- Appearance inspection
- Communication verification
- Firmware verification
- Calibration verification
- Image quality verification
- Failure reproduction

### Acceptance Criteria

Inspection completed.

---

## Step 8 – Failure Analysis

### Process

Determine root cause.

Possible categories:

- Hardware
- Firmware
- SDK
- Calibration
- Communication
- User operation
- Environment

### Acceptance Criteria

Failure classified.

---

## Step 9 – Repair or Replacement

### Process

Perform:

- Hardware repair
- Firmware update
- Detector replacement
- Calibration
- Functional verification

### Acceptance Criteria

Detector passes verification.

---

## Step 10 – Return Verification

### Process

Customer verifies:

- Communication
- Image acquisition
- Image quality
- Clinical workflow

### Acceptance Criteria

Customer accepts detector.

---

## Step 11 – Close RMA

### Process

Archive:

- RMA Report
- Repair Report
- Detector.log
- Test Images
- Root Cause Analysis

Update maintenance history.

### Output

RMA completed.

---

# Acceptance Checklist

- Standard troubleshooting completed.
- Technical review completed.
- Detector.log archived.
- Images archived.
- Configuration archived.
- Detector packaged correctly.
- Factory inspection completed.
- Root cause identified.
- Repair verified.
- Customer acceptance completed.
- RMA closed.

---

# Exception Matrix

| Situation | Action |
|-----------|--------|
| Missing Detector.log | Request customer to recollect before shipment |
| Detector cannot power on | Record condition and continue RMA |
| Packaging damaged | Repackage before shipment |
| Failure cannot be reproduced | Continue engineering analysis |
| Multiple previous RMAs | Escalate to Quality and R&D |

---

# Records

Record:

- RMA Number
- Customer Name
- Company
- Detector Model
- Detector Serial Number
- Firmware Version
- SDK Version
- Failure Description
- Root Cause
- Repair Action
- Repair Engineer
- Verification Result
- Return Date
- Customer Acceptance
- Detector.log
- Test Images

---

# Notes

- Every RMA shall have a unique RMA number.
- Detector.log should always be collected before shipment whenever possible.
- Calibration templates should be backed up before repair if data preservation is required.
- Attach representative images demonstrating the reported issue.
- If multiple detectors exhibit the same failure, notify the Quality and R&D teams for trend analysis.

---

# Related Documents

- SOP/RemoteSupport
- SOP/DetectorReplacement
- SOP/ImageTroubleshooting
- SOP/Calibration
- 06_Workflow/RMA
- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- 13_Template/RMA
- 14_Glossary

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |