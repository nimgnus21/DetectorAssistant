# Phenomenon → Evidence → Candidate Root Cause

> P0-Image-3 diagnostic layer
> Version: v1.0
> Last Updated: 2026-08-11

## Purpose

This layer converts an observed image phenomenon into an evidence-driven candidate set. It does **not** identify a root cause from image morphology alone.

```text
Observed Image
    ↓
Phenomenon
    ↓
Feature Extraction
    ↓
Evidence Gate
    ↓
Candidate Mechanisms
    ↓
Verification
    ↓
Confirmed Root Cause / Not Confirmed
```

## Mandatory Output Contract

For every uploaded abnormal image, return:

```text
Observed phenomenon:
Pattern:
Position:
Extent:
Repeatability:
RAW status:
Current confidence:
Candidate mechanisms:
Evidence still required:
Root Cause: Not Confirmed | Confirmed
```

### Hard rule

A single image can establish an **observed phenomenon**, but cannot by itself establish:

- Channel failure
- Readout failure
- Gate failure
- Hardware failure
- Calibration failure
- Network failure
- Software root cause

`Channel abnormality` is always a candidate until channel-level evidence exists.

---

# 1. Universal Evidence Gate

Before selecting a mechanism, classify these features:

| Feature | Values |
|---|---|
| Shape | point / line / band / grid / block / ghost / global / mixed |
| Direction | horizontal / vertical / both / none |
| Position | fixed / moving / random / edge / center / whole image |
| Extent | local / partial width / full width / partial height / full image |
| Polarity | dark / bright / mixed |
| Repeatability | single / intermittent / repeated |
| RAW | present / absent / unknown |
| Frame history | related / unrelated / unknown |
| Exposure dependence | yes / no / unknown |
| Calibration dependence | yes / no / unknown |
| Processing dependence | yes / no / unknown |

If any feature needed for a branch is unknown, keep the branch as **Candidate**.

---

# 2. Point / Pixel Phenomena

## Bad Point / Black Point / White Point / Dead Pixel

```text
Point-like defect
    ↓
Same coordinate across repeated frames?
    ├─ NO → random / acquisition / noise candidate
    └─ YES
        ↓
Present in RAW?
        ├─ NO → processing / correction / display candidate
        └─ YES
            ↓
Defect Template / calibration explains it?
            ├─ YES → calibration/template candidate
            └─ NO → pixel/hardware candidate
```

Required evidence:

- RAW
- repeated images
- fixed X/Y coordinate
- Dark
- Defect Template
- Offset/Gain status

Do not label `hardware dead pixel` from a processed image alone.

## Bad Pixel Cluster

Apply the same gate as a single bad point, then record:

- cluster size
- geometry
- fixed coordinate
- whether the cluster follows a detector boundary or processing block

Candidate mechanisms:

- defect template / correction
- pixel cluster
- local detector hardware
- processing artifact

---

# 3. Horizontal Line / Horizontal Stripe / Exposure Row

```text
Horizontal artifact
    ↓
Repeated?
    ├─ NO → exposure / timing / transient candidate
    └─ YES
        ↓
Fixed row?
        ├─ NO → acquisition / timing / exposure candidate
        └─ YES
            ↓
RAW contains it?
            ├─ NO → processing / correction candidate
            └─ YES
                ↓
Dark / Offset / Gain / Defect explain it?
                ├─ YES → calibration candidate
                └─ NO → Row Readout / Gate / acquisition hardware candidate
```

Important: `horizontal line ≠ channel abnormality`.

Hardware candidates may include Row Readout, Gate Driver/TFT, timing logic, FPGA/acquisition path, but these require supporting evidence.

---

# 4. Vertical Line / Equal-Spaced Vertical Stripes

```text
Vertical artifact
    ↓
Repeated and fixed?
    ├─ NO → acquisition / interference candidate
    └─ YES
        ↓
RAW contains it?
        ├─ NO → processing / correction candidate
        └─ YES
            ↓
Calibration explains it?
            ├─ YES → calibration candidate
            └─ NO → Column / Readout / hardware candidate
```

Important: `vertical line ≠ Read channel failure`.

