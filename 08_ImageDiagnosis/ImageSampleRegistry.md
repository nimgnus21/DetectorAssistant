# Image Sample Registry

## Purpose

Record actual abnormal images used to improve future image analysis. A sample is not a root-cause label by itself.

## Current samples

| Sample ID | Phenomenon | Source | Repository Artifact | Linked Case | Status |
|---|---|---|---|---|---|
| IMG-001 | Horizontal line | User-provided chat image | Pending repository artifact | `11_Case/Image/HorizontalLine.md` | Awaiting image file |
| IMG-002 | Image abnormality / suspected channel pattern | User-provided chat image | Pending repository artifact | `11_Case/Image/HorizontalLine.md` / `VerticalLine.md` after classification | Awaiting image file |
| IMG-003 | Additional abnormal image samples | User-provided chat images | Pending repository artifacts | Map after phenomenon classification | Awaiting image files |

## Promotion rule

A chat image becomes a reusable repository sample only after the actual image bytes are available to the repository. The sample entry must then include:

- Phenomenon
- Image type: RAW / Dark / Gain / Defect / Processed
- Detector model
- Firmware
- SDK
- Exposure condition
- Repeatability information
- Fixed coordinates or ROI when relevant
- Analysis conclusion status
- Linked DecisionTree
- Linked FailureKnowledge
- Linked Case

## Diagnostic learning rule

When a new image is analyzed:

```text
Image
→ Phenomenon classification
→ Compare with existing samples
→ Evidence extraction
→ Candidate mechanisms
→ Verification
→ Confirmed conclusion only if evidence supports it
→ Add/update sample metadata
→ Feed verified knowledge back to Case / FailureKnowledge / DecisionTree
```

Never use visual similarity alone to label `Read Channel`, `Gate Channel`, or `Hardware` as the root cause.
