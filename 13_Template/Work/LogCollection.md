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

- Collect evidence from the affected detector and the affected software environment.
- Preserve original files whenever possible.
- Do not modify Detector.log, RAW images, templates, or original screenshots.
- Record software, SDK and firmware versions together with detector identification.
- Record the symptom and the acquisition conditions before performing corrective actions.

---

# Basic Information

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

# Image Abnormality Evidence

For image-related issues, collect:

- Original RAW image
- Corrected image
- Dark image when applicable
- Detector interface screenshot
- Software acquisition screenshot
- Exposure parameters
- Image resolution
- Current calibration/template status
- Reproduction frequency

For stripe, banding or line artifacts, additionally record:

- Whether the artifact appears in every image
- Whether the artifact appears in the dark image
- Whether the position is fixed or changes
- Whether moving the detector changes or removes the artifact
- Whether the image contains missing data segments
- Whether the pattern is equal-width and regularly alternating bright/dark

These observations support initial differentiation between fixed line artifacts, environmental interference, packet loss and calibration-related stripe patterns.

---

# Connection and Network Evidence

For communication-related issues, collect:

- Detector IP
- Computer IP
- Network Mask
- Gateway
- Connection mode
- Switch or network equipment model when used
- Ping result
- Network topology when available
- Detector interface screenshot

For wireless products, additionally record the configured AP/Client mode and the connection result after applying the configuration.

---

# Calibration Evidence

For calibration issues, provide:

- Calibration type
- Offset data/template
- Gain data/template
- Defect template
- Calibration images
- Calibration result screenshot
- Calibration log
- SDK version
- Firmware version

Do not replace or overwrite the original calibration files before the failure evidence is preserved.

---

# Firmware Upgrade Evidence

Record before and after the operation:

- Detector model
- Detector SN
- Current firmware version
- Target firmware version
- SDK version
- Upgrade tool version
- Upgrade package name
- Upgrade screenshot or status
- Detector.log
- Upgrade stage at which the failure occurred
- Whether the detector can reconnect after the operation

---

# Error Information

Provide:

- Error code
- Error message
- Screenshot
- Time of occurrence
- Operation stage
- Reproduction frequency
- Detector status at the time of failure

---

# Reproduction Information

Describe:

- Operating procedure
- Expected result
- Actual result
- Whether the issue is reproducible
- Frequency of occurrence
- Whether another detector or another software environment reproduces the same issue

---

# Scenario Checklists

## Connection Failure

- Detector.log
- Detector IP
- Computer IP
- Connection mode
- Ping result
- Detector interface screenshot

## Image Abnormality

- RAW image
- Corrected image
- Dark image when applicable
- Detector.log
- Exposure parameters
- Calibration/template information
- Detector interface screenshot
- Stripe/line characteristics when applicable

## Calibration Failure

- Detector.log
- Calibration images
- Template files
- SDK version
- Firmware version
- Calibration result screenshot

## Firmware Upgrade Failure

- Detector.log
- Upgrade package name
- Current and target firmware versions
- Upgrade tool/SDK version
- Upgrade screenshot
- Failure stage
- Post-upgrade reconnection result

---

# File Naming Recommendation

```text
SN_Date_Type

Example:
P1717A001_20260807_Detector.log
P1717A001_20260807_Raw.raw
P1717A001_20260807_Image.png
```

---

# Escalation Standard

Before escalation, verify that the scenario-specific checklist is complete. Missing original evidence should be marked explicitly rather than replaced with reconstructed files or descriptions.

---

# Related Modules

- 04_Software/Log
- 05_Calibration
- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added image stripe, wireless, calibration and firmware evidence requirements |
| v1.0 | 2026-08-07 | Initial release |