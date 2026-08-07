# Calibration

> Module: Template
>
> Category: Calibration Workflow Template

---

# Overview

This document provides standardized information collection, execution confirmation, and troubleshooting templates for detector calibration.

It is intended for Field Application Engineers (FAEs) during detector installation, factory calibration, maintenance, and after-sales support.

This document is **not** intended to replace the technical procedures in **05_Calibration**, but to standardize the execution and communication process during calibration.

---

# Applicable Scope

This template applies to:

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Hardware Calibration
- Calibration Verification
- Calibration Troubleshooting

---

# Calibration Preparation

Before starting calibration, verify the following items.

## Detector Status

□ Detector connected successfully

□ Detector status is **Ready**

□ Detector communication normal

□ Detector temperature within operating range

□ Detector humidity normal

---

## Software Environment

□ SDK version confirmed

□ Firmware version confirmed

□ Calibration software version confirmed

□ Detector.log enabled

---

## Hardware Environment

□ Detector powered normally

□ Stable power supply

□ Generator operating normally

□ Network communication stable

---

## Calibration Environment

□ X-ray generator warmed up

□ Exposure parameters confirmed

□ Calibration fixture prepared

□ Detector placement verified

---

# Offset Calibration

## Information Collection

Detector Model:

Detector SN:

SDK Version:

Firmware Version:

Offset Template Version:

---

## Required Files

□ Detector.log

□ Offset Images

□ Offset Template

□ Error Screenshot (if applicable)

---

## Verification Checklist

□ Offset generation completed

□ Offset template generated

□ Offset template downloaded

□ Offset template selected

□ Image quality verified

---

# Gain Calibration

## Information Collection

Detector Model:

Detector SN:

SDK Version:

Firmware Version:

Gain Template Version:

---

## Required Files

□ Detector.log

□ Gain Images

□ Gain Template

□ Exposure Parameters

---

## Verification Checklist

□ Gain initialization completed

□ All images acquired

□ Images selected correctly

□ Gain template generated

□ Gain template downloaded

□ Gain template selected

---

# Defect Calibration

## Information Collection

Detector Model:

Detector SN:

SDK Version:

Firmware Version:

Defect Template Version:

---

## Required Files

□ Detector.log

□ Defect Images

□ Defect Template

□ Error Screenshot

---

## Verification Checklist

□ Defect initialization completed

□ Required images acquired

□ Image selection completed

□ Defect template generated

□ Template downloaded

□ Template selected

---

# Hardware Calibration

Applicable when using:

- HW Gain
- HW Defect
- HW PreOffset

---

## Verification

□ Template downloaded to detector

□ Hardware template selected

□ Detector restarted if required

□ Hardware calibration loaded successfully

---

# Calibration Verification

After calibration, verify:

□ Detector reconnects normally

□ Image acquisition successful

□ Image quality normal

□ No abnormal artifacts

□ No unexpected noise

□ No obvious ghost

□ Calibration templates loaded correctly

---

# Common Calibration Failures

## Offset Generation Failed

Collect:

□ Detector.log

□ Offset Images

□ Detector Interface Screenshot

□ SDK Version

□ Firmware Version

---

## Gain Generation Failed

Collect:

□ Detector.log

□ Gain Images

□ Exposure Parameters

□ Generator Model

□ Detector Interface Screenshot

---

## Defect Generation Failed

Collect:

□ Detector.log

□ Defect Images

□ Current Template

□ Detector Screenshot

---

# Troubleshooting Checklist

## Communication

□ Detector online

□ Detector Ready

□ Network stable

---

## Exposure

□ Generator Ready

□ Exposure successful

□ Trigger mode correct

□ Exposure parameters correct

---

## Image

□ Images received correctly

□ Correct image count

□ No acquisition timeout

---

## Software

□ SDK Version correct

□ Firmware Version correct

□ Configuration file correct

---

# Information Required for Technical Support

Please provide:

□ Detector Model

□ Detector SN

□ SDK Version

□ Firmware Version

□ Detector.log

□ Calibration Type

□ Calibration Images

□ Exposure Parameters

□ Template Files

□ Detector Interface Screenshot

□ Error Screenshot

□ Reproduction Steps

---

# Related SDK Commands

Common calibration commands include:

- Cmd_OffsetGeneration
- Cmd_GainInit
- Cmd_GainSelectCurrent
- Cmd_GainSelectAll
- Cmd_GainGeneration
- Cmd_DefectInit
- Cmd_DefectSelectCurrent
- Cmd_DefectSelectAll
- Cmd_DefectGeneration
- Cmd_FinishGenerationProcess
- Cmd_DownloadCaliFile
- Cmd_SelectCaliFile
- Cmd_HwGeneratePreOffsetTemplate

---

# Related SDK Events

- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed
- Evt_Image
- Evt_GeneralError

---

# Related Error Codes

Common calibration-related error codes:

- Err_Cali_GeneralError
- Err_Cali_DataNotReadyForGen
- Err_Cali_UnexpectImage_DoseHighHigh
- Err_Cali_UnexpectImage_MistakeTrigger
- Err_Cali_NotEnoughIntervalTime_OffsetTmpl
- Err_FPD_HWCaliFileError
- Err_TaskTimeOut

---

# Related Modules

- 05_Calibration
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode
- LogCollection.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |