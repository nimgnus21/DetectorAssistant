# Firmware Upgrade Failed Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-10

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
    ↓
Communication OK?
    ├─ No → NetworkFailure / connection branch
    └─ Yes → Package correct?
                 ├─ No → Verify approved package
                 └─ Yes → Version compatible?
                              ├─ No → VersionMismatch
                              └─ Yes → Power stable?
                                           ├─ No → Correct power condition
                                           └─ Yes → Interrupted?
                                                        ├─ Yes → Controlled recovery/retry
                                                        └─ No → Verification/recovery branch
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

## Communication

- Network interruption
- Timeout during programming
- Unstable connection

## Power

- Power interruption
- Unstable power adapter

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

- Preserve failed-stage evidence.
- Perform approved firmware recovery if supported.

Priority 4

- Retry only after the failure branch is identified.
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

- [InitializationWorkflow](../../06_Workflow/InitializationWorkflow.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)

## Case

- [FirmwareUpgradeFailed](../../11_Case/Firmware/FirmwareUpgradeFailed.md)
- [VersionMismatch](../../11_Case/Firmware/VersionMismatch.md)
- [ParameterRecovery](../../11_Case/Firmware/ParameterRecovery.md)

## Tools

- [FirmwareUpgrade](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

## Reference

- [SDKReference](../../15_Reference/SDKReference.md)

## Failure Knowledge

- [FailureAnalysisMethod](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [FailureClassification](../../07_FailureKnowledge/FailureClassification.md)
- [FailureCode](../../07_FailureKnowledge/FailureCode.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Replaced obsolete FirmwareUpgradeWorkflow and FirmwareFailure links with existing workflow and generic FailureKnowledge nodes |
| v1.0 | 2026-08-06 | Initial release |