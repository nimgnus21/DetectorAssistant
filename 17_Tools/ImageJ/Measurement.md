# ImageJ Measurement

## Purpose

Measure image features consistently when troubleshooting detector image abnormalities.

## Input

- Original image
- Defined comparison target: row, column, region or repeated artifact

## Procedure

1. Open the image and confirm dimensions/bit depth.
2. Select the measurement type before recording results.
3. For local abnormality, use a defined ROI and record its location.
4. For line-like artifacts, compare multiple affected and unaffected rows or columns.
5. Record image name, ROI coordinates or selection method, and result.
6. Export or screenshot the measurement result for the support record.

## Interpretation

Measurement identifies an image characteristic; it is not a standalone root-cause conclusion. Combine the result with acquisition conditions, calibration status, network evidence and logs when required.

## Output

- ROI or line definition
- Measurement result
- Screenshot/exported evidence

## Related Documents

- [Common Operations](CommonOperations.md)
- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Case Template](../../00_Project/Templates/CaseTemplate.md)
