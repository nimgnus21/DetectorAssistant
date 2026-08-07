# Calibration

> Module: Glossary
>
> Category: Calibration Terminology

---

# Overview

This document defines the standard terminology related to detector calibration.

Calibration is the process of compensating for detector hardware characteristics to improve image quality and ensure consistent detector performance.

These terms are referenced throughout the DetectorAssistant knowledge base, including calibration procedures, troubleshooting workflows, SDK documentation, and error code references.

---

# Calibration

## Definition

The process of generating and applying correction templates to compensate for detector hardware characteristics and improve image quality.

## Objectives

- Reduce detector background noise
- Correct pixel response differences
- Eliminate defective pixels
- Improve image consistency

## Related Terms

- Offset
- Gain
- Defect
- Template

---

# Calibration Template

## Definition

A correction file generated during calibration and used by the detector or SDK to perform image correction.

## Common Types

- Offset Template
- Gain Template
- Defect Template
- PreOffset Template

---

# Offset Calibration

## Definition

Calibration used to compensate for the detector's dark signal when no X-ray exposure is present.

## Purpose

- Remove electronic offset
- Reduce background noise
- Establish the image baseline

## Related Terms

- Offset Template
- Dark Image

---

# Offset Template

## Definition

A calibration template generated during Offset Calibration and applied during image correction.

---

# Gain Calibration

## Definition

Calibration used to compensate for differences in pixel sensitivity under uniform X-ray exposure.

## Purpose

- Improve image uniformity
- Correct pixel response variation

## Related Terms

- Gain Template
- Uniform Exposure

---

# Gain Template

## Definition

A correction template generated during Gain Calibration.

---

# Defect Calibration

## Definition

Calibration used to identify abnormal pixels and generate a defect correction template.

## Purpose

Replace defective pixels using neighboring image information.

---

# Defect Template

## Definition

A correction template containing defective pixel information used during image correction.

---

# Bad Pixel

## Definition

A detector pixel that does not respond normally due to hardware characteristics or failure.

## Typical Types

- Dead Pixel
- Hot Pixel
- Unstable Pixel

---

# Dead Pixel

## Definition

A pixel that produces little or no usable signal.

---

# Hot Pixel

## Definition

A pixel that continuously outputs an abnormally high signal.

---

# PreOffset

## Definition

A hardware-based offset correction template stored inside the detector.

## Purpose

Reduce detector offset before software image correction.

## Related Terms

- HW Gain
- HW Defect

---

# HW Gain

## Definition

A gain correction template executed directly by detector hardware.

## Notes

The template must first be downloaded to the detector before use.

---

# HW Defect

## Definition

A defect correction template executed inside detector hardware.

---

# Hardware Calibration

## Definition

Calibration performed inside detector hardware instead of the host software.

## Advantages

- Faster correction
- Lower host CPU usage
- Real-time processing

---

# Software Calibration

## Definition

Calibration executed by the SDK or host application after image acquisition.

---

# Calibration File

## Definition

A file containing calibration data generated during detector calibration.

## Common Types

- Offset
- Gain
- Defect
- PreOffset

---

# Calibration Subset

## Definition

A named calibration configuration associated with a specific detector application mode.

## Purpose

Select the correct calibration templates for different operating modes.

## Related Terms

- Application Mode
- Cmd_SetCaliSubset

---

# Application Mode

## Definition

A predefined detector operating mode containing parameters such as FPS, PGA, and Binning.

Each Application Mode is associated with a unique calibration subset.

---

# Uniform Exposure

## Definition

An X-ray exposure producing an even radiation field across the detector.

## Purpose

Required for Gain Calibration.

---

# Dark Image

## Definition

An image acquired without X-ray exposure.

## Purpose

Used during Offset Calibration.

---

# Calibration Generation

## Definition

The process of collecting calibration images and generating correction templates.

---

# Calibration Verification

## Definition

The process of confirming that generated templates function correctly after calibration.

## Verification Items

- Template generation
- Template download
- Template selection
- Image quality
- Artifact inspection

---

# Ghost Correction

## Definition

A correction process used to reduce residual image artifacts caused by previous exposures.

## Related Terms

- Image Lag
- Dynamic Correction

---

# Dynamic Correction

## Definition

A correction method applied during dynamic detector operation to improve image consistency and reduce residual artifacts.

---

# Image Lag

## Definition

Residual signal remaining from previous exposures that appears in subsequent images.

---

# Calibration Download

## Definition

The process of transferring calibration templates from the host computer to the detector.

## Related SDK Command

Cmd_DownloadCaliFile

---

# Calibration Selection

## Definition

The process of selecting which calibration template the detector will use.

## Related SDK Command

Cmd_SelectCaliFile

---

# Calibration Initialization

## Definition

The preparation stage before template generation begins.

## Examples

- Cmd_GainInit
- Cmd_DefectInit

---

# Calibration Generation Process

## Definition

The complete workflow of collecting images, generating templates, and completing calibration.

## Typical Steps

1. Initialize
2. Acquire Images
3. Select Images
4. Generate Template
5. Download Template
6. Select Template
7. Verify Image Quality

---

# Related SDK Commands

- Cmd_SetCaliSubset
- Cmd_OffsetGeneration
- Cmd_GainInit
- Cmd_GainGeneration
- Cmd_DefectInit
- Cmd_DefectGeneration
- Cmd_DownloadCaliFile
- Cmd_SelectCaliFile
- Cmd_HwGeneratePreOffsetTemplate
- Cmd_FinishGenerationProcess

---

# Related SDK Events

- Evt_TaskResult_Succeed
- Evt_TaskResult_Failed
- Evt_Image
- Evt_TemplateOverDue

---

# Related Error Codes

- Err_Cali_GeneralError
- Err_Cali_DataNotReadyForGen
- Err_Cali_UnexpectImage_DoseHighHigh
- Err_Cali_UnexpectImage_MistakeTrigger
- Err_Cali_NotEnoughIntervalTime_OffsetTmpl
- Err_FPD_HWCaliFileError

---

# Related Modules

- 05_Calibration
- 06_Workflow
- 09_DecisionTree
- 11_Case
- 12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |