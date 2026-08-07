# Version Mismatch Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

The detector firmware version is incompatible with the software or SDK version.

Typical symptoms include:

- Detector cannot connect after upgrade.
- Unsupported firmware version.
- SDK reports version mismatch.
- Some detector functions are unavailable.
- Calibration cannot be performed.
- Image acquisition fails after software update.

---

# Diagnostic Flow

```
                  Version Mismatch
                         │
              Firmware Version Readable?
                         │
               ┌─────────┴─────────┐
               │                   │
              NO                  YES
               │                   │
       Go to Boot Failure     Compare Version Matrix
                                   │
                                   ▼
                    Firmware Supported by SDK?
                                   │
                      ┌────────────┴────────────┐
                      │                         │
                     NO                        YES
                      │                         │
            Install Compatible SDK      Continue
                                   │
                                   ▼
                    Detector Model Correct?
                                   │
                      ┌────────────┴────────────┐
                      │                         │
                     NO                        YES
                      │                         │
              Verify Detector Model      Continue
                                   │
                                   ▼
                    Configuration Compatible?
                                   │
                      ┌────────────┴────────────┐
                      │                         │
                     NO                        YES
                      │                         │
               Reload Parameters        Continue
                                   │
                                   ▼
                  Calibration Successful?
                                   │
                      ┌────────────┴────────────┐
                      │                         │
                     NO                        YES
                      │                         │
           Go to Calibration Tree      Continue
                                   │
                                   ▼
                 Image Acquisition Successful?
                                   │
                      ┌────────────┴────────────┐
                      │                         │
                     NO                        YES
                      │                         │
              Go to Image Tree         Problem Solved
```

---

# Quick Checklist

Verify the following items:

- □ Firmware version
- □ SDK version
- □ Detector model
- □ Supported version matrix
- □ Configuration file
- □ Detector parameters
- □ Calibration status
- □ Image acquisition

---

# Required Evidence

Collect the following information before escalation:

- □ Detector Serial Number (SN)
- □ Detector Model
- □ Current Firmware Version
- □ SDK Version
- □ Software Version
- □ Upgrade History
- □ Error Screenshot
- □ SDK Log
- □ Detector Status Screenshot

---

# Possible Root Causes

## Firmware

- Unsupported firmware version
- Incorrect firmware package
- Firmware downgrade

---

## SDK

- SDK too old
- SDK too new
- Incorrect runtime library

---

## Configuration

- Old parameter file
- Configuration not updated
- Mode configuration mismatch

---

## Product

- Incorrect detector model
- Wrong firmware branch

---

# Recommended Actions

Priority 1

- Verify detector model.
- Verify firmware version.
- Verify SDK version.

Priority 2

- Compare with the official compatibility matrix.
- Install the supported SDK version.

Priority 3

- Reload detector parameters.
- Verify detector configuration.

Priority 4

- Reinstall compatible firmware if required.

---

# Escalation Criteria

Escalate when:

- No compatible firmware can be identified.
- Official compatibility matrix cannot resolve the issue.
- Detector remains incompatible after firmware replacement.
- Multiple detector models exhibit the same behavior.

---

# Related Documents

## Workflow

- 06_Workflow/FirmwareUpgradeWorkflow.md
- 06_Workflow/ConfigurationWorkflow.md

## Case

- 11_Case/Firmware/VersionMismatch.md
- 11_Case/Firmware/FirmwareUpgradeFailed.md
- 11_Case/Firmware/ParameterRecovery.md

## Tools

- 17_Tools/SDKTool/FirmwareUpgrade.md
- 17_Tools/SDKTool/README.md

## Reference

- 15_Reference/SDKReference.md

## Failure Knowledge

- 07_FailureKnowledge/Firmware/

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-06 | Initial release |