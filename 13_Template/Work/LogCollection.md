# Log Collection

> Module: Template
>
> Category: Information Collection

---

# Overview

This document defines the standard information collection requirements for detector troubleshooting.

Complete and accurate information significantly improves troubleshooting efficiency and reduces unnecessary communication.

Unless otherwise specified, Detector.log should always be collected before escalating an issue.

---

# Collection Principles

When collecting troubleshooting information:

- Collect only information related to the current issue.
- Preserve original files whenever possible.
- Do not modify Detector.log.
- Record software and firmware versions.
- Record detector identification information.
- Keep screenshots and images in their original resolution.

---

# Basic Information

Always collect the following information.

| Item | Required |
|------|----------|
| Detector Model | ✓ |
| Detector Serial Number (SN) | ✓ |
| SDK Version | ✓ |
| Firmware Version | ✓ |
| Detector.log | ✓ |
| Operating System | ✓ |
| Software Version | ✓ |

---

# Detector Information

Please record:

- Detector Model
- Detector SN
- Detector IP Address
- Detector Status
- Detector Interface Screenshot

---

# Software Information

Please record:

- SDK Version
- Application Version
- Operating System
- Driver Version (if applicable)

---

# Detector.log

## Location

Detector.log is generated automatically in the detector working directory.

Typical file name:

```text
Detector.log
```

---

## Requirements

Always provide:

- Original Detector.log
- Complete log file
- Do not edit the log

---

# Network Information

For communication-related issues, collect:

- Detector IP
- Computer IP
- Network Mask
- Gateway
- Switch Model
- Ping Result
- Network Topology (if available)

---

# Image Information

For image-related issues, collect:

- Original Image (Raw)
- Corrected Image
- Error Image
- Exposure Parameters
- Image Resolution
- Detector Interface Screenshot

---

# Exposure Information

Record:

- Generator Model
- Trigger Mode
- Exposure Mode
- kV
- mA
- Exposure Time
- Number of Exposures

---

# Calibration Information

For calibration issues, provide:

- Calibration Type
- Offset Template
- Gain Template
- Defect Template
- Calibration Images
- Calibration Result Screenshot

---

# Firmware Information

Record:

- Current Firmware Version
- Target Firmware Version (if upgrading)
- Upgrade Tool Version
- Upgrade Package Name

---

# Error Information

Please provide:

- Error Code
- Error Message
- Screenshot
- Time of Occurrence
- Reproduction Frequency

---

# Reproduction Information

Describe:

- Operating Procedure
- Expected Result
- Actual Result
- Whether the issue is reproducible
- Frequency of occurrence

---

# Required Information by Scenario

## Connection Failure

- Detector.log
- Detector IP
- Computer IP
- Ping Result
- Detector Interface Screenshot

---

## Image Abnormality

- Original Image
- Corrected Image
- Detector.log
- Exposure Parameters
- Calibration Templates

---

## Calibration Failure

- Detector.log
- Calibration Images
- Template Files
- SDK Version
- Firmware Version

---

## Firmware Upgrade Failure

- Detector.log
- Upgrade Package
- Firmware Version
- Upgrade Screenshot

---

## License Issue

- Detector SN
- Detector.log
- License File
- Error Screenshot

---

# File Naming Recommendation

Collected files should use a consistent naming format.

```text
SN_Date_Type

Example:

P1717A001_20260807_Detector.log
P1717A001_20260807_Raw.raw
P1717A001_20260807_Image.png
```

---

# Recommended Attachment Checklist

Before submitting a support request, verify the following:

□ Detector.log

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version

□ Original Image

□ Corrected Image

□ Detector Interface Screenshot

□ Software Screenshot

□ Error Screenshot

□ Exposure Parameters

□ Network Configuration

□ Reproduction Steps

---

# Related Modules

- CustomerReply.md
- InternalReply.md
- EmailTemplate.md
- ChatTemplate.md
- Checklist.md
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |