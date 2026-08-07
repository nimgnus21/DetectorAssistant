# FAQ

> Frequently Asked Questions - Log Module

---

# 1. Purpose

This document summarizes frequently asked questions related to the **Log** module in iDetector.

The Log module records software operation events and provides important information for troubleshooting, technical support, and engineering analysis.

---

# 2. Frequently Asked Questions

---

## Q1. Why is the Log window empty?

### Possible Causes

- No software operations have been performed.
- Logging has not yet started.
- The software has just been launched.

### Recommended Actions

- Perform the required operation again.
- Refresh the Log window.
- Verify that the software is operating normally.

---

## Q2. Why can't I find the required log information?

### Possible Causes

- The event did not occur.
- Log records have been cleared.
- The software has been restarted.

### Recommended Actions

- Reproduce the issue.
- Export logs immediately after the problem occurs.
- Avoid restarting the software before collecting logs.

---

## Q3. When should logs be exported?

Logs should be exported whenever:

- Detector connection fails.
- Image acquisition fails.
- Calibration fails.
- Firmware upgrade fails.
- Software crashes.
- Technical support or R&D requests diagnostic information.

---

## Q4. Can exported log files be modified?

No.

Exported log files should remain unchanged to preserve the original diagnostic information.

---

## Q5. Can log files be deleted?

It is not recommended to delete log files before issue analysis has been completed.

Always keep the original log files until troubleshooting is finished.

---

## Q6. What information should be submitted together with logs?

It is recommended to include:

- Detector Model
- Detector Serial Number
- Software Version
- SDK Version
- Firmware Version
- Problem Description
- Steps to Reproduce
- Exported Log Files

---

## Q7. Why are Warning messages displayed?

Warning messages indicate that an operation completed with conditions that may require attention.

Warnings do not always indicate a failure but should be reviewed together with the corresponding operation.

---

## Q8. Why are Error messages displayed?

Error messages indicate that an operation did not complete successfully.

Further investigation should be performed using:

- Detector status
- Software operation history
- Related log records
- Corresponding error information

---

## Q9. Should logs be provided to R&D?

Yes.

When an issue cannot be resolved locally, exported log files together with detector information should be provided to R&D for analysis.

---

## Q10. What is the best practice for using the Log module?

Recommended practices include:

- Review logs immediately after an issue occurs.
- Export logs before restarting the software.
- Preserve original log files.
- Record detector information together with exported logs.
- Archive logs with related engineering records.

---

# 3. Related Documents

## Log Module

- LogCollection.md
- LogAnalysis.md
- LogLocation.md
- ExportLog.md

## Related Knowledge Base

- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../11_Case
- ../../12_ErrorCode

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Log FAQ documentation |