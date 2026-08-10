# Boot Failure Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.2
>
> Last Updated: 2026-08-10

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
    ↓
Power / link normal?
    ├─ No → Check power and physical connection
    └─ Yes → Detector detected by SDK?
                 ├─ No → Connection / DetectorOffline branch
                 └─ Yes → Firmware version readable?
                              ├─ No → Upgrade/recovery branch
                              └─ Yes → Configuration valid?
                                           ├─ No → Configuration recovery
                                           └─ Yes → Acquisition successful?
                                                        ├─ No → Image branch
                                                        └─ Yes → Problem solved
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

## Configuration

- Invalid detector parameters
- Startup configuration error

## Hardware

- Flash storage failure
- FPGA startup abnormal
- Power initialization failure

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

- Perform approved parameter/configuration recovery.
- Reboot detector.

Priority 4

- Re-upgrade firmware only when the package/version scope and failure branch justify recovery.

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

- [InitializationWorkflow](../../06_Workflow/InitializationWorkflow.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)

## Case

- [BootFailed](../../11_Case/Firmware/BootFailed.md)
- [VersionMismatch](../../11_Case/Firmware/VersionMismatch.md)
- [ParameterRecovery](../../11_Case/Firmware/ParameterRecovery.md)

## Tools

- [FirmwareUpgrade](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [LogExport](../../17_Tools/Log/LogExport.md)

## Failure Knowledge

- [FailureAnalysisMethod](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [FailureClassification](../../07_FailureKnowledge/FailureClassification.md)
- [FailureCode](../../07_FailureKnowledge/FailureCode.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.2 | 2026-08-10 | P0 Markdown link audit: repaired LogExport path and removed nonexistent SDKReference target |
| v1.1 | 2026-08-10 | Replaced obsolete FirmwareUpgradeWorkflow and FirmwareFailure links with existing workflow and generic FailureKnowledge nodes |
| v1.0 | 2026-08-06 | Initial release |