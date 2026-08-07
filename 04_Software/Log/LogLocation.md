# Log Location

> iDetector Software Module - Log Storage Location

---

# 1. Purpose

The **Log Location** function describes where iDetector stores runtime log files and how engineers can locate these files for troubleshooting, technical support, and issue analysis.

Log files provide important diagnostic information and should be preserved whenever software abnormalities occur.

---

# 2. Scope

This document describes the log storage mechanism of the iDetector software.

Depending on the software version and configuration, log files may be stored in the software working directory or in a designated log directory.

The actual storage path is determined by the installed software version.

---

# 3. Log Storage

During software operation, log information is automatically written to log files.

Typical log contents include:

- Software startup
- Detector connection
- Detector disconnection
- SDK initialization
- Image acquisition
- Calibration
- Firmware upgrade
- Warning messages
- Error messages

---

# 4. Viewing Log Files

Log files can be accessed through the Log module or by opening the corresponding log storage directory.

If the software provides an **Open Log Folder** or similar function, it is recommended to use the built-in function to locate the log files.

If no such function is available, refer to the installation guide or software configuration for the log storage location.

---

# 5. Log File Management

Engineers should:

- Preserve original log files before troubleshooting.
- Export logs before uninstalling or reinstalling the software.
- Archive logs together with detector information and software version.
- Avoid modifying log file contents.

Log files should be retained until fault analysis is completed.

---

# 6. Engineering Recommendations

When submitting logs to technical support or R&D, include:

- Detector Model
- Detector Serial Number
- Software Version
- SDK Version
- Firmware Version
- Time of occurrence
- Description of the issue
- Corresponding log files

Providing complete information improves troubleshooting efficiency.

---

# 7. Notes

- Do not manually edit log files.
- Do not delete log files before confirming that issue analysis is complete.
- If multiple tests are performed, record the corresponding operation time for easier log correlation.
- The log storage location may vary between software versions.

---

# 8. Related Documents

## Log Module

- LogCollection.md
- LogAnalysis.md
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
| v1.0 | 2026-08-07 | Initial Log Location documentation |