# Image Reference

> Version: v1.0
>
> Status: Draft
>
> Last Updated: 2026-08-06

---

# 1. Purpose

This document serves as the navigation reference for all image-quality related knowledge within DetectorAssistant.

It connects image symptoms, engineering diagnosis, detector principles, troubleshooting workflows, calibration procedures, and field cases into a unified knowledge network.

This document does not explain image artifacts in detail.

Instead, it provides the entry point for locating the correct technical documentation.

---

# 2. Scope

Image-related knowledge includes:

- Image Artifacts
- Image Quality
- Detector Defects
- Exposure Abnormalities
- Calibration Influence
- Generator Influence
- External Equipment Influence

---

# 3. Image Symptom Mapping

| Image Symptom | Image Diagnosis | Case | Decision Tree | Failure Knowledge |
|---------------|----------------|------|---------------|-------------------|
| Noise | Noise.md | Image/Noise.md | Noise Tree | Noise Mechanism |
| Ghost | Ghost.md | Image/Ghost.md | Ghost Tree | Ghost Principle |
| Vertical Line | VerticalLine.md | VerticalLine.md | Vertical Line Tree | TFT Readout |
| Horizontal Line | HorizontalLine.md | HorizontalLine.md | Horizontal Line Tree | Gate Driver |
| Image Shift | ImageShift.md | ImageShift.md | Image Shift Tree | Readout Timing |
| Mosaic | Mosaic.md | Mosaic.md | Mosaic Tree | Communication |
| Lag | Lag.md | Lag.md | Lag Tree | Detector Timing |
| Black Dots | BlackDots.md | BlackDots.md | Pixel Defect Tree | Pixel Defect |
| White Dots | WhiteDots.md | WhiteDots.md | Pixel Defect Tree | Pixel Defect |

---

# 4. Related Calibration

Image abnormalities may originate from calibration.

Related documents:

- Offset Calibration
- Gain Calibration
- Ghost Correction

Always verify calibration status before investigating hardware.

---

# 5. Related Hardware

Image abnormalities may originate from detector hardware.

Related modules:

- TFT Panel
- Gate Driver
- Readout Circuit
- ADC
- FPGA
- Detector Power

---

# 6. Related Software

Image abnormalities may originate from software.

Related modules:

- SDK
- Mode Configuration
- Image Buffer
- Trigger Synchronization
- Display Processing

---

# 7. Related External Equipment

Image abnormalities may originate from external devices.

Typical sources include:

- X-ray Generator
- Anti-scatter Grid
- Exposure Parameters
- Mechanical Installation
- Synchronization Signal

---

# 8. Engineering Troubleshooting Sequence

Recommended troubleshooting order:

1. Confirm image symptom.
2. Review Image Diagnosis.
3. Follow the corresponding Decision Tree.
4. Check related Case documents.
5. Verify Calibration.
6. Verify Detector Configuration.
7. Verify External Equipment.
8. Investigate Hardware only after previous steps have been completed.

---

# 9. Related Documents

## Image Diagnosis

08_ImageDiagnosis/

## Case

11_Case/Image/

## Decision Tree

09_DecisionTree/

## Calibration

05_Calibration/

## Failure Knowledge

07_FailureKnowledge/

## Workflow

06_Workflow/

## Tools

17_Tools/

---

# 10. Maintenance Rules

Review this document when:

- A new image symptom is added.
- A new detector model introduces different image characteristics.
- A new troubleshooting workflow is published.
- Field engineering experience identifies new image-related failure patterns.

This document should always remain the primary navigation entry for image-related knowledge.