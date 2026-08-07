# Boot Failure Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

The detector fails to complete the startup process after power-on.

Typical symptoms include:

- Detector cannot complete initialization.
- Detector remains Offline after power-on.
- SDK cannot establish communication.
- Detector repeatedly disconnects.
- Status indicator remains abnormal.

---

# Diagnostic Flow

```
                    Boot Failure
                          │
                  Power Supply Normal?
                          │
              ┌───────────┴───────────┐
              │                       │
             NO                      YES
              │                       │
      Check Power Adapter       Continue
      Check Power Cable              │
                                     ▼
                     Detector Detected by SDK?
                                     │
                     ┌───────────────┴───────────────┐
                     │                               │
                    NO                              YES
                     │                               │
         Go to Detector Offline              Continue
                                             │
                                             ▼
                          Firmware Version Readable?
                                             │
                     ┌───────────────┴───────────────┐
                     │                               │
                    NO                              YES
                     │                               │
              Firmware Corrupted?            Continue
                     │                               │
             Parameter Recovery              ▼
                                     Detector Status Normal?
                                             │
                     ┌───────────────┴───────────────┐
                     │                               │
                    NO                              YES
                     │                               │
              Check Configuration          Continue
                                             │
                                             ▼
                           Image Acquisition Successful?
                                             │
                     ┌───────────────┴───────────────┐
                     │                               │
                    NO                              YES
                     │                               │
               Go to Image Tree           Problem Solved
```

---

# Quick Checklist

Before escalation, verify:

- □ Power supply is stable.
- □ Detector starts normally.
- □ SDK can detect the detector.
- □ Firmware version can be read.
- □ Firmware matches SDK version.
- □ Detector parameters are valid.
- □ Boot process completes successfully.
- □ Image acquisition can be started.

---

# Possible Root Causes

## Firmware

- Firmware corruption
- Incomplete firmware upgrade
- Version incompatibility

---

## Configuration

- Invalid detector parameters
- Startup configuration error

---

## Hardware

- Flash storage failure
- FPGA startup abnormal
- Power initialization failure

---

## Software

- SDK version mismatch
- Driver incompatibility

---

# Recommended Actions

Priority 1

- Verify detector power-on sequence.
- Read firmware version.

Priority 2

- Compare firmware with supported SDK version.
- Verify detector parameters.

Priority 3

- Perform Parameter Recovery.
- Reboot detector.

Priority 4

- Re-upgrade firmware if corruption is confirmed.

---

# Escalation Criteria

Escalate when:

- Firmware version cannot be read.
- Detector repeatedly fails to boot.
- Parameter recovery is unsuccessful.
- Firmware reinstallation does not resolve the issue.
- Hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/FirmwareUpgradeWorkflow.md

## Case

- 11_Case/Firmware/BootFailed.md
- 11_Case/Firmware/VersionMismatch.md
- 11_Case/Firmware/ParameterRecovery.md

## Tools

- 17_Tools/SDKTool/FirmwareUpgrade.md

## Reference

- 15_Reference/SDKReference.md

## Failure Knowledge

- 07_FailureKnowledge/Firmware/

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |