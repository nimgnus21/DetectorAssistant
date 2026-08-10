# Calibration Error Code - Offset

> Module: Calibration
>
> Category: Offset Calibration Error Codes

---

# Overview

This document describes error codes that may occur during Offset calibration.

Offset calibration is the foundation of detector image correction. It compensates for detector dark current and electronic offset before Gain and Defect calibration.

An abnormal Offset template may affect subsequent image quality and may contribute to Gain or Defect calibration failure. An Offset error code alone does not prove a template, hardware, communication, or ghosting root cause.

---

# Related Commands

- `Cmd_OffsetGeneration`
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
| `Err_Cali_GeneralError` | [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md) | Detector state, `Detector.log`, [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md) |
| `Err_Cali_DataNotReadyForGen` | [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md) | Required image set, acquisition result, log |
| `Err_Cali_NotEnoughIntervalTime_OffsetTmpl` | [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md) | Exposure history, recovery interval, Offset evidence |

---

# Error Codes

## Err_Cali_GeneralError

A general error occurred during Offset calibration.

### Diagnostic Procedure

1. Preserve the current log and calibration context before restart.
2. Verify detector state is `Ready`.
3. Verify the calibration acquisition completed without interruption.
4. Check whether a communication or detector-state error occurred at the same timestamp.
5. Follow [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md).
6. Execute the applicable [Calibration](../../10_SOP/Calibration.md) recovery step.
7. Use [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md) only after the input evidence is complete.

---

## Err_Cali_DataNotReadyForGen

The SDK has not received sufficient image data to generate the Offset template.

### Diagnostic Procedure

1. Verify the required Offset image count and acquisition completion.
2. Check for image loss, interruption, or task failure before generation.
3. Preserve the acquisition result and `Detector.log`.
4. Reacquire only the missing or invalid dataset according to the calibration procedure.
5. Regenerate after a complete dataset is confirmed.

---

## Err_Cali_NotEnoughIntervalTime_OffsetTmpl

Insufficient idle time elapsed before generating a valid Offset template. Residual signal may still be present.

### Diagnostic Procedure

1. Record the preceding exposure condition and timestamp.
2. Check whether the symptom followed high-dose exposure or repeated acquisition.
3. Allow the required recovery interval defined by the applicable product procedure; do not invent a fixed interval in this error-code reference.
4. Acquire new Offset evidence only after recovery.
5. If the problem persists, inspect the Offset pattern using [Offset Viewer](../../17_Tools/Offset%20Viewer/README.md) and continue through [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md).

---

# Verification Rule

Do not treat successful template generation as sufficient closure. Verify:

- template generation completed;
- selected/downloaded template is the intended one where hardware calibration is used;
- detector reconnect/reinitialization succeeded where required;
- controlled acquisition no longer shows the original symptom.

---

# Evidence Package

Collect before escalation or template replacement:

- exact error/event and timestamp;
- detector state;
- Offset acquisition completion status and image count where applicable;
- preceding exposure history;
- detector temperature/state if available;
- original Offset/template evidence;
- `Detector.log`;
- result after one controlled regeneration.

Use [LogExport](../../17_Tools/SDKTool/LogExport.md) for log preservation.

---

# Related DecisionTree / SOP / Tool

- [OffsetFailure](../../09_DecisionTree/Calibration/OffsetFailure.md)
- [Calibration](../../10_SOP/Calibration.md)
- [CalibrationTools](../../17_Tools/SDKTool/CalibrationTools.md)
- [DTDITool](../../17_Tools/SDKTool/DTDITool.md)
- [Offset Viewer](../../17_Tools/Offset%20Viewer/README.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

# Related Case / Knowledge

- [OffsetGenerationFailed](../../11_Case/Calibration/OffsetGenerationFailed.md)
- [OffsetFailure](../../07_FailureKnowledge/CalibrationFailure/OffsetFailure.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added direct diagnostic links, evidence package, and controlled verification rules |
| v1.0 | 2026-08-07 | Initial release |