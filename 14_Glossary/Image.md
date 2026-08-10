# Image

> Module: Glossary
>
> Category: Image Terminology

---

# Overview

This document defines standardized terminology for detector image acquisition, image correction, image quality and image troubleshooting.

---

# Core Acquisition Terms

## Image

Digital image data acquired from the detector.

Related Terms: Raw Image, Corrected Image, Frame.

## Raw Image

Original detector image data before the configured correction chain is applied.

Typical Usage: calibration, troubleshooting and image quality analysis.

## Corrected Image

Image data after the applicable Offset, Gain and Defect corrections are applied.

## Dark Image

Image acquired without X-ray exposure.

Typical Usage: Offset calibration and investigation of background or stripe artifacts.

## Image Acquisition

The process of receiving image data from the detector.

---

# Artifact Terms

## Artifact

An unwanted image structure that does not represent the imaged object.

## Line Artifact

An abnormal horizontal or vertical line appearing in an image.

## Interference Stripe

A stripe artifact associated with external or environmental interference. In field diagnosis, a key characteristic is that the stripe may change or disappear when the detector position changes, including during repeated dark-image acquisition.

Related Terms: Dark Image, Environmental Interference, Line Artifact.

## Packet-Loss Artifact

A stripe or band-like image abnormality associated with missing transmitted image data. A typical field characteristic is multiple missing data segments with consistent band width.

Related Terms: Packet Loss, Network Communication.

## Calibration Stripe

A regular equal-width bright/dark alternating stripe pattern associated with the correction/template direction.

Related Terms: Calibration Template, Offset, Gain, Defect Correction.

## Defective Bar

An abnormal bar-shaped image region. For applicable products, the first documented handling direction is recalibration followed by verification.

Related Terms: Calibration, Image Verification.

## Defective Pixel

A pixel that does not respond according to detector specifications.

## Defect Line

A fixed abnormal line associated with a line-level detector defect or correction requirement.

## Black Dot Artifact

An abnormal localized black-dot structure appearing in an image.

## TFT Damage

Physical damage affecting the TFT array and potentially causing persistent image abnormalities.

---

# Correction Terms

## Offset Correction

Correction used to compensate detector background signal.

## Gain Correction

Correction used to compensate pixel response differences.

## Defect Correction

Correction using the applicable defect information to compensate defective pixels or lines.

## Calibration Template

The active calibration data set used by the image correction chain.

---

# Diagnostic Usage

For stripe or line complaints, terminology should follow the observed characteristics rather than using the generic term "horizontal line" for every condition:

- Fixed-position line → Line Artifact / fixed line diagnostic direction
- Stripe changes with detector position → Interference Stripe
- Multiple missing segments with consistent width → Packet-Loss Artifact
- Equal-width alternating bright/dark stripes → Calibration Stripe
- Bar-shaped abnormal region on applicable product → Defective Bar

---

# Related Documents

- 05_Calibration
- 07_FailureKnowledge/ImageFailure
- 09_DecisionTree/Image/HorizontalLine.md
- 13_Template/Work/LogCollection.md

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Standardized image artifact terminology and diagnostic distinctions |
| v1.0 | 2026-08-07 | Initial release |