# Calibration Defect Failure Decision Tree

> Module: Calibration
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

Calibration cannot be completed successfully, or calibration completes but image quality remains abnormal.

Typical symptoms include:

- Offset calibration repeatedly fails.
- Gain calibration repeatedly fails.
- Ghost correction is ineffective.
- The same image defect remains after successful calibration.
- Calibration results are inconsistent.
- Image quality does not improve after multiple calibration attempts.

---

# Diagnostic Flow

```
              Calibration Failure
                      │
          Calibration Completed?
                      │
             ┌────────┴────────┐
             │                 │
            NO                YES
             │                 │
   Go to Offset / Gain      Continue
                             │
                             ▼
         Calibration Repeated Successfully?
                             │
                 ┌───────────┴───────────┐
                 │                       │
                NO                      YES
                 │                       │
         Check Software          Continue
         Check Firmware                │
                                       ▼
        Same Image Defect Remains?
                                       │
                 ┌───────────┴───────────┐
                 │                       │
                NO                      YES
                 │                       │
          Calibration Solved      Continue
                                       │
                                       ▼
         Compare with Another Detector
                                       │
                 ┌───────────┴───────────┐
                 │                       │
          Problem Disappears      Problem Remains
                 │                       │
          Environment Issue      Suspect Detector
                                       │
                                       ▼
              Pixel / Line / TFT Defect?
                                       │
                 ┌───────────┴───────────┐
                 │                       │
                YES                     NO
                 │                       │
      Hardware Failure Suspected   Continue Investigation
```

---

# Quick Checklist

Verify:

- □ Offset calibration completed successfully.
- □ Gain calibration completed successfully.
- □ Ghost correction completed successfully.
- □ Firmware version is correct.
- □ SDK version is compatible.
- □ Exposure parameters are correct.
- □ Calibration files were regenerated.
- □ Detector restarted after calibration.
- □ Image defect remains unchanged.

---

# Required Evidence

Collect before escalation:

- □ Detector Model
- □ Detector SN
- □ Firmware Version
- □ SDK Version
- □ Offset File
- □ Gain File
- □ Ghost File
- □ Calibration Log
- □ Before Calibration Image
- □ After Calibration Image
- □ Detector Status Screenshot

---

# Possible Root Causes

## Detector Hardware

- Pixel defect
- Line defect
- TFT failure
- Readout circuit failure
- ADC abnormality

---

## Calibration

- Corrupted calibration files
- Incomplete calibration
- Incorrect calibration sequence

---

## Exposure System

- Generator instability
- Incorrect exposure parameters
- Trigger synchronization issue

---

## Software

- SDK compatibility issue
- Calibration tool abnormality

---

# Recommended Actions

Priority 1

- Regenerate all calibration files.
- Verify firmware and SDK compatibility.

Priority 2

- Compare with another detector under identical conditions.
- Compare with previous calibration results.

Priority 3

- Perform hardware verification.
- Analyze persistent defect characteristics.

Priority 4

- Escalate to hardware engineering if detector defect is suspected.

---

# Escalation Criteria

Escalate when:

- The same image defect persists after complete recalibration.
- Multiple calibration attempts produce identical results.
- Hardware-related defect patterns are observed.
- Comparison with another detector confirms the issue is detector-specific.
- Detector hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/CalibrationWorkflow.md

## Case

- 11_Case/Calibration/DefectFailure.md

## Tools

- 17_Tools/CalibrationTools.md

## Reference

- 15_Reference/CalibrationReference.md

## Failure Knowledge

- 07_FailureKnowledge/Calibration/
- 07_FailureKnowledge/TFT/
- 07_FailureKnowledge/Readout/

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |