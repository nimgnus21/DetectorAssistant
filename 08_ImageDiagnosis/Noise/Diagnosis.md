# Noise — Diagnosis

## Purpose
Classify the observed noise pattern before assigning a mechanism.

## Diagnostic Sequence

```text
Noise-like abnormality
→ determine random vs fixed-pattern behavior
→ compare repeated acquisitions
→ compare Dark / RAW where available
→ record exposure conditions
→ check calibration context
→ route to Image DecisionTree
```

## Evidence Required

- repeated images
- RAW / Dark where available
- exposure parameters
- detector status
- calibration context
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

Noise is a phenomenon class. Electronics, exposure, environment, calibration, acquisition, interference, or processing mechanisms remain candidates until evidence distinguishes them.

## Stop Condition

Do not infer `Channel abnormality` from a noisy appearance or from a single image. Report the noise pattern and required evidence first.
