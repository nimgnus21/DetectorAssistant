# Generator Error Code - Exposure

> Module: Generator
>
> Category: Exposure Control

---

# Overview

This document describes exposure-related abnormalities between the detector and the X-ray generator.

Generator exposure failures are often reflected through SDK events rather than a dedicated generator error code. The diagnostic objective is to determine which stage failed: permission, acquisition readiness, trigger, actual exposure, or image delivery.

---

# Related Commands / Events

Commands:

- `Cmd_StartAcq`
- `Cmd_StopAcq`
- `Cmd_ClearAcq`

Events:

- `Evt_Exp_Enable`
- `Evt_Exp_Prohibit`
- `Evt_WaitImage_Timeout`
- `Evt_TaskResult_Failed`
- `Evt_Image`

---

# Error / Event → Diagnostic Entry

| Event / Symptom | Primary Path | Evidence |
|---|---|---|
| `Evt_Exp_Prohibit` / cannot expose | [NoExposure](../../09_DecisionTree/Connection/NoExposure.md) | Interlock, generator state, detector state |
| `Evt_WaitImage_Timeout` | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) | Acquisition, trigger, exposure, log |
| Exposure completed but no `Evt_Image` | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) | Exposure proof, image/RAW, network/log |
| `Err_DetectorRespTimeout` | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | Device/network state, log |

---

# Diagnostic Procedure

1. Confirm detector is `Ready`.
2. Start acquisition and record the command/result.
3. Confirm exposure permission (`Evt_Exp_Enable`) or identify prohibition (`Evt_Exp_Prohibit`).
4. Verify generator state.
5. Verify trigger mode and synchronization.
6. Confirm whether physical exposure actually occurred.
7. If exposure occurred, confirm whether `Evt_Image` or image data was received.
8. Route missing exposure to [NoExposure](../../09_DecisionTree/Connection/NoExposure.md); route missing image after confirmed exposure to [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md).
9. Export `Detector.log` and correlate timestamps.
10. Perform one controlled retest after the identified condition is corrected.

---

# Evidence Package

- exact event/error and timestamp;
- detector state;
- acquisition mode and key parameters;
- exposure permission/prohibition state;
- generator state/fault indication;
- trigger mode and timing evidence;
- proof of actual exposure;
- image/RAW evidence when an image was delivered;
- `Detector.log`;
- controlled retest result.

---

# Related DecisionTree / Workflow / Tool

- [NoExposure](../../09_DecisionTree/Connection/NoExposure.md)
- [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md)
- [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md)
- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)
- [Log Viewer](../../17_Tools/Log%20Viewer/README.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added stage-based exposure routing, evidence package and verification rules |
| v1.0 | 2026-08-07 | Initial release |