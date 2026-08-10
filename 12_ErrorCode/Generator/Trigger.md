# Generator Error Code - Trigger

> Module: Generator
>
> Category: Trigger Control

---

# Overview

This document describes trigger-related abnormalities between the detector and the X-ray generator.

Trigger problems must be separated into configuration, physical signal, timing, and acquisition-window failures. A timeout alone does not identify which layer failed.

---

# Related Commands / Events

Commands:

- `Cmd_StartAcq`
- `Cmd_StopAcq`
- `Cmd_SetCaliSubset`

Events:

- `Evt_Exp_Enable`
- `Evt_Exp_Prohibit`
- `Evt_WaitImage_Timeout`
- `Evt_Image`
- `Evt_TaskResult_Failed`

---

# Diagnostic Entry

| Symptom / Error | Primary Path | Evidence |
|---|---|---|
| `Err_Cali_UnexpectImage_MistakeTrigger` | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Calibration mode, trigger mode, timing |
| `Evt_WaitImage_Timeout` | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) | Acquisition state, trigger, exposure |
| No exposure response | [NoExposure](../../09_DecisionTree/Connection/NoExposure.md) | Interlock, trigger signal, configuration |
| Exposure occurred but no image | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) | Trigger timing, image/RAW, network/log |

---

# Diagnostic Procedure

1. Confirm detector state is `Ready`.
2. Start acquisition and confirm the expected mode.
3. Record detector trigger mode and generator trigger configuration.
4. Verify physical trigger connection and pin/interface mapping.
5. Verify polarity and timing/pulse evidence where available.
6. Confirm whether exposure occurred inside the expected acquisition window.
7. Confirm `Evt_Image` or image data was received.
8. Route to the matching DecisionTree rather than changing multiple trigger parameters at once.
9. Perform one controlled retest after a documented configuration change.

---

# Trigger Mode Boundary

Possible modes may include Software Trigger, External Trigger, AED Trigger, and Dynamic Trigger depending on the product/configuration. This document does not define universal parameter values or timing thresholds; use the applicable product configuration source before changing values.

---

# Evidence Package

Collect:

- exact event/error and timestamp;
- detector and generator trigger mode;
- acquisition/application mode;
- trigger interface/pin configuration;
- polarity and waveform/timing where available;
- exposure evidence;
- image/RAW evidence when relevant;
- `Detector.log`;
- result after one controlled retest.

---

# Related DecisionTree / Workflow / Tool

- [NoExposure](../../09_DecisionTree/Connection/NoExposure.md)
- [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md)
- [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md)
- [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)
- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [ModeConfiguration](../../17_Tools/SDKTool/ModeConfiguration.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added trigger-layer routing, evidence boundary and controlled verification |
| v1.0 | 2026-08-07 | Initial release |