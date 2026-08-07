# Remote Support

> Module: Template
>
> Category: Remote Technical Support

---

# Overview

This document provides standardized procedures, preparation requirements, information collection templates, and support records for remote technical support.

It is intended for Field Application Engineers (FAEs) performing remote troubleshooting, commissioning, firmware upgrades, calibration guidance, and customer technical support.

The objective is to improve remote support efficiency, reduce communication costs, and ensure complete troubleshooting records.

---

# Applicable Scope

This template applies to:

- Detector Installation
- Detector Configuration
- Detector Connection Failure
- Image Acquisition Failure
- Image Quality Issues
- Calibration Support
- Firmware Upgrade
- SDK Debugging
- Customer Training

---

# Remote Support Request

## Basic Information

Customer:

Project:

Country/Region:

Contact Person:

Phone / Email:

Support Engineer:

Date:

Time Zone:

Meeting Time:

Expected Duration:

---

# Remote Support Preparation

## Customer Side

Please confirm the following before the meeting.

### Hardware

□ Detector powered on

□ Detector connected

□ Generator available

□ Stable power supply

□ Network connection available

---

### Software

□ SDK installed

□ Application software installed

□ Detector.log enabled

□ Remote software installed (AnyDesk / TeamViewer)

□ Administrator privileges available

---

### Information

Prepare the following information before the meeting.

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version

□ Detector.log

□ Error Screenshot

□ Original Image

□ Corrected Image

□ Exposure Parameters

---

# FAE Preparation

Before starting remote support.

□ Customer information confirmed

□ Detector model confirmed

□ Firmware package prepared (if required)

□ SDK package prepared (if required)

□ Calibration files prepared (if required)

□ Latest documentation available

□ Knowledge Base reviewed

---

# Remote Support Workflow

## Step 1

Customer Information Verification

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version

---

## Step 2

Environment Verification

□ Detector Ready

□ Detector Connected

□ Network Normal

□ Detector Status Normal

---

## Step 3

Problem Reproduction

Record:

Issue Description:

Reproduction Steps:

Occurrence Frequency:

Expected Result:

Actual Result:

---

## Step 4

Information Collection

Collect:

□ Detector.log

□ Error Screenshot

□ Original Image

□ Corrected Image

□ Configuration Files

□ Network Configuration

---

## Step 5

Technical Verification

Verify:

□ Detector Communication

□ Exposure

□ Image Acquisition

□ Calibration

□ Firmware

□ SDK Configuration

---

## Step 6

Problem Resolution

Action Taken:

Temporary Solution:

Permanent Solution:

Need R&D Support:

□ Yes

□ No

---

# Firmware Upgrade Support

Verify before upgrade.

□ Correct firmware selected

□ Detector connected

□ Stable power

□ Detector.log enabled

After upgrade.

□ Firmware version verified

□ Detector reconnected

□ Image acquisition verified

□ Calibration verified

---

# Calibration Support

Verify:

□ Offset completed

□ Gain completed

□ Defect completed

□ Templates downloaded

□ Templates selected

□ Image quality verified

---

# Information Collection Checklist

Always collect the following before escalating.

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version

□ Detector.log

□ Original Image

□ Corrected Image

□ Detector Interface Screenshot

□ Application Screenshot

□ Error Screenshot

□ Exposure Parameters

□ Trigger Mode

□ Network Configuration

---

# Remote Support Record

Customer:

Support Engineer:

Date:

Support Duration:

Detector Model:

Detector SN:

SDK Version:

Firmware Version:

Issue Description:

Root Cause:

Solution:

Status:

□ Resolved

□ Temporary Solution

□ Escalated to R&D

---

# Follow-up Record

Follow-up Date:

Customer Feedback:

Issue Reproduced:

□ Yes

□ No

Current Status:

Further Action Required:

---

# Case Closure Checklist

Before closing the support case.

□ Issue reproduced

□ Root cause identified

□ Solution verified

□ Customer confirmed

□ Detector operating normally

□ Detector.log archived

□ Knowledge base updated (if applicable)

---

# Related SDK Commands

Frequently used during remote support.

- Cmd_Connect
- Cmd_Disconnect
- Cmd_Reset
- Cmd_StartAcq
- Cmd_StopAcq
- Cmd_ReadTemperature
- Cmd_ReadHumidity
- Cmd_UpdateFirmware
- Cmd_OffsetGeneration
- Cmd_GainGeneration
- Cmd_DefectGeneration
- Cmd_DownloadCaliFile
- Cmd_SelectCaliFile

---

# Related SDK Events

Monitor during troubleshooting.

- Evt_TaskResult_Succeed

- Evt_TaskResult_Failed

- Evt_GeneralError

- Evt_GeneralWarn

- Evt_Image

- Evt_ConnectProcess

- Evt_WaitImage_Timeout

- Evt_TemperatureHigh

---

# Related Error Codes

Frequently encountered during remote support.

- Err_DetectorNotFound

- Err_GeneralSocketErr

- Err_CommParamNotMatch

- Err_TaskTimeOut

- Err_DetectorRespTimeout

- Err_FPD_Busy

- Err_FPD_CmdExecuteTimeout

- Err_Cali_GeneralError

- Err_CallbackNotFinished

---

# Related Modules

- LogCollection.md
- Calibration.md
- FirmwareUpgrade.md
- CustomerReply.md
- InternalReply.md
- Checklist.md
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |