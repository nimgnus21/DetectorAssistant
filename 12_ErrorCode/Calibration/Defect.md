# Calibration Error Code - Defect

> Module: Calibration
>
> Category: Defect Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Defect calibration.

Defect calibration identifies defective pixels and generates a defect template for image correction. Calibration image quality, trigger correctness, exposure condition, and defect-map capacity must be evaluated separately.

---

# Related Commands

- `Cmd_DefectInit`
- `Cmd_LoadTemporaryDefectFile`
- `Cmd_DefectSelectCurrent`
- `Cmd_DefectSelectAll`
- `Cmd_DefectGeneration`
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
| `Err_Cali_GeneralError` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | State, image completeness, log |
| `Err_Cali_DataNotReadyForGen` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Image count and selection |
| `Err_Cali_UnexpectImage_DoseHighHigh` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Exposure/generator evidence |
| `Err_Cali_UnexpectImage_MistakeTrigger` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Trigger mode, waveform/timing where available |
| `Err_TooMuchDefectPoints` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Defect map/count and threshold evidence |
| `Err_FPD_HWCaliFileError` | [Calibration](../../10_SOP/Calibration.md) | Template identity, download/selection result |

---

# Error Codes

## Err_Cali_GeneralError

Preserve the current calibration context, detector state, input image set, and `Detector.log`, then enter [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md). Do not repeat generation until the failed stage is identified.

## Err_Cali_DataNotReadyForGen

Verify the required image set and selected images before generation. Check for image loss or interruption, then reacquire only the invalid or missing dataset according to [Calibration](../../10_SOP/Calibration.md).

## Err_Cali_UnexpectImage_DoseHighHigh

The image dose exceeded the expected Defect calibration condition.

1. Record the actual exposure settings.
2. Verify the applicable product calibration procedure.
3. Verify generator output rather than changing thresholds blindly.
4. Acquire a new dataset only after the exposure condition is corrected.

## Err_Cali_UnexpectImage_MistakeTrigger

The received image does not match the expected trigger/exposure mode.

1. Record detector trigger mode and acquisition mode.
2. Verify generator trigger configuration.
3. Check timing and signal evidence where available.
4. Continue through [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md); do not classify this as an image-quality problem alone.

## Err_TooMuchDefectPoints

The generated defect map exceeds supported hardware correction capacity.

1. Preserve the generated map and defect-count evidence.
2. Verify the defect threshold and false-defect contribution.
3. Regenerate only with a documented parameter change.
4. If the count remains beyond supported capacity, escalate as a detector/hardware limitation rather than forcing template selection.

## Err_FPD_HWCaliFileError

The detector cannot use the intended hardware calibration file.

1. Preserve the existing template and log evidence.
2. Verify template identity and integrity.
3. Download the intended template.
4. Select the intended template.
5. Verify hardware calibration state with controlled acquisition.

---

# Product-Specific Field Rule: Pluto0900X

For **Pluto0900X Defect calibration**, the SDK changes internal processing state when the **63rd image of the third image group** is received.

**Do not stop exposure at image 63. Acquisition must continue until image 64 has been received.**

This is a product-specific rule and must not be generalized to other models without verification.

---

# Verification Rule

A Defect calibration issue is closed only when:

- the intended image set completed;
- trigger/exposure conditions are verified where relevant;
- generation and `Cmd_FinishGenerationProcess` completed;
- the intended hardware template is downloaded/selected where applicable;
- controlled acquisition confirms the original symptom or error is resolved.

---

# Evidence Package

Collect:

- exact error/event and timestamp;
- detector state;
- image count and selection state;
- exposure parameters;
- trigger mode and timing evidence where applicable;
- defect map/count and threshold where applicable;
- template identity and hardware selection result;
- original image/RAW evidence when relevant;
- `Detector.log`;
- controlled verification result.

Use [LogExport](../../17_Tools/SDKTool/LogExport.md) for log preservation.

---

# Related DecisionTree / SOP / Tool

- [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md)
- [Calibration](../../10_SOP/Calibration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [DTDITool](../../17_Tools/SDKTool/DTDITool.md)
- [ModeConfiguration](../../17_Tools/SDKTool/ModeConfiguration.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

# Related Case / Knowledge

- [DefectGenerationFailed](../../11_Case/Calibration/DefectGenerationFailed.md)
- [DefectFailure](../../07_FailureKnowledge/CalibrationFailure/DefectFailure.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added per-error diagnostic mapping, evidence package, Pluto0900X boundary and closure verification |
| v1.0 | 2026-08-07 | Initial release |