# SDK Error Code - License

> Module: SDK
>
> Category: License-related Error Interpretation

---

# Overview

This document records SDK error codes that may appear during license verification, authorization loading, or license-dependent operations.

> **Evidence boundary:** the current SDK Programming Reference does **not** define a dedicated License command, event, or error-code family. Therefore, this document must not be used to infer that a generic SDK error uniquely proves a license failure.

License diagnosis requires the error code to be evaluated together with the installed license file, detector identity, SDK version, firmware version, `Detector.log`, and the actual operation being executed.

---

# Related Commands

No dedicated License command is defined in the current SDK Programming Reference.

---

# Related Events

- `Evt_GeneralError`
- `Evt_TaskResult_Failed`

---

# Diagnostic Entry Rule

```text
Generic SDK Error / Image Locked / Licensed Function Unavailable
        ↓
Collect error code + operation + license file + Detector.log
        ↓
Is authorization evidence present?
   ├── Yes → LicenseManagement → LicenseFailure DecisionTree
   └── No  → Follow the native error-code DecisionTree first
```

The generic error code is the **entry condition**, not the root-cause conclusion.

---

# Applicable Error Codes

## Err_AccessDenied

### Description

The requested operation is not permitted. During a license-dependent operation, this may indicate that the current operation is not authorized.

### Evidence Required

- Operation that returned the error
- Installed license file identity/version
- Detector model/SN relationship where applicable
- SDK version
- Firmware version
- `Detector.log` around the failure time

### Diagnostic Path

1. Verify whether the operation is actually license-dependent.
2. Verify the installed license using [LicenseManagement](../../17_Tools/SDKTool/LicenseManagement.md).
3. Check [LicenseFailure](../../09_DecisionTree/Software/LicenseFailure.md).
4. If authorization cannot be verified, do not conclude that `Err_AccessDenied` is caused by the license; continue with the operation-specific diagnosis.
5. After correction, restart the SDK, reconnect the detector, and verify acquisition or the affected function.

---

## Err_NotImplemented

### Description

The requested function is not implemented. A license restriction is only one possible interpretation; SDK, firmware, detector model, or feature support must also be checked.

### Diagnostic Path

1. Verify SDK version and supported API.
2. Verify detector firmware and model support.
3. If the feature is documented as license-dependent, verify the license using [LicenseManagement](../../17_Tools/SDKTool/LicenseManagement.md).
4. If version compatibility is the primary issue, enter [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md).

---

## Err_PreCondition

### Description

The required preconditions have not been satisfied. A license-related initialization dependency is possible, but detector initialization and runtime state must be checked first.

### Diagnostic Path

1. Verify SDK initialization through [SDKInitializationFailed](../../09_DecisionTree/Software/SDKInitializationFailed.md).
2. Verify detector state and required configuration.
3. If the operation is license-dependent, continue with [LicenseFailure](../../09_DecisionTree/Software/LicenseFailure.md) and [LicenseManagement](../../17_Tools/SDKTool/LicenseManagement.md).
4. Retry only after the required initialization and configuration conditions are satisfied.

---

# Field Experience Boundary

In field service, image locking or unavailable acquisition functions may be related to a license problem. This is a field-experience entry point, not a dedicated SDK error-code definition.

Typical verified workflow:

1. Preserve the current license file and relevant logs.
2. Verify the current license file.
3. Replace the license file only when the replacement is authorized and applicable.
4. Restart the SDK.
5. Reconnect the detector.
6. Verify normal image acquisition or the affected function.

---

# Evidence Package

Before escalation, collect:

- Exact SDK error code/event
- API or operation that triggered the error
- Installed license file information
- Detector model and applicable detector identity
- SDK version
- Firmware version
- `Detector.log`
- Screenshot or original symptom evidence
- Result after restart/reconnect or authorized license replacement

For log export, use [LogExport](../../17_Tools/SDKTool/LogExport.md).

---

# Related DecisionTree

- [LicenseFailure](../../09_DecisionTree/Software/LicenseFailure.md)
- [SDKInitializationFailed](../../09_DecisionTree/Software/SDKInitializationFailed.md)
- [VersionMismatch](../../09_DecisionTree/Firmware/VersionMismatch.md)

# Related Tool

- [LicenseManagement](../../17_Tools/SDKTool/LicenseManagement.md)
- [LogExport](../../17_Tools/SDKTool/LogExport.md)

# Related Case

- [ParameterRecovery](../../11_Case/Firmware/ParameterRecovery.md)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added evidence boundary and direct diagnostic/tool links without inventing dedicated license errors |
| v1.0 | 2026-08-07 | Initial release |