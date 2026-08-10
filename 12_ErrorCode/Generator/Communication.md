# Generator Error Code - Communication

> Module: Generator
>
> Category: Generator Communication

---

# Overview

This document describes communication and interface failures between the detector system and the X-ray generator.

The current SDK reference does not define dedicated generator communication error codes. This document therefore routes observed symptoms and related SDK events into a reproducible diagnostic path without treating the detector-side timeout as proof of a generator fault.

---

# Diagnostic Entry

Typical entries:

- exposure cannot be triggered;
- detector waits for exposure;
- generator exposure completed but no image is received;
- exposure signal is not detected;
- abnormal exposure delay;
- `Evt_WaitImage_Timeout`;
- `Evt_TaskResult_Failed`;
- `Err_DetectorRespTimeout` where applicable.

---

# Diagnostic Procedure

1. Record detector state and generator state.
2. Verify the physical trigger/interface connection and connector seating.
3. Verify detector and generator trigger configuration match.
4. Confirm acquisition was started before the exposure sequence.
5. Confirm whether exposure actually occurred.
6. Capture trigger/timing evidence where available.
7. If the detector communication path is also suspected, run [NetworkConfiguration](../../10_SOP/NetworkConfiguration.md) and preserve relevant logs.
8. Enter [NoExposure](../../09_DecisionTree/Connection/NoExposure.md) for missing exposure, or [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) when exposure occurred but image delivery failed.
9. Perform one controlled retest and record the result.

---

# Evidence Package

- SDK event/error and timestamp;
- detector state;
- generator Ready/Fault indication if available;
- trigger mode and interface configuration;
- physical connection evidence;
- proof of exposure;
- trigger waveform/timing if available;
- `Detector.log`;
- generator log/fault indication if available;
- controlled retest result.

Use [LogExport](../../17_Tools/SDKTool/LogExport.md) for log preservation.

---

# Related DecisionTree / Workflow / Tool

- [NoExposure](../../09_DecisionTree/Connection/NoExposure.md)
- [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md)
- [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)
- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)
- [Log Viewer](../../17_Tools/Log%20Viewer/README.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added routing, evidence package and controlled verification |
| v1.0 | 2026-08-07 | Initial release |