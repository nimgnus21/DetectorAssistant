# Generator Error Code - Communication

> Module: Generator
>
> Category: Generator Communication

---

# Overview

This document describes communication-related failures between the detector and the X-ray generator.

Although the SDK does not define dedicated generator error codes, communication failures between the detector and generator are common in field applications and can prevent normal exposure or image acquisition.

---

# Typical Symptoms

- Exposure cannot be triggered.
- Detector remains in waiting state.
- Generator exposure completed but no image received.
- Exposure signal not detected.
- Exposure delay is abnormal.
- Image acquisition timeout.

---

# Possible Causes

## Physical Connection

- Trigger cable disconnected.
- Trigger cable damaged.
- Incorrect interface wiring.
- Loose connector.

---

## Configuration

- Incorrect trigger mode.
- Generator output disabled.
- Detector trigger mode mismatch.
- Incorrect application mode.

---

## Timing

- Trigger pulse width too short.
- Exposure timing mismatch.
- Detector not ready before exposure.

---

## SDK Related

Associated SDK events:

- Evt_WaitImage_Timeout
- Evt_TaskResult_Failed
- Err_DetectorRespTimeout

---

# Diagnostic Procedure

1. Verify detector is Ready.
2. Verify generator is Ready.
3. Verify trigger cable.
4. Verify trigger voltage.
5. Verify trigger mode.
6. Verify exposure timing.
7. Check Detector.log.
8. Capture trigger waveform if necessary.

---

# Related DecisionTree

- 09_DecisionTree/Connection/NoExposure.md
- 09_DecisionTree/Image/ImageLoss.md

---

# Related Workflow

- 06_Workflow/ConfigurationWorkflow.md
- 06_Workflow/ImageGenerationWorkflow.md

---

# Related Case

- 11_Case/Communication