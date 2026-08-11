# Non-Uniformity — Diagnosis

## Purpose
Classify spatially uneven signal distribution without assigning a specific calibration or hardware root cause from appearance alone.

## Diagnostic Sequence

```text
Uneven signal distribution
→ determine global vs local pattern
→ compare repeated acquisitions
→ compare RAW / Dark where available
→ record exposure conditions
→ check Offset / Gain context
→ route to Image / Calibration DecisionTree
```

## Evidence Required

- RAW image where available
- processed image
- repeated acquisition results
- exposure conditions
- Dark / Offset / Gain context
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

Non-Uniformity is a phenomenon classification. Offset, Gain, exposure, detector response, processing, or hardware mechanisms remain candidates until evidence distinguishes them.

## Stop Condition

Do not convert spatial non-uniformity directly into `Channel abnormality` or hardware failure.
