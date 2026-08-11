# Dead Pixel — Diagnosis

## Purpose
Classify a suspected fixed pixel-coordinate artifact. Do not infer intrinsic detector damage from appearance alone.

## Diagnostic Sequence

```text
Point-like artifact
→ confirm fixed detector coordinate
→ compare repeated RAW images
→ check Dark / Offset / Gain context
→ inspect active Defect Template
→ repeat after applicable correction
→ route to Image DecisionTree
```

## Evidence Required

- repeated RAW images
- affected pixel coordinates
- Dark / Offset evidence where available
- active Defect Template and mapping
- before/after correction images
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

A fixed dark or bright pixel is a phenomenon classification. The underlying pixel condition, stale/incomplete defect mapping, or hardware mechanism must not be declared confirmed without supporting evidence.

## Stop Condition

Successful Defect compensation proves that the correction path worked; it does not by itself prove or disprove an underlying pixel-level hardware condition.
