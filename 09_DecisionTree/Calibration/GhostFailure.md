# Ghost Correction Decision Tree

> Module: Calibration
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

Ghost correction cannot be completed successfully or ghost artifacts remain after calibration.

Typical symptoms include:

- Ghost Correction Failed
- Ghost image remains after calibration
- Residual image is visible
- Ghost verification failed
- Image lag is still observed

---

# Diagnostic Flow

```
                 Ghost Correction Failed
                            │
                  Detector Connected?
                            │
               ┌────────────┴────────────┐
               │                         │
              NO                        YES
               │                         │
      Go to Connection Tree        Continue
                                        │
                                        ▼
                Offset Calibration Passed?
                                        │
                     ┌──────────────────┴──────────────────┐
                     │                                     │
                    NO                                    YES
                     │                                     │
              Complete Offset                     Continue
                                        │
                                        ▼
                 Gain Calibration Passed?
                                        │
                     ┌──────────────────┴──────────────────┐
                     │                                     │
                    NO                                    YES
                     │                                     │
               Complete Gain                      Continue
                                        │
                                        ▼
              Ghost Calibration Executed?
                                        │
                     ┌──────────────────┴──────────────────┐
                     │                                     │
                    NO                                    YES
                     │                                     │
              Start Calibration                  Continue
                                        │
                                        ▼
               Ghost Artifact Removed?
                                        │
                     ┌──────────────────┴──────────────────┐
                     │                                     │
                    YES                                   NO
                     │                                     │
              Problem Solved                     Continue Investigation
```

---

# Quick Checklist

Verify the following items:

- □ Detector is Online.
- □ Offset calibration completed successfully.
- □ Gain calibration completed successfully.
- □ Detector firmware is compatible.
- □ SDK version is compatible.
- □ Calibration environment is stable.
- □ Detector temperature is normal.
- □ Exposure conditions meet calibration requirements.

---

# Required Evidence

Collect before escalation:

- □ Detector Model
- □ Detector SN
- □ Firmware Version
- □ SDK Version
- □ Ghost Calibration Log
- □ Before / After Images
- □ Exposure Parameters
- □ Calibration Configuration
- □ Detector Status Screenshot

---

# Possible Root Causes

## Calibration

- Offset calibration abnormal
- Gain calibration abnormal
- Ghost correction parameters incorrect

---

## Exposure

- Incorrect exposure settings
- Unstable generator output
- Inconsistent calibration conditions

---

## Detector

- Detector image lag
- Internal detector status abnormal

---

## Software

- SDK incompatibility
- Calibration tool failure

---

# Recommended Actions

Priority 1

- Verify Offset calibration.
- Verify Gain calibration.

Priority 2

- Repeat Ghost correction under stable exposure conditions.

Priority 3

- Compare before/after calibration images.

Priority 4

- Collect logs and escalate if ghost artifacts persist.

---

# Escalation Criteria

Escalate when:

- Ghost artifacts remain after repeated calibration.
- Official calibration software produces the same result.
- Detector exhibits abnormal image lag.
- Firmware and SDK compatibility have been confirmed.
- Multiple calibration attempts under verified conditions fail.

---

# Related Documents

## Workflow

- 06_Workflow/CalibrationWorkflow.md

## Case

- 11_Case/Calibration/GhostCorrection.md

## Tools

- 17_Tools/CalibrationTools.md

## Reference

- 15_Reference/CalibrationReference.md

## Failure Knowledge

- 07_FailureKnowledge/Calibration/Ghost.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |