# Remote Support

> Module: Standard Operating Procedure
>
> SOP ID: SOP-006
>
> Category: Remote Technical Support

---

# Scope

This SOP describes the standard procedure for providing remote technical support for Flat Panel Detectors (FPDs).

This procedure applies to:

- Communication failures
- Calibration failures
- Image abnormalities
- Firmware-related issues
- SDK-related issues
- Installation support
- Customer troubleshooting

---

# Objective

Provide efficient and standardized remote technical support while ensuring that sufficient diagnostic information is collected before analysis or escalation.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | First-line remote support |
| Technical Support Engineer | Remote diagnosis and solution |
| Customer | Provide required information and perform requested operations |
| R&D Engineer | Analyze unresolved issues |

---

# Preconditions

Before starting remote support, confirm:

- Customer contact information is available.
- Detector model and serial number are confirmed.
- Communication method has been established.
- Required software versions are known.
- Customer can perform basic operations.

---

# Required Tools

Hardware

- Customer Computer
- Detector
- Network Connection

Software

- SDK Tool
- DTDI Tool
- Remote Desktop Software
- Image Viewer
- Log Viewer

---

# Required Files

Collect the following files whenever possible:

- Detector.log
- Original Images
- Calibration Files
- Configuration Files
- Firmware Version Information
- SDK Version Information

---

# Safety Precautions

- Do not modify customer data without confirmation.
- Preserve original logs before troubleshooting.
- Record every configuration change.
- Confirm backup before firmware or calibration operations.

---

# Remote Support Workflow

```text
Receive Request

↓

Collect Basic Information

↓

Collect Logs

↓

Analyze Symptoms

↓

Identify Root Cause

↓

Guide Customer

↓

Verify Result

↓

Resolved?

↓

YES → Close Case

NO

↓

Escalate to R&D
```

---

# Procedure

## Step 1 – Receive Support Request

### Process

Collect:

- Customer Name
- Contact Information
- Product Model
- Detector SN
- Software Version
- Firmware Version

### Output

Support case created.

---

## Step 2 – Collect Problem Description

### Process

Request:

- Problem description
- Time of occurrence
- Frequency
- Recent changes
- Operating procedure

### Output

Problem identified.

---

## Step 3 – Collect Diagnostic Files

### Process

Request:

- Detector.log
- Error screenshots
- Test images
- Configuration files
- Firmware version
- SDK version

### Acceptance Criteria

Required diagnostic files received.

---

## Step 4 – Analyze Information

### Process

Review:

- Logs
- Error messages
- Image abnormalities
- Detector status
- Communication status

Determine probable cause.

---

## Step 5 – Guide Customer

### Process

Provide step-by-step instructions.

Possible actions include:

- Restart detector
- Verify network
- Repeat calibration
- Upgrade firmware
- Modify configuration

Verify each step before continuing.

---

## Step 6 – Verify Result

### Process

Request customer to:

- Reconnect detector
- Acquire test image
- Repeat failed operation

### Acceptance Criteria

Issue reproduced or resolved.

---

## Step 7 – Escalation

Escalate when:

- Root cause cannot be determined.
- Hardware failure is suspected.
- Firmware recovery fails.
- SDK abnormality cannot be reproduced.
- Multiple troubleshooting attempts fail.

Required attachments:

- Detector.log
- Images
- Configuration files
- Firmware version
- SDK version
- Customer operation record

---

# Acceptance Checklist

- Customer information collected.
- Detector information confirmed.
- Logs collected.
- Images collected.
- Root cause identified or narrowed.
- Solution verified.
- Support record completed.

---

# Records

Record:

- Customer Name
- Company
- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Problem Description
- Root Cause
- Corrective Action
- Detector.log
- Images
- Support Engineer
- Date

---

# Exception Matrix

| Situation | Action |
|-----------|--------|
| Missing Detector.log | Guide customer to collect logs |
| Missing images | Request original images before analysis |
| Unable to reproduce issue | Collect operation video and environment information |
| Communication interrupted | Verify network before continuing |
| Issue unresolved | Escalate with complete evidence package |

---

# Notes

- Always request **Detector.log** before performing troubleshooting.
- Prefer reproducing the problem before making configuration changes.
- Use the standard templates in **13_Template** when requesting customer information.
- Ensure all evidence is archived before escalation.

---

# Related Documents

- 06_Workflow/RemoteSupport
- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- 13_Template/CustomerReply
- 13_Template/LogCollection
- 13_Template/RemoteSupport
- SOP/ImageTroubleshooting

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |