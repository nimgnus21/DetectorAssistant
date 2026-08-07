# Customer Reply Template

> Module: Template
>
> Category: Customer Communication

---

# Overview

This document provides standardized customer reply templates for common detector support scenarios.

The templates are intended for Field Application Engineers (FAEs), Technical Support Engineers, and After-sales Engineers to improve communication efficiency and ensure complete technical information is collected before troubleshooting.

---

# Usage Principles

Before replying to the customer:

- Use professional and concise language.
- Clearly describe the required information.
- Avoid requesting duplicate information.
- Request original files whenever possible.
- Collect Detector.log before escalating issues.

---

# Template 1 - Initial Information Collection

**Applicable Scenarios**

- First customer contact
- New support case
- Insufficient issue description

---

Dear Customer,

To assist you in analyzing the issue, please provide the following information:

1. Detector Model
2. Detector Serial Number (SN)
3. SDK Version
4. Firmware Version
5. Detector.log
6. Software Name and Version
7. Operating System Version
8. Detailed problem description
9. Steps to reproduce the issue
10. Approximate occurrence time

Thank you.

---

# Template 2 - Detector Connection Failure

**Applicable Scenarios**

- Detector cannot be connected
- Detector not found
- Network communication failure

---

Dear Customer,

Please help verify the following items:

□ Detector power status

□ Network cable connection

□ Network port indicator LEDs

□ Detector IP address

□ Host computer IP address

□ Ping test result

□ Detector.log

□ Detector interface screenshot

□ SDK Version

□ Firmware Version

If possible, please provide screenshots of the network configuration.

Thank you.

---

# Template 3 - Unable to Acquire Image

**Applicable Scenarios**

- No image received
- Acquisition timeout
- Exposure completed without image

---

Dear Customer,

Please provide the following information:

□ Detector.log

□ Generator model

□ Exposure parameters (kV / mA / ms)

□ Trigger mode

□ Detector operating mode

□ Detector interface screenshot

□ Acquisition software screenshot

□ Whether Evt_Exp_Enable is received

□ Whether Evt_Image is received

□ Whether the issue is reproducible

Thank you.

---

# Template 4 - Image Quality Issue

**Applicable Scenarios**

- Artifact
- Noise
- Ghost
- Line defect
- Bright/Dark area
- Non-uniform image

---

Dear Customer,

Please provide:

□ Original image (Raw Image)

□ Corrected image

□ Detector.log

□ Offset template version

□ Gain template version

□ Defect template version

□ Detector front photo

□ Detector rear photo

□ Detector interface screenshot

□ Exposure parameters

□ Whether recalibration has been performed

Thank you.

---

# Template 5 - Calibration Failure

**Applicable Scenarios**

- Offset failure

- Gain failure

- Defect failure

---

Dear Customer,

Please provide:

□ Calibration type

□ Detector.log

□ Calibration images

□ Calibration workflow

□ SDK Version

□ Firmware Version

□ Detector SN

□ Error message screenshot

□ Current calibration templates

□ Whether the issue occurs repeatedly

Thank you.

---

# Template 6 - Firmware Upgrade Failure

**Applicable Scenarios**

- Firmware update failed
- Upgrade interrupted
- Version mismatch

---

Dear Customer,

Please provide:

□ Detector SN

□ Current firmware version

□ Target firmware version

□ Upgrade software version

□ Upgrade package

□ Detector.log

□ Upgrade screenshot

□ Error message

□ Whether power loss occurred during upgrade

Thank you.

---

# Template 7 - License Issue

**Applicable Scenarios**

- Image locked

- License invalid

- License expired

---

Dear Customer,

Please provide:

□ Detector SN

□ License file

□ Detector.log

□ SDK Version

□ Firmware Version

□ License error screenshot

□ Time when the issue occurred

Thank you.

---

# Template 8 - Communication Abnormality

**Applicable Scenarios**

- Detector disconnects frequently

- Packet loss

- Communication timeout

---

Dear Customer,

Please provide:

□ Detector.log

□ Network topology

□ Switch model

□ Cable type

□ Detector IP

□ Computer IP

□ Ping test result

□ Whether the issue is intermittent

□ Network configuration screenshots

Thank you.

---

# Template 9 - Factory Inspection / OQC

**Applicable Scenarios**

- Factory inspection

- Shipment verification

- RMA confirmation

---

Dear Customer,

Please provide the following files:

□ Detector interface screenshot

□ Image acquisition interface screenshot

□ Detector front photo

□ Detector rear photo

□ Package label photo

□ Firmware version information

□ Detector Serial Number

□ Test images

If firmware versions are inconsistent, please contact R&D before shipment.

Thank you.

---

# Template 10 - Remote Support Request

**Applicable Scenarios**

- Remote troubleshooting

- Joint debugging

---

Dear Customer,

Before arranging a remote support session, please prepare the following:

□ Detector.log

□ TeamViewer / AnyDesk ID

□ Meeting time

□ Detector connected and powered on

□ Generator available (if required)

□ Administrator privileges

□ Test environment ready

□ Stable Internet connection

Thank you.

---

# Recommended Attachments

When submitting a support request, it is recommended to include:

- Detector.log
- Original images
- Corrected images
- Detector interface screenshots
- Acquisition software screenshots
- Detector front/rear photos
- Package label photo
- Firmware version
- SDK version
- Detector SN
- Error screenshots

---

# Related Modules

- 11_Case
- 12_ErrorCode
- 09_DecisionTree
- 06_Workflow
- 07_FailureKnowledge

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.0 | 2026-08-07 | Initial release |