# Vertical Line Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v1.1
>
> Last Updated: 2026-08-11

---

# Diagnostic Boundary

This DecisionTree routes a **vertical-line phenomenon**. It must not infer a specific failed channel, component, or hardware mechanism from image morphology alone.

`Column Readout / ADC / TFT / FPGA / Hardware` are candidate branches only after evidence supports them.

---

# Symptom Classification

□ Single bright line

□ Single dark line

□ Multiple lines

□ Fixed-position line

□ Intermittent line

□ Line appears only after exposure

□ Line appears in every image

□ Full-height / Partial-height

□ RAW confirmed / RAW not yet checked

Do not assign root cause at this stage.

---

# Diagnostic Flow

```text
Vertical Line
      │
      ▼
Repeated acquisitions?
      │
  ┌───┴───┐
  NO     YES
  │       │
Check    Continue
exposure    │
/history    ▼
       Fixed position?
          │
      ┌───┴───┐
     NO      YES
      │        │
 Check       Continue
 timing        │
 /acq         ▼
         RAW also contains line?
             │
       ┌─────┴─────┐
      NO           YES
       │             │
 Process /        Continue
 display              │
 branch               ▼
                Check Dark / calibration
```

---

# Calibration Evidence

Check:

1. Offset status / result
2. Gain status / result
3. Defect context where applicable
4. Dark image
5. RAW image

If calibration is abnormal, follow the Calibration DecisionTree.

If recalibration does not remove the line, record this as evidence. It does not by itself prove hardware failure.

---

# Software Boundary

Compare with SDK Demo where applicable.

```text
Customer Application only
→ investigate application / processing branch

SDK Demo also reproduces
→ continue detector-side evidence collection
```

SDK Demo reproduction is supporting evidence, not a standalone hardware proof.

---

# Hardware Candidate Branch

Only raise detector-side hardware mechanisms after evidence supports a persistent structured artifact, preferably including:

- fixed position;
- RAW confirmation;
- repeated acquisition;
- calibration checks;
- SDK Demo comparison where applicable;
- comparison detector / environment evidence where applicable.

Possible candidates may include:

- column readout path;
- TFT-related path;
- ADC / acquisition path;
- FPGA / data acquisition path;
- other detector-side hardware.

These are candidate mechanisms, not confirmed root causes.

---

# Required Evidence

Collect before escalation:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- Original RAW image
- Processed image
- repeated acquisitions
- abnormal column coordinate
- Dark image where available
- Offset / Gain context
- Calibration Log
- Detector Status Screenshot

---

# Root-Cause Output Rule

If only an image is available:

```text
Observed phenomenon: vertical line
Root Cause: Not Confirmed

Next evidence:
- RAW
- repeated images
- fixed column coordinate
- Dark / calibration context
- SDK Demo comparison where applicable
```

Do **not** output `Channel abnormality`, `ADC channel abnormal`, or a specific hardware failure as confirmed root cause from the image alone.

---

# Escalation Criteria

Escalate to hardware/R&D analysis when the evidence supports a persistent detector-side candidate and supported calibration/software branches do not explain the artifact.

Preserve the evidence package and uncertainty boundary in the escalation record.

---

# Related Documents

- [VerticalLine Case](../../11_Case/Image/VerticalLine.md)
- [Image Diagnosis](../../08_ImageDiagnosis/README.md)
- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v1.1 | 2026-08-11 | Added evidence-first routing and prohibited direct channel/hardware conclusions from image morphology alone |
| v1.0 | 2026-08-06 | Initial release |