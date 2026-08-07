# Save Image Failed Decision Tree

> Module: Software
>
> Category: Decision Tree
>
> Version: v4.0
>
> Last Updated: 2026-08-06

---

# Purpose

This decision tree is used when image acquisition completes successfully, but the image cannot be saved to the local storage.

Image saving failures usually occur **after successful acquisition** and are typically related to the operating system, file system, storage device, application configuration, or image encoding rather than the detector itself.

Typical workflow:

Application

↓

SDK Callback

↓

Image Buffer

↓

Image Conversion

↓

File Encoding

↓

File System

↓

Storage Device

↓

Image Saved

---

# Symptom

Image acquisition succeeds, but the image cannot be saved.

Typical symptoms include:

- Save Image Failed
- Failed to Save Image
- Cannot Create File
- Invalid Save Path
- Access Denied
- Disk Full
- Unsupported Image Format
- Image File Size = 0 KB
- File Saved but Cannot Open

---

# Symptom Classification

Identify the observed behavior.

□ Save failed immediately

□ Save timeout

□ Empty image file

□ Image file corrupted

□ Invalid image format

□ Permission denied

□ Disk full

□ File path invalid

□ Save only fails for one format

□ Save fails for all formats

---

# Image Save Pipeline

```
Application
      │
      ▼
SDK Image Buffer
      │
      ▼
Image Conversion
      │
      ▼
Encoder
      │
      ▼
File System
      │
      ▼
Storage Device
      │
      ▼
Image File
```

Verification Status

```
Application          □

SDK Buffer           □

Image Data           □

Encoder              □

File Path            □

Disk                 □

Image File           □
```

---

# Diagnostic Flow

```
                Save Image Failed
                        │
             Image Acquired Successfully?
                        │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
AcquisitionTimeout              Continue
                                       │
                                       ▼
              Image Buffer Valid?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
SDK Investigation              Continue
                                       │
                                       ▼
               Save Path Exists?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Create Directory               Continue
                                       │
                                       ▼
             Write Permission OK?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Check Permission              Continue
                                       │
                                       ▼
             Disk Space Enough?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Free Disk Space               Continue
                                       │
                                       ▼
           Image Format Supported?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
Verify Encoder                Continue
                                       │
                                       ▼
         Image Opens Successfully?
                                       │
         ┌──────────────┴──────────────┐
         │                             │
        NO                            YES
         │                             │
File Corrupted                 Problem Solved
```

---

# Save Failure Classification

| Failure Type | Possible Cause | Next Action |
|--------------|----------------|-------------|
| Invalid Path | Wrong directory | Verify path |
| Access Denied | Insufficient permissions | Run with proper permissions |
| Disk Full | Storage exhausted | Free disk space |
| Empty File | Buffer not written | Verify image buffer |
| Corrupted Image | Encoding failed | Verify encoder |
| Unsupported Format | Invalid file extension | Change format |
| Slow Save | Storage performance | Check disk health |

---

# Diagnosis Hint

Save failures generally occur after image acquisition has completed.

Recommended troubleshooting order:

1. Verify image acquisition success.
2. Verify image buffer.
3. Verify save directory.
4. Verify file permissions.
5. Verify available disk space.
6. Verify image encoding.
7. Verify saved file integrity.

Do not suspect detector hardware before verifying the local storage environment.

---

# Software Hint

Most likely affected modules

★★★★★ File System

★★★★★ Application

★★★★★ Image Encoder

★★★★☆ SDK Buffer

★★★★☆ Storage Device

★★★☆☆ Operating System

★★☆☆☆ Detector

---

# Diagnostic Tools

| Tool | Purpose | Expected Result |
|------|---------|----------------|
| SDK Demo | Save test image | Image saved successfully |
| File Explorer | Verify directory | Directory exists |
| Disk Management | Verify free space | Sufficient storage |
| Image Viewer | Open saved image | Image displayed correctly |
| SDK Log | Verify save process | Save completed |
| Event Viewer | Check file system errors | No write errors |

---

# Expected Result

### Image Acquisition

Expected Result

- Image acquisition completed successfully.

---

### Image Buffer

Expected Result

- Valid image buffer received.

---

### Save Directory

Expected Result

- Directory exists.
- Directory writable.

---

### Storage Device

Expected Result

- Sufficient free space.
- No disk errors.

---

### Output Image

Expected Result

- File generated successfully.
- File size is normal.
- Image opens correctly.

---

# Quick Checklist

Verify

□ Image acquisition completed

□ SDK buffer valid

□ Save path exists

□ Write permission granted

□ Disk space sufficient

□ Image format supported

□ Image file size normal

□ Image opens successfully

□ SDK Demo reproduces issue

---

# Required Evidence

Collect before escalation

- Detector Model

- Detector SN

- SDK Version

- Firmware Version

- Save Path

- Image Format

- File Size

- SDK Log

- Error Code

- Screenshot of Save Failure

- Example Saved File (if generated)

---

# Possible Root Causes

## Application

- Invalid save path
- Incorrect file name
- Invalid extension
- Buffer released before saving

---

## SDK

- Save interface failed
- Buffer corruption
- Encoder failure

---

## Operating System

- Folder permission denied
- Path length limitation
- Antivirus blocking write access

---

## Storage Device

- Disk full
- Read-only media
- Storage hardware failure

---

## Image Format

- Unsupported format
- Incorrect encoder
- Invalid image header

---

# Recommended Actions

Priority 1

- Verify acquisition completed successfully.

Priority 2

- Verify save directory exists.

Priority 3

- Verify write permission.

Priority 4

- Verify available disk space.

Priority 5

- Save using SDK Demo.

Priority 6

- Save to another directory or storage device.

Priority 7

- Escalate with logs and sample files if reproducible.

---

# Escalation Criteria

Escalate when:

- SDK Demo also fails to save images.
- Image buffer is confirmed valid.
- Storage device is healthy.
- Save path and permissions are correct.
- Different directories produce the same result.
- Multiple image formats fail.

---

# Related Documents

## Software

- 09_DecisionTree/Software/SDKInitializationFailed.md
- 09_DecisionTree/Software/DetectorNotFound.md
- 09_DecisionTree/Software/AcquisitionTimeout.md
- 09_DecisionTree/Software/APIError.md
- 09_DecisionTree/Software/SDKException.md
- 09_DecisionTree/Software/DetectorBusy.md

## Image

- 09_DecisionTree/Image/ImageLoss.md

## Reference

- 15_Reference/SDKReference.md

## Tools

- 17_Tools/SDKDemo.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v4.0 | 2026-08-06 | Initial release |