# License Failure Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.1
>
> Last Updated: 2026-08-10

---

# Purpose

This decision tree is used when the SDK cannot be activated because the software license is missing, invalid, expired, or incompatible.

Typical license workflow:

Application

↓

Load SDK

↓

Load License

↓

Verify License

↓

Initialize SDK

↓

Open Detector

↓

Acquire Image

Failure during license verification prevents the SDK from operating normally.

---

# Symptom

The SDK reports a license-related error.

Typical symptoms include:

- License Invalid
- License Not Found
- License Expired
- Activation Failed
- License Verification Failed
- Hardware Key Not Found
- License Server Unreachable
- SDK Initialization Failed (License)
- Image Locked（经现场验证的 License 相关场景）

---

# Symptom Classification

Identify the observed behavior.

□ License file missing

□ License expired

□ USB Dongle not detected

□ Computer fingerprint mismatch

□ License server unavailable

□ Activation failed

□ Offline activation failed

□ Image Locked

□ Unknown license error

---

# License Verification Pipeline

```
Application

↓

SDK

↓

License Manager

↓

License File / Dongle

↓

License Verification

↓

SDK Initialization

↓

Detector Ready
```

Verification Status

```
Application      □
SDK              □
License File     □
Dongle           □
Activation       □
Verification     □
Detector Ready   □
```

---

# Diagnostic Flow

```
             License Failure
                    │
           SDK Installed?
                    │
       ┌────────────┴────────────┐
       │                         │
      NO                        YES
       │                         │
Install SDK               Continue
                                  │
                                  ▼
        License File Exists?
                                  │
      ┌────────────┴────────────┐
      │                         │
     NO                        YES
      │                         │
Copy License File        Continue
                                  │
                                  ▼
      License Verification Passed?
                                  │
      ┌────────────┴────────────┐
      │                         │
     NO                        YES
      │                         │
Check Activation         Continue
                                  │
                                  ▼
     Hardware Key Detected?
                                  │
      ┌────────────┴────────────┐
      │                         │
     NO                        YES
      │                         │
Check Dongle             Continue
                                  │
                                  ▼
      Detector Opens?
                                  │
      ┌────────────┴────────────┐
      │                         │
     NO                        YES
      │                         │
SDK Investigation       Problem Solved
```

---

# License Classification

| Failure | Possible Cause | Next Action |
|----------|----------------|-------------|
| License Missing | File deleted | Restore license |
| License Expired | Expired activation | Renew license |
| Fingerprint Mismatch | New computer | Reissue license |
| USB Dongle Missing | Dongle unplugged | Reconnect dongle |
| License Server Offline | Server unavailable | Verify server |
| Invalid License | Wrong SDK version | Replace license |
| Image Locked | License abnormality confirmed by applicable field case | Verify and replace the corresponding license |

---

# Diagnosis Hint

License problems are usually unrelated to detector hardware.

Typical investigation order:

1. Verify license file.
2. Verify activation status.
3. Verify SDK version.
4. Verify computer fingerprint.
5. Verify hardware dongle.
6. Verify license server.

For license file replacement, backup and post-replacement acquisition verification, use the dedicated [License Management Tool](../../17_Tools/SDKTool/LicenseManagement.md).

---

# Software Hint

Most likely affected modules

★★★★★ License Manager

★★★★★ SDK

★★★★☆ Activation Service

★★★★☆ USB Dongle

★★★☆☆ Operating System

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| [License Management Tool](../../17_Tools/SDKTool/LicenseManagement.md) | Backup, replace and verify applicable LIC file | License verification and acquisition can proceed |
| SDK Demo | Verify activation | SDK starts normally |
| Device Manager | Detect USB dongle | Dongle detected |
| SDK Log | Verify license loading | Success |

---

# Expected Result

License successfully loaded.

License verification passed.

SDK initialized successfully.

Detector available.

Image acquisition available.

---

# Quick Checklist

Verify

□ License file exists

□ License path correct

□ License valid

□ Activation completed

□ SDK version matches

□ Dongle detected

□ Computer fingerprint matches

□ SDK Demo tested

---

# Required Evidence

Collect before escalation

- Detector Model
- Detector SN
- SDK Version
- License Version
- License Type
- Activation Status
- Error Code
- SDK Log
- License Screenshot

---

# Possible Root Causes

## License

- Missing license
- Invalid license
- Expired license

---

## SDK

- Version mismatch
- Activation failure

---

## Hardware

- USB dongle missing
- Dongle driver abnormal

---

## System

- Computer changed
- License path changed
- License server unavailable

---

# Recommended Actions

Priority 1

- Verify license file.

Priority 2

- Verify SDK version.

Priority 3

- Verify activation.

Priority 4

- Verify dongle or fingerprint.

Priority 5

- Test with SDK Demo.

Priority 6

- Use [License Management Tool](../../17_Tools/SDKTool/LicenseManagement.md) for applicable file replacement and verification.

Priority 7

- Escalate with license information.

---

# Escalation Criteria

Escalate when:

- License remains invalid after reactivation.
- SDK Demo reports the same license error.
- SDK version matches the license.
- Activation has been verified.

---

# Related Documents

## Software

- SDKInitializationFailed.md
- APIError.md
- SDKException.md
- [License Management Tool](../../17_Tools/SDKTool/LicenseManagement.md)

## Reference

- SDKReference.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.1 | 2026-08-10 | Linked License Management Tool and added Image Locked classification |
| v4.0 | 2026-08-06 | Initial release |