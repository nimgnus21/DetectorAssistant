# Log Collection

> iDetector Software Module - Log Collection

---

# 1. Purpose

The **Log Collection** function is used to record software operation information during the execution of iDetector.

Collected logs provide important diagnostic information for:

- Software operation monitoring
- Detector communication analysis
- SDK debugging
- Image acquisition troubleshooting
- Calibration troubleshooting
- Firmware upgrade analysis
- Technical support

Log collection is one of the primary methods for locating software and communication problems.

---

# 2. Scope

This document describes the log collection function provided by the iDetector software.

The log module records software events generated during normal operation. The recorded content depends on the software version and current operating state.

---

# 3. Log Sources

Typical log information may include:

- Software startup
- Software shutdown
- Detector connection
- Detector disconnection
- SDK initialization
- SDK operation
- Image acquisition
- Calibration execution
- Firmware upgrade
- Parameter read/write
- Warning messages
- Error messages

---

# 4. Log Generation

Log records are generated automatically when the software performs operations.

Typical trigger events include:

- User operations
- Detector status changes
- Communication events
- SDK events
- Calibration operations
- Firmware upgrade operations
- Software exceptions

No manual operation is required to generate logs.

---

# 5. Typical Collection Process

```text
Software Starts

↓

Initialize Log Module

↓

User Operation

↓

Software Executes Command

↓

SDK Response

↓

Detector Response

↓

Operation Result

↓

Log Record Generated

↓

Display in Log Module
```

---

# 6. Log Content

A log entry may contain information such as:

- Time
- Module
- Operation
- Result
- Message
- Warning
- Error

The actual displayed fields depend on the software version.

---

# 7. Engineering Applications

Collected logs are commonly used for:

- Detector connection failures
- SDK initialization failures
- Acquisition failures
- Calibration failures
- Firmware upgrade failures
- Network communication analysis
- Technical support

Engineers should retain original log records before troubleshooting.

---

# 8. Best Practices

When collecting logs:

- Perform the complete operation before exporting logs.
- Avoid restarting the software before logs are saved.
- Keep detector connected if possible.
- Record detector information together with exported logs.
- Preserve logs before reproducing additional failures.

---

# 9. Notes

- Log collection does not affect normal detector operation.
- Log contents depend on software version.
- Some debugging information may only be available in specific software builds.
- Do not manually modify exported log files.

---

# 10. Related Documents

## Log Module

- LogAnalysis.md
- LogLocation.md
- ExportLog.md
- FAQ.md

## Related Knowledge Base

- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../11_Case
- ../../12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Log Collection documentation |