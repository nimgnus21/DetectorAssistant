# Generator Error Code

> Module: Generator
>
> Category: Generator-related Diagnostic Entry

---

# Overview

This module describes generator-related abnormalities that may affect detector operation.

The current SDK reference does not define a dedicated generator error-code family. Generator problems commonly appear through detector-side events, acquisition timeout, missing images, exposure prohibition, or synchronization abnormalities. Therefore, these files are diagnostic entry documents and must not invent vendor-specific generator fault codes.

---

# Diagnostic Chain

```text
Generator Symptom / SDK Event
        ↓
Generator State / Interlock / Exposure / Trigger / Communication / Configuration
        ↓
Primary DecisionTree
        ↓
SOP / Workflow
        ↓
Tool + Evidence
        ↓
Controlled Exposure / Acquisition Verification
```

---

# Directory Map

- `Communication.md` — interface and trigger communication failures
- `Exposure.md` — exposure execution and image reception
- `Trigger.md` — trigger mode, polarity, timing and synchronization
- `Interlock.md` — exposure permission/prohibition and safety conditions
- `GeneratorState.md` — Ready/Busy/Standby/Fault state interpretation
- `GeneratorFault.md` — generator fault evidence and escalation boundary
- `Configuration.md` — detector/generator configuration consistency

---

# Primary Routing

| Symptom / Event | Entry | Primary DecisionTree | Evidence |
|---|---|---|---|
| `Evt_Exp_Prohibit` / cannot expose | Interlock | [NoExposure](../../09_DecisionTree/Connection/NoExposure.md) | Generator state, interlock state, logs |
| `Evt_WaitImage_Timeout` | Exposure / Trigger | [AcquisitionTimeout](../../09_DecisionTree/Software/AcquisitionTimeout.md) | Acquisition state, trigger, exposure, log |
| Exposure completed, no image | Exposure | [ImageLoss](../../09_DecisionTree/Image/ImageLoss.md) | Exposure proof, trigger, image/RAW, network/log |
| Trigger mismatch | Trigger / Configuration | [NoExposure](../../09_DecisionTree/Connection/NoExposure.md) | Trigger mode, timing, waveform if available |
| Generator communication abnormal | Communication | [ConnectionTimeout](../../09_DecisionTree/Connection/ConnectionTimeout.md) | Physical interface, configuration, log |
| Calibration image trigger mismatch | Trigger | [DefectFailure](../../09_DecisionTree/Calibration/DefectFailure.md) | Calibration mode, trigger, image set |

---

# Evidence Package

Collect before changing configuration or replacing hardware:

- exact SDK event/error and timestamp;
- detector state;
- generator state/fault indication if available;
- trigger and synchronization configuration;
- exposure parameters;
- evidence that exposure actually occurred;
- trigger waveform/timing where available;
- original image/RAW when relevant;
- `Detector.log`;
- generator fault log where available;
- controlled retest result.

---

# Related Workflow / SOP / Tool

- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)
- [ImageGenerationWorkflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [Calibration](../../10_SOP/Calibration.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)
- [Log Viewer](../../17_Tools/Log%20Viewer/README.md)

---

# Engineering Boundary

Follow this order before declaring a generator hardware fault:

1. generator state;
2. detector state;
3. interlock/exposure permission;
4. trigger configuration and timing;
5. communication/interface;
6. controlled exposure evidence;
7. generator hardware fault evidence.

A detector timeout is not by itself proof of a generator hardware failure.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added generator diagnostic routing, evidence boundary and verification chain |
| v1.0 | 2026-08-07 | Initial release |