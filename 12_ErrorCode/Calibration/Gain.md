# Calibration Error Code - Gain

> Module: Calibration
>
> Category: Gain Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Gain calibration.

Gain calibration compensates for pixel sensitivity differences and supports detector output uniformity. An abnormal Gain template may contribute to non-uniformity or banding, but the image symptom alone does not prove Gain as the root cause.

---

# Related Commands

- `Cmd_GainInit`
- `Cmd_GainSelectCurrent`
- `Cmd_GainSelectAll`
- `Cmd_GainGeneration`
- `Cmd_FinishGenerationProcess`
- `Cmd_DownloadCaliFile`
- `Cmd_SelectCaliFile`

# Related Events

- `Evt_TaskResult_Succeed`
- `Evt_TaskResult_Failed`
- `Evt_GeneralError`

---

# Error Code → Diagnostic Entry

| Error | Primary Path | Tool / Evidence |
|---|---|---|
| `Err_Cali_GeneralError` | [GainFailure](../../09_DecisionTree/Calibration/GainFailure.md) | Detector state, exposure parameters, `Detector.log` |
| `Err_Cali_DataNotReadyForGen` | [GainFailure](../../09_DecisionTree/Calibration/GainFailure.md) | Complete image set, selection state, acquisition evidence |

---

# Error Codes

## Err_Cali_GeneralError

A general error occurred during Gain calibration.

### Diagnostic Procedure

1. Preserve current Gain input evidence and `Detector.log`.
2. Verify detector state is `Ready`.
3. Verify exposure parameters and image acquisition completed as required.
4. Check communication or task errors at the same timestamp.
5. Enter [GainFailure](../../09_DecisionTree/Calibration/GainFailure.md).
6. Follow [Calibration](../../10_SOP/Calibration.md) rather than repeatedly restarting generation without evidence.

---

## Err_Cali_DataNotReadyForGen

The SDK has not received enough valid images to generate the Gain template.

### Diagnostic Procedure

1. Verify the required image count and sequence.
2. Verify `Cmd_GainSelectCurrent` or `Cmd_GainSelectAll` selected the intended images.
3. Check for image loss or acquisition interruption.
4. Preserve the selection state and log before reacquisition.
5. Reacquire missing or invalid images, then regenerate only after the full dataset is confirmed.

---

# Hardware Calibration Boundary

When hardware Gain is used:

1. Generate the intended template.
2. Download the template with `Cmd_DownloadCaliFile`.
3. Select it with `Cmd_SelectCaliFile`.
4. Verify the selected hardware template before controlled acquisition.

Do not treat software-template generation success as proof that the detector is using the intended hardware template.

---

# Verification Rule

Closure requires:

- successful generation;
- correct image selection;
- correct template download/selection where hardware Gain is used;
- controlled image acquisition;
- comparison against the original symptom or baseline.

If non-uniformity or banding remains after a verified Gain workflow, return to the image diagnostic path rather than declaring calibration failure resolved.

---

# Evidence Package

Collect:

- exact error/event and timestamp;
- detector state;
- exposure parameters;
- required/received image count;
- selected image state;
- hardware/software calibration mode;
- template identity where applicable;
- original image/RAW evidence when image quality is affected;
- `Detector.log`;
- controlled verification result.

---

# Related DecisionTree / SOP / Tool

- [GainFailure](../../09_DecisionTree/Calibration/GainFailure.md)
- [Calibration](../../10_SOP/Calibration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [DTDITool](../../17_Tools/SDKTool/DTDITool.md)
- [ImageJ](../../17_Tools/ImageJ/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

# Related Case / Knowledge

- [GainGenerationFailed](../../11_Case/Calibration/GainGenerationFailed.md)
- [GainFailure](../../07_FailureKnowledge/CalibrationFailure/GainFailure.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added diagnostic mapping, hardware template verification, evidence and closure rules |
| v1.0 | 2026-08-07 | Initial release |