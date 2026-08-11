# Horizontal Line Decision Tree

> Module: Image
>
> Category: Decision Tree
>
> Version: v2.1
>
> Last Updated: 2026-08-11

---

# Diagnostic Boundary

This DecisionTree routes a **horizontal-line phenomenon**. It must not infer a specific failed channel, component, or hardware mechanism from image morphology alone.

`Channel / Row Readout / Gate Driver / TFT / FPGA` are candidate branches only after the required evidence is collected.

---

# Symptom

Horizontal line artifacts appear in the acquired image.

Typical symptoms include:

- Single horizontal line
- Multiple horizontal lines
- Bright horizontal line
- Dark horizontal line
- Fixed-position horizontal line
- Intermittent horizontal line

---

# Step 1 — Phenomenon Classification

Identify:

□ Single / Multiple

□ Bright / Dark

□ Fixed / Changing position

□ Every image / Intermittent

□ Full-width / Partial-width

□ RAW confirmed / RAW not yet checked

Do not assign a root cause at this stage.

---

# Step 2 — Reproducibility

```text
Horizontal Line
      │
      ▼
Appears in repeated acquisitions?
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

# Step 3 — Calibration Evidence

Check, in order:

1. Offset status / result
2. Gain status / result
3. Defect context where applicable
4. Dark image
5. RAW image

If calibration data is abnormal, follow the Calibration DecisionTree.

If recalibration does not remove the line, record that as evidence. Do not convert this result directly into hardware failure.

---

# Step 4 — Software Boundary

Compare with SDK Demo when applicable.

```text
Customer Application only
→ investigate application / processing branch

SDK Demo also reproduces
→ continue detector-side evidence collection
```

This comparison does not by itself prove hardware failure.

---

# Step 5 — Hardware Candidate Branch

Only enter the hardware candidate branch when evidence supports all or most of the following:

- line is repeatable;
- position is fixed or otherwise structurally consistent;
- RAW contains the same artifact;
- relevant calibration checks do not explain it;
- SDK Demo reproduces it where applicable;
- comparison detector / environment evidence is available where applicable.

Possible candidate mechanisms may include:

- row readout path;
- Gate Driver / TFT gate control;
- timing-related logic;
- FPGA / acquisition path;
- other detector-side hardware.

These remain **candidate mechanisms** until hardware or equivalent technical evidence confirms them.

---

# Required Evidence

Collect:

- Detector Model
- Detector SN
- Firmware Version
- SDK Version
- RAW Image
- Processed / Window Image
- repeated acquisitions
- abnormal row coordinate
- Dark image where available
- Offset / Gain context
- Calibration Log
- Detector Status

---

# Root-Cause Output Rule

If only an image is available, output:

```text
Observed phenomenon: horizontal line
Root Cause: Not Confirmed

Next evidence:
- RAW
- repeated images
- fixed row coordinate
- Dark / calibration context
- SDK Demo comparison where applicable
```

Do **not** output `Channel abnormality` as a confirmed conclusion from the image alone.

---

# Escalation Criteria

Escalate to hardware/R&D analysis when the collected evidence supports a persistent detector-side candidate and the supported calibration/software branches do not explain the artifact.

The escalation record must preserve the evidence package and the exact uncertainty boundary.

---

# Related Documents

- [HorizontalLine Case](../../11_Case/Image/HorizontalLine.md)
- [Image Diagnosis](../../08_ImageDiagnosis/README.md)
- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)

---

# Revision History

| Version | Date | Description |
|---|---|---|
| v2.1 | 2026-08-11 | Added evidence-first routing and prohibited direct channel/hardware conclusions from image morphology alone |
| v2.0 | 2026-08-06 | Added Diagnosis Hint and Hardware Hint |