# Firmware Upgrade Failed Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.0
>
> Last Updated: 2026-08-06

---

# Symptom

Firmware upgrade cannot be completed successfully.

Typical symptoms include:

- Firmware upgrade failed.
- Upgrade interrupted.
- Programming timeout.
- Verification failed.
- Upgrade progress stops.
- Detector cannot restart after upgrade.

---

# Diagnostic Flow

```
                  Firmware Upgrade Failed
                               │
                 Detector Communication OK?
                               │
                ┌──────────────┴──────────────┐
                │                             │
               NO                            YES
                │                             │
     Go to Connection Tree            Continue
                                      │
                                      ▼
                      Firmware Package Correct?
                                      │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
             Verify Firmware File             Continue
                                              │
                                              ▼
                       Firmware Version Compatible?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
               Select Correct Package        Continue
                                              │
                                              ▼
                     Detector Battery / Power Stable?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
              Verify Power Supply           Continue
                                              │
                                              ▼
                         Upgrade Interrupted?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     YES                             NO
                      │                               │
              Restart Upgrade                 Continue
                                              │
                                              ▼
                     Firmware Verification Passed?
                                              │
                      ┌───────────────┴───────────────┐
                      │                               │
                     NO                              YES
                      │                               │
             Retry Upgrade / Recovery      Upgrade Successful
```

---

# Quick Checklist

Verify the following items:

- □ Detector communication is stable.
- □ Firmware package matches detector model.
- □ Firmware version is correct.
- □ SDK version is compatible.
- □ Stable power supply.
- □ Stable Ethernet connection.
- □ Upgrade process is uninterrupted.
- □ Firmware verification passes.

---

# Possible Root Causes

## Firmware

- Incorrect firmware package
- Corrupted firmware file
- Version incompatibility

---

## Communication

- Network interruption
- Timeout during programming
- Unstable connection

---

## Power

- Power interruption
- Unstable power adapter

---

## Software

- SDK version mismatch
- Upgrade tool abnormality

---

# Recommended Actions

Priority 1

- Verify detector communication.
- Verify firmware package.

Priority 2

- Verify firmware compatibility.
- Compare firmware version matrix.

Priority 3

- Restart upgrade procedure.
- Perform firmware recovery if supported.

Priority 4

- Replace firmware package.
- Escalate if repeated failures occur.

---

# Escalation Criteria

Escalate when:

- Firmware cannot be programmed repeatedly.
- Verification fails after multiple attempts.
- Detector cannot boot after upgrade.
- Recovery mode also fails.
- Flash hardware failure is suspected.

---

# Related Documents

## Workflow

- 06_Workflow/FirmwareUpgradeWorkflow.md

## Case

- 11_Case/Firmware/FirmwareUpgradeFailed.md
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