# FAQ

> Frequently Asked Questions — Detector Module

---

# 1. Purpose

This document summarizes the most frequently encountered questions related to the **Detector** module of the iDetector software.

It is intended to help Field Application Engineers (FAEs), Technical Support Engineers, and Service Engineers quickly identify common detector issues and locate the corresponding troubleshooting documents.

For detailed troubleshooting procedures, refer to the corresponding **Failure Knowledge**, **Decision Tree**, and **SOP** documents.

---

# 2. Frequently Asked Questions

---

## Q1. Why is my detector not displayed in the Device List?

### Possible Causes

- Detector is powered off.
- Network connection is abnormal.
- Detector and PC are on different network segments.
- SDK initialization failed.
- Detector communication service is unavailable.

### Recommended Actions

- Verify detector power.
- Check Ethernet or Wi-Fi connection.
- Verify IP configuration.
- Restart iDetector.
- Restart the detector.
- Refer to:

    - DetectorConnection.md
    - 09_DecisionTree/Connection
    - 07_FailureKnowledge/Communication

---

## Q2. Why can't the detector connect?

### Possible Causes

- Detector is already occupied.
- Network communication failure.
- SDK communication failure.
- Incorrect detector configuration.

### Recommended Actions

- Verify detector status.
- Restart detector communication.
- Check network connectivity.
- Verify SDK operation.
- Collect software logs if necessary.

---

## Q3. Why is the detector always Offline?

### Possible Causes

- Detector disconnected.
- Detector startup failed.
- Communication interruption.
- Incorrect network configuration.

### Recommended Actions

- Check detector power.
- Verify network connection.
- Refresh the Device List.
- Restart the detector.
- Restart iDetector.

---

## Q4. Why is detector information incomplete?

### Possible Causes

- Communication interrupted.
- Detector not fully initialized.
- SDK failed to obtain detector information.

### Recommended Actions

- Reconnect the detector.
- Refresh detector information.
- Restart the software.
- Verify firmware compatibility.

---

## Q5. Why is firmware version unavailable?

### Possible Causes

- Detector communication abnormal.
- Firmware query failed.
- Detector initialization incomplete.

### Recommended Actions

- Reconnect the detector.
- Verify communication.
- Restart detector.
- Check firmware compatibility.

---

## Q6. Why does the detector remain Busy?

### Possible Causes

- Image acquisition in progress.
- Calibration running.
- Previous operation not completed.
- Communication timeout.

### Recommended Actions

- Wait for current task to finish.
- Verify acquisition status.
- Verify calibration status.
- Restart detector if necessary.

---

## Q7. Why is the detector status not updated?

### Possible Causes

- Communication interruption.
- SDK status not refreshed.
- Software interface not updated.

### Recommended Actions

- Refresh detector information.
- Reconnect detector.
- Restart iDetector.
- Collect diagnostic logs.

---

## Q8. Why does the detector disconnect automatically?

### Possible Causes

- Network instability.
- Detector power interruption.
- Communication timeout.
- Hardware fault.

### Recommended Actions

- Check power supply.
- Verify network quality.
- Review software logs.
- Verify detector hardware status.

---

# 3. Engineering Recommendations

When troubleshooting detector-related issues:

- Verify detector power before software troubleshooting.
- Confirm the detector appears in the Device List.
- Verify detector communication before image acquisition.
- Record detector information before firmware upgrade.
- Collect diagnostic logs before escalating issues.
- Follow the Decision Tree before replacing hardware.

---

# 4. Related Documents

## Software Module

- README.md
- DeviceList.md
- DetectorInformation.md
- DetectorConnection.md
- DetectorStatus.md
- DetectorConfiguration.md

## Knowledge Base

- 03_Hardware
- 06_Workflow
- 07_FailureKnowledge
- 09_DecisionTree
- 10_SOP
- 11_Case
- 12_ErrorCode
- 17_Tools

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Detector FAQ documentation |