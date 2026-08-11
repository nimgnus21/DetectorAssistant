# Banding — Diagnosis

## Purpose
Classify regular band / stripe patterns without assigning a specific hardware or channel root cause from morphology alone.

## Diagnostic Sequence

```text
Band / stripe observed
→ determine orientation
→ determine periodicity
→ determine fixed vs variable position
→ compare repeated images
→ check RAW
→ check exposure / acquisition conditions
→ check calibration context
→ route to Image DecisionTree
```

## Evidence Required

- original image
- RAW where available
- repeated acquisitions
- orientation and periodicity
- exposure parameters
- calibration context
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

Banding is a phenomenon class. Readout, interference, calibration, exposure, processing, or communication mechanisms must remain candidates until evidence distinguishes them.

## Stop Condition

Do not convert a band or stripe pattern directly into `Channel abnormality`. If evidence is insufficient, report the pattern and the next required checks.
