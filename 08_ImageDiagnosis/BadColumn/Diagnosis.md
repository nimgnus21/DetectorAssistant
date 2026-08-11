# Bad Column — Diagnosis

## Purpose
Classify a suspected fixed-column image phenomenon. This document does not confirm a failed column-readout channel or hardware component.

## Diagnostic Sequence

```text
Visible vertical line / column pattern
→ confirm column orientation
→ check whether the column position is fixed
→ compare repeated images
→ check RAW
→ check Dark
→ check Offset / Gain / Defect context
→ route to Image DecisionTree
```

## Evidence Required

- RAW image
- repeated acquisitions
- abnormal column coordinate
- Dark image where available
- correction/template context
- Detector model / SN / firmware / SDK

## Root-Cause Boundary

A fixed column pattern is a phenomenon classification. `Column Readout`, `Channel`, `TFT`, or other hardware mechanisms remain candidates until evidence confirms them.

## Stop Condition

If only one processed image is available, report the observed column pattern and required evidence. Do not output a specific channel or hardware failure as confirmed root cause.
