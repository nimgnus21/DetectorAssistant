# Lag — Diagnosis

## Purpose
Classify persistence of previous-frame information during continuous acquisition. Do not infer a specific detector component from image appearance alone.

## Diagnostic Sequence

```text
Previous-frame information persists
→ confirm continuous acquisition
→ inspect frame order
→ compare current frame with previous frame
→ repeat under controlled acquisition conditions
→ compare RAW / processed output where available
→ route to Image DecisionTree
```

## Evidence Required

- consecutive frames
- acquisition sequence
- exposure conditions
- RAW where available
- processed images
- timing / acquisition context

## Root-Cause Boundary

Lag is a phenomenon classification. Detector response, timing, acquisition, dynamic correction, or processing mechanisms remain candidates until evidence distinguishes them.

## Stop Condition

Do not classify frame persistence from a single image and do not convert it directly into `Channel abnormality`.
