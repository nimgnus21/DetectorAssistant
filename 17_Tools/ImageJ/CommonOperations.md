# ImageJ Common Operations

## Scope

Use this file for detector image inspection and evidence generation. ImageJ is used for observation and measurement support; it does not by itself establish the detector root cause.

## Input

- Original image file or supported export
- Correct image dimensions and bit depth when known
- Problem description and acquisition condition

## Procedure

1. Open the original image without modifying the source file.
2. Confirm image dimensions and bit depth.
3. Use zoom and contrast display only to improve observation; do not treat display adjustment as a change in detector data.
4. Inspect the full image and then the abnormal region.
5. Use line or rectangular selections when comparing rows, columns or local regions.
6. Record the operation and preserve screenshots or measurement output.

## Output

- Annotated screenshot or measurement result
- Clear description of abnormal location and direction
- Evidence suitable for the related FailureKnowledge or Case

## Related Use

- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Image DecisionTree](../../09_DecisionTree/Image/)
- [Measurement](Measurement.md)

## Notes

Do not overwrite the original customer image. Keep the original file and save derived analysis separately.