For equal-spaced vertical stripes, additionally record:

- stripe period in pixels
- number of stripes
- full/partial height
- whether period is stable across frames

Only after periodicity and RAW evidence are established should a channel/readout mechanism be considered.

---

# 5. Banding / Horizontal-Vertical Stripes / Structured Pattern

First classify:

```text
single line
→ line branch

regular repeated lines
→ periodic-pattern branch

broad bands
→ banding / uniformity branch

mixed horizontal + vertical grid
→ structured interference / processing / readout candidate
```

Required evidence:

- orientation
- period
- fixed position
- RAW
- repeated acquisition
- exposure dependence
- Dark comparison

Do not map all structured stripes to channel failure.

---

# 6. Irregular Artifact / Black Patch / Local Artifact

```text
Irregular artifact
    ↓
Fixed location?
    ├─ YES → detector / correction / pressure / hardware candidates
    └─ NO → acquisition / exposure / processing / environmental candidates
```

For black patches, distinguish:

- fixed black defect
- saturation-related dark region
- pressure artifact
- processing artifact
- detector physical condition

Evidence must include RAW and, where relevant, physical inspection.

---

# 7. Ghost / Lag

```text
Residual image
    ↓
Compare with previous exposure
    ↓
Previous image content reproduced?
    ├─ YES → Ghost candidate
    └─ NO
        ↓
Continuous-frame persistence?
        ├─ YES → Lag candidate
        └─ NO → other artifact candidate
```

Required evidence:

- previous frame
- current frame
- exposure sequence
- dose/exposure conditions
- continuous acquisition result
- RAW where available

Do not infer Ghost from a single residual-looking image.

---

# 8. Grain Noise / Background Jump / Background Drift

```text
Noise / background abnormality
    ↓
Random or structured?
    ├─ Random → noise / exposure / electronics / environment
    └─ Structured → fixed-pattern / interference / readout / calibration
```

Then compare:

```text
Dark
→ repeated Dark statistics
→ exposure condition
→ RAW
→ processed image
```

Background jump and background drift must be distinguished by time behavior:

- jump = discrete change
- drift = gradual change

Do not classify either as channel failure without channel-correlated evidence.

---

# 9. Gain-Loaded Non-Uniformity / Sensitivity Low

```text
Gain loaded
    ↓
Image grey distribution abnormal?
    ↓
Compare before/after Gain
    ↓
Gain file valid and matched?
    ↓
Gain generation condition valid?
    ↓
Uniformity / sensitivity measurement
```

Candidates:

- Gain data
- Gain generation condition
- calibration mismatch
- detector response
- exposure condition

Required evidence:

- Gain file/version
- before/after image
- exposure condition
- measured grey distribution
- calibration result

---

# 10. Grey Value Does Not Increase with Dose / Saturation Staircase

First determine whether the response is:

```text
linear → expected response range
compressed → saturation / processing candidate
flat → detector / acquisition / exposure candidate
stair-step → saturation / ADC / processing / acquisition candidate
```

Required evidence:

- multiple dose levels
- measured mean/ROI grey value
- RAW values
- exposure parameters
- saturation level
- curve or table

Do not conclude ADC/channel failure from one exposure point.

---

# 11. CrossTalk

```text
CrossTalk candidate
    ↓
Is signal from an active region appearing in a neighboring region?
    ↓
Repeat under controlled exposure
    ↓
Compare RAW and processed image
    ↓
Check geometry / distance / dose dependence
```

Candidates:

- detector pixel coupling
- readout coupling
- signal processing
- exposure geometry

Requires controlled comparison before hardware conclusion.

---

# 12. Microphony / EMC Interference

## Microphony

Check whether the artifact changes with:

- mechanical vibration
- detector movement
- pressure/contact
- cable movement

## EMC

Check correlation with:

- external equipment
- power state
- cable arrangement
- exposure timing
- environment

Do not infer EMC from stripe shape alone.

---

# 13. Stitching Error / Zipper Line / Image Shift

First determine whether the artifact is introduced during image assembly or already exists in RAW.

```text
RAW correct
→ stitching / processing / transfer candidate

RAW already wrong
→ acquisition / detector-side candidate
```

