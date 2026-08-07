# Internal Reply Template

> Module: Template
>
> Category: Internal Communication

---

# Overview

This document provides standardized internal communication templates for Field Application Engineers (FAEs), Technical Support Engineers, Quality Engineers, and R&D teams.

Unlike CustomerReply.md, these templates are intended for communication within the company or with distributors and partners. They focus on technical confirmation, issue escalation, OQC verification, firmware validation, and troubleshooting coordination.

---

# Usage Principles

Before sending an internal reply:

- Clearly describe the technical issue.
- Provide collected evidence.
- Avoid subjective conclusions.
- Include Detector.log whenever available.
- Specify the expected support from the recipient.

---

# Template 1 - Request R&D Analysis

**Applicable Scenarios**

- Unknown issue
- SDK exception
- Firmware abnormality
- Image anomaly requiring R&D analysis

---

Subject

Request R&D Analysis - Detector Issue

---

Please assist in analyzing the following issue.

Detector Information

- Detector Model:
- Detector SN:
- SDK Version:
- Firmware Version:

Issue Description

- Symptom:
- Frequency:
- Reproduction Procedure:

Attachments

- Detector.log
- Original Image
- Corrected Image
- Screenshots

Current Investigation

- Network verified
- Calibration verified
- Firmware verified
- Issue reproducible

Requested Support

- Root cause analysis
- Temporary workaround
- Firmware confirmation
- Development feedback

---

# Template 2 - OQC Verification

**Applicable Scenarios**

- Shipment inspection
- Factory verification
- RMA inspection

---

Please verify the following items before shipment.

Checklist

□ Detector Interface Screenshot

□ Acquisition Interface Screenshot

□ Detector Front Photo

□ Detector Rear Photo

□ Package Label Photo

□ Detector SN

□ Firmware Version

□ Image Test Completed

□ Detector Appearance Confirmed

Notes

If firmware versions are inconsistent, please contact R&D before shipment.

---

# Template 3 - Firmware Version Confirmation

**Applicable Scenarios**

- Firmware inconsistency
- Upgrade confirmation
- Production verification

---

Please confirm the following firmware information.

Detector Model:

Detector SN:

Current Firmware:

Target Firmware:

Upgrade Package:

SDK Version:

Please verify whether the firmware combination is approved for shipment.

---

# Template 4 - License Replacement

**Applicable Scenarios**

- Locked image
- License replacement
- Authorization update

---

Please verify the following information.

Detector SN:

Current License:

Issue Description:

Detector.log Attached:

If confirmed, please generate a replacement license.

---

# Template 5 - Calibration Review

**Applicable Scenarios**

- Offset
- Gain
- Defect calibration review

---

Please review the calibration results.

Calibration Type:

SDK Version:

Firmware Version:

Detector SN:

Template Version:

Attachments

- Calibration Images
- Detector.log
- Generated Templates

Please confirm whether the calibration results are acceptable.

---

# Template 6 - Customer Follow-up

**Applicable Scenarios**

- Customer issue tracking
- Pending verification
- Waiting for feedback

---

Current Status

The issue has been reproduced.

Completed Actions

- Detector verification completed
- Communication verified
- Firmware verified
- Calibration verified

Waiting For

□ Customer confirmation

□ Additional logs

□ Additional images

□ Remote support

Next Action

Continue troubleshooting after receiving the requested information.

---

# Template 7 - Remote Support Summary

**Applicable Scenarios**

- Remote debugging completed
- Meeting summary

---

Remote Support Summary

Date:

Participants:

Detector:

SDK:

Firmware:

Problem Description:

Operations Performed

- Communication verification
- Calibration verification
- Firmware verification
- Image acquisition test

Result

□ Issue resolved

□ Further analysis required

□ Escalated to R&D

Attachments

- Detector.log
- Screenshots
- Test Images

---

# Template 8 - Field Experience Record

**Applicable Scenarios**

- New issue discovered
- Valuable troubleshooting experience
- Knowledge base update

---

Issue Summary

Detector:

SDK:

Firmware:

Symptom:

Root Cause

(To be completed)

Solution

(To be completed)

Recommendation

(To be completed)

Need Knowledge Base Update

□ Yes

□ No

Related Documents

- DecisionTree
- ErrorCode
- Case
- FailureKnowledge

---

# Related Modules

- CustomerReply.md
- LogCollection.md
- 11_Case
- 12_ErrorCode
- 09_DecisionTree

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |