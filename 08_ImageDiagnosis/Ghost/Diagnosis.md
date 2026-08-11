# Ghost — Diagnosis

## Purpose
Classify residual image information associated with previous exposure history. Do not infer a hardware mechanism from one frame.

## Diagnostic Sequence

```text
Residual structure observed
→ compare with previous exposure
→ check whether residual follows prior image content
→ compare frame sequence
→ record exposure conditions
→ compare RAW / processed output where available
→ route to Image DecisionTree
```

## Evidence Required

- current image
- previous exposure image
- frame order
- exposure conditions
- repeated acquisition sequence
- RAW where available
- correction / dynamic-processing context

## Root-Cause Boundary

Ghost is a phenomenon classification. Detector response, dynamic correction, acquisition sequence, or processing mechanisms remain candidates until the sequence evidence supports a mechanism.

## Stop Condition

Do not classify a single residual-looking image as `Channel abnormality` or hardware failure without frame-history evidence.