For image shift record:

- direction
- pixel displacement
- repeatability
- trigger timing
- frame sequence

For zipper line record:

- location
- periodicity
- frame boundary relationship
- RAW vs processed comparison

---

# 14. Pressure Artifact / Moisture / Detector Temperature

These are not purely image morphology problems.

Require physical/environmental evidence.

## Pressure Artifact

Record:

- pressure location
- pressure duration
- before/after image
- whether artifact disappears after release

## Moisture / 潮解

Record:

- environmental condition
- detector condition
- physical inspection
- image symptom
- duration/history

## Overheat

Record:

- detector temperature/status
- operating duration
- exposure frequency
- image symptom
- recovery after cooling

Do not classify environmental/physical causes solely from an image.

---

# 15. Image Drop / Network / Trigger No-Image

These are **not image morphology diagnoses** and should leave `08_ImageDiagnosis` once identified as acquisition/communication symptoms.

Route to:

```text
Image Drop
→ Network / Communication DecisionTree

Internal Trigger No Image
→ Trigger / Acquisition DecisionTree

External Trigger No Image
→ Trigger / Acquisition DecisionTree

Software Trigger Timeout
→ SDK / Acquisition DecisionTree

AED No Image
→ AED / Acquisition DecisionTree
```

Evidence:

- trigger event
- detector state
- SDK event/log
- timeout
- packet evidence where applicable
- exposure confirmation

---

# 16. Channel / Read / Gate Mechanism Gate

Never enter this branch merely because the image contains lines or stripes.

A channel/read/gate candidate requires a combination of evidence such as:

```text
fixed spatial relationship
+
repeatability
+
RAW presence
+
controlled acquisition comparison
+
calibration branch does not explain it
+
where applicable, channel/read/gate-specific evidence
```

The minimum acceptable conclusion from morphology alone is:

```text
Observed phenomenon: structured line/stripe artifact
Root Cause: Not Confirmed
```

---

# 17. Candidate Ranking

Use this order:

```text
1. Directly observed phenomenon
2. Evidence-supported mechanism
3. Common alternative mechanisms
4. Hardware-specific candidates
5. Rare mechanisms
```

Do not rank a hardware failure first simply because it is technically possible.

---

# 18. Evidence Sufficiency

### Level 0 — Image only

Allowed:

- phenomenon classification
- visible pattern description

Not allowed:

- confirmed root cause

### Level 1 — Image + repeatability

Allowed:

- fixed/intermittent classification
- stronger candidate ranking

### Level 2 — RAW + acquisition context

Allowed:

- detector-side vs processing-side separation

### Level 3 — Calibration / SDK / Tool evidence

Allowed:

- mechanism candidate with high confidence

### Level 4 — Controlled verification / repair / replacement

Allowed:

- confirmed root cause

---

# 19. Standard Final Response

When evidence is incomplete:

```text
Observed phenomenon: <phenomenon>

Image features:
- <shape>
- <direction>
- <position>
- <repeatability>

Current conclusion:
- Phenomenon confirmed
- Root Cause: Not Confirmed

Candidate mechanisms:
1. <candidate>
2. <candidate>
3. <candidate>

Required evidence:
- RAW
- repeated acquisition
- fixed coordinate / period
- Dark / calibration context
- acquisition sequence where applicable

Do not yet conclude:
- Channel failure
- Readout failure
- Gate failure
- Hardware failure
```

When evidence is sufficient:

```text
Observed phenomenon: <phenomenon>

Evidence:
- <evidence>

Verified mechanism:
- <mechanism>

Root Cause:
- <confirmed cause>

Verification:
- <test / replacement / recalibration result>

Knowledge Feedback:
- <updated ImageDiagnosis / DecisionTree / FailureKnowledge / Case>
```

---

# 20. Knowledge Feedback Rule

Every confirmed image case should update, when applicable:

```text
08_ImageDiagnosis
↕
09_DecisionTree
↕
07_FailureKnowledge
↕
11_Case
```

A new image sample must not be added as a generic example unless its phenomenon, evidence boundary, and conclusion are recorded.
