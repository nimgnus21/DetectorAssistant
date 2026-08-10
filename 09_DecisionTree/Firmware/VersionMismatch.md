# Version Mismatch Decision Tree

> Module: Firmware
>
> Category: Decision Tree
>
> Version: v1.2
>
> Last Updated: 2026-08-10

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
    ↓
Firmware version readable?
    ├─ No → BootFailure
    └─ Yes → Compare approved compatibility requirement
                 ↓
          Firmware supported by SDK?
                 ├─ No → Select approved compatible SDK/package
                 └─ Yes → Detector model correct?
                              ├─ No → Verify product/model scope
                              └─ Yes → Configuration compatible?
                                           ├─ No → Configuration recovery
                                           └─ Yes → Calibration successful?
                                                        ├─ No → Calibration branch
                                                        └─ Yes → Acquisition successful?
                                                                     ├─ No → Image branch
                                                                     └─ Yes → Problem solved
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

## SDK

- SDK too old
- SDK too new
- Incorrect runtime library

## Configuration

- Old parameter file
- Configuration not updated
- Mode configuration mismatch

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

- [InitializationWorkflow](../../06_Workflow/InitializationWorkflow.md)
- [ConfigurationWorkflow](../../06_Workflow/ConfigurationWorkflow.md)

## Case

- [VersionMismatch](../../11_Case/Firmware/VersionMismatch.md)
- [FirmwareUpgradeFailed](../../11_Case/Firmware/FirmwareUpgradeFailed.md)
- [ParameterRecovery](../../11_Case/Firmware/ParameterRecovery.md)

## Tools

- [FirmwareUpgrade](../../17_Tools/SDKTool/FirmwareUpgrade.md)
- [SDKTool README](../../17_Tools/SDKTool/README.md)

## Failure Knowledge

- [FailureAnalysisMethod](../../07_FailureKnowledge/FailureAnalysisMethod.md)
- [FailureClassification](../../07_FailureKnowledge/FailureClassification.md)
- [FailureCode](../../07_FailureKnowledge/FailureCode.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.2 | 2026-08-10 | P0 Markdown link audit: removed nonexistent SDKReference target |
| v1.1 | 2026-08-10 | Replaced obsolete FirmwareUpgradeWorkflow and FirmwareFailure links with existing workflow and generic FailureKnowledge nodes |
| v1.0 | 2026-08-06 | Initial release |