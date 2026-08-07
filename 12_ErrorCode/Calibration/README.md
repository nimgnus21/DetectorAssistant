# Calibration Error Code

> Module: Calibration
>
> Category: Error Code Reference

---

# Overview

This module summarizes all calibration-related error codes defined by the SDK and provides engineering-oriented troubleshooting guidance.

Calibration is the foundation of detector image quality. Offset, Gain, and Defect templates work together to compensate for detector offset, pixel response non-uniformity, and defective pixels.

Calibration failures may lead to:

- Image artifacts
- Residual (ghost) images
- Non-uniform brightness
- Excessive defective pixels
- Calibration interruption
- Hardware correction failure

This document serves as the entry point for all calibration-related error code analysis.

---

# Scope

This module applies to:

- Offset Calibration
- Gain Calibration
- Defect Calibration
- Hardware Calibration
- Template Generation
- Template Download
- Template Selection

---

# Document Structure

```text
Calibration
├── README.md
├── Offset.md
├── Gain.md
└── Defect.md
```

---

# Category Description

## Offset

Compensates detector electronic offset and dark current.

Typical issues include:

- Offset generation failure
- Residual signal
- Recovery interval
- Template generation

---

## Gain

Compensates pixel response differences.

Typical issues include:

- Gain image acquisition
- Image selection
- Gain template generation
- Hardware Gain configuration

---

## Defect

Generates the detector defect map.

Typical issues include:

- Defect image acquisition
- Trigger mismatch
- Excessive exposure
- Excessive defect pixels
- Hardware Defect correction

---

# Calibration Workflow

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Template Download

↓

Template Selection

↓

Image Verification
```

Each calibration stage depends on the successful completion of the previous stage.

---

# Common Error Codes

| Error Code | Description |
|------------|-------------|
| Err_Cali_GeneralError | General calibration error |
| Err_Cali_DataNotReadyForGen | Insufficient image data |
| Err_Cali_UnexpectImage_DoseHighHigh | Exposure dose too high |
| Err_Cali_UnexpectImage_MistakeTrigger | Trigger mode mismatch |
| Err_Cali_NotEnoughIntervalTime_OffsetTmpl | Recovery time insufficient |
| Err_TooMuchDefectPoints | Defect count exceeds FPGA capability |
| Err_FPD_HWCaliFileError | Hardware calibration template unavailable |

---

# Field Recommendations

## Offset

- Allow sufficient recovery time after exposure.
- Avoid generating Offset templates immediately after high-dose imaging.

## Gain

- Ensure all required images are acquired.
- Verify image selection before template generation.
- When using **HW_Gain**, the corresponding **PreOffset** must also use hardware calibration.

## Defect

- Verify trigger mode and exposure parameters.
- Ensure the complete calibration image set is acquired.
- For **Pluto0900X**, continue acquisition until **image 64** of the third image group. Do **not** stop at image 63.

---

# Hardware Calibration

Hardware correction requires the following sequence:

```text
Generate Template

↓

Cmd_DownloadCaliFile

↓

Cmd_SelectCaliFile

↓

Hardware Correction Enabled
```

A generated template will not take effect until it has been downloaded to the detector and selected.

---

# Recommended Troubleshooting Procedure

When calibration-related errors occur:

1. Verify detector status is **Ready**.
2. Check exposure parameters.
3. Verify trigger mode.
4. Ensure the complete image set has been acquired.
5. Generate the template.
6. Execute `Cmd_FinishGenerationProcess`.
7. Download and select the template if hardware correction is used.
8. Review `Detector.log`.
9. Follow the related DecisionTree.

---

# Related Modules

## DecisionTree

```text
09_DecisionTree/Calibration
```

---

## Workflow

```text
05_Calibration
06_Workflow/CalibrationWorkflow.md
```

---

## FailureKnowledge

```text
07_FailureKnowledge/CalibrationFailure
```

---

## Case

```text
11_Case/Calibration
```

---

# Related Log

```
Detector.log
```

When escalating calibration issues, collect:

- Detector.log
- Detector Model
- Detector Serial Number
- Firmware Version
- SDK Version
- Calibration Type (Offset / Gain / Defect)
- Exposure Parameters
- Trigger Mode
- Calibration Images
- Reproduction Procedure

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |