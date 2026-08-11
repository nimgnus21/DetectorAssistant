# Bad Row — Diagnosis

## Purpose
Classify a suspected fixed-row image phenomenon. This document does not confirm a failed row-readout channel or hardware component.

## Diagnostic Sequence

```text
Visible horizontal line / row pattern
→ confirm row orientation
→ check whether the row position is fixed
→ compare repeated images
→ check RAW
→ check Dark
→ check Offset / Gain / Defect context
→ route to Image DecisionTree
```

## Evidence Required

- RAW image
- repeated acquisitions
- abnormal row coordinate
- Dark image where available
- correction/template context
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

A fixed row pattern is a phenomenon classification. `Row Readout`, `Channel`, `TFT`, or other hardware mechanisms remain candidates until evidence confirms them.

## Stop Condition

If only one processed image is available, report the observed row pattern and required evidence. Do not output a specific channel or hardware failure as confirmed root cause.
