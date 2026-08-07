# Image List

> iDetector Acquire Module - Image List

---

# 1. Purpose

The **Image List** displays all images acquired during the current acquisition session.

It provides engineers with a centralized interface for reviewing, selecting, managing, and verifying acquired images before exporting, analyzing, or saving them.

The Image List is located on the right side of the **Acquire** page.

---

# 2. Scope

This document describes the Image List functions available in the Acquire module.

Typical operations include:

- Display acquired images
- Select an image
- Switch between images
- Review acquisition results
- Verify image sequence
- Prepare images for saving

The available functions depend on the iDetector software version.

---

# 3. Function Overview

The Image List records every image received during image acquisition.

Typical information displayed includes:

- Image Order
- Image Preview (Thumbnail)
- Acquisition Sequence
- Current Selected Image

The exact displayed information depends on the software version.

---

# 4. Engineering Applications

The Image List is commonly used for:

- Reviewing acquired images
- Comparing consecutive images
- Confirming image acquisition success
- Selecting images for detailed inspection
- Verifying sequence acquisition
- Checking image completeness

---

# 5. Typical Workflow

```text
Acquire Image

↓

Image Received

↓

Image Added To Image List

↓

Select Image

↓

Display Image

↓

Review Image Quality

↓

Save Image (Optional)
```

---

# 6. Sequence Acquisition

During sequence acquisition:

- New images are continuously appended to the Image List.
- Images are displayed in acquisition order.
- Engineers can verify whether image frames are missing.
- The Image List serves as the basis for cine playback and image saving.

---

# 7. Image Selection

Selecting an image from the Image List updates the main display window.

Engineers should verify:

- Correct image is selected.
- Image quality is acceptable.
- Image orientation is correct.
- Required correction has been applied.

---

# 8. Engineering Recommendations

When using the Image List:

- Review every acquired image before saving.
- Verify that no frames are missing during sequence acquisition.
- Compare adjacent images when investigating image abnormalities.
- Confirm the correct image is selected before export.
- Archive important engineering images promptly.

---

# 9. Common Issues

| Problem | Possible Cause |
|----------|----------------|
| Image not added to list | Acquisition failed |
| Image list not refreshed | Display refresh abnormal |
| Missing image | Communication interruption |
| Wrong image displayed | Incorrect image selected |
| Empty image list | No successful acquisition |

For troubleshooting, refer to:

- 07_FailureKnowledge
- 09_DecisionTree
- 11_Case

---

# 10. Related Documents

## Acquire Module

- README.md
- Acquisition.md
- SequenceAcquisition.md
- ImageCorrection.md
- ImageDisplay.md
- ImageSave.md
- FAQ.md

## Knowledge Base

- ../../07_FailureKnowledge
- ../../09_DecisionTree
- ../../11_Case

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial Image List documentation |