# Calibration

> Module: Standard Operating Procedure
>
> SOP ID: SOP-003
>
> Category: Detector Calibration
>
> Version: v1.1

---

# Scope

This SOP describes the standard procedure for detector calibration, including Offset, Gain, Defect, and hardware calibration template management.

This procedure applies to:

- New detector installation
- Detector replacement
- Detector maintenance
- Firmware upgrade requiring recalibration
- Image quality recovery
- Factory calibration verification

---

# Objective

Generate valid calibration templates and verify that they are correctly applied to ensure stable detector performance and optimal image quality.

---

# Responsibility

| Role | Responsibility |
|------|----------------|
| FAE | Execute calibration and verify results |
| Technical Support Engineer | Provide remote support for abnormal calibration |
| Production Engineer | Perform factory calibration |
| R&D Engineer | Analyze abnormal calibration failures |

---

# Preconditions

Before calibration, confirm:

- Detector status is **Ready**.
- Detector communication is normal.
- Detector firmware matches the SDK version.
- Correct calibration SubSet has been selected.
- Detector temperature is within the operating range.
- No calibration task is currently running.
- Stable power supply is available.
- Stable X-ray generator output is available.
- Detector has completed warm-up if required.

---

# Required Tools

## Hardware

- Detector
- Host Computer
- X-ray Generator
- Calibration Fixture (if required)

## Software / Diagnostics

- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- [DTDI Tool](../17_Tools/SDKTool/DTDITool.md)
- [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md)
- [Offset Viewer](../17_Tools/OffsetViewer/)（Offset 结果或异常分析时）
- [Log Viewer](../17_Tools/LogViewer/)（重复失败或 SDK 事件分析时）

---

# Required Files

- Calibration Configuration
- Existing Calibration Templates (if applicable)
- Detector.log
- DynamicApplicationMode.ini (Dynamic Detector)

---

# Safety Precautions

Before calibration:

- Verify detector communication is stable.
- Do not disconnect the detector during calibration.
- Do not interrupt template generation.
- Ensure generator output remains stable.
- Preserve original calibration templates before replacement.

---

# Calibration Workflow

```text
Detector Ready

↓

Select Calibration SubSet

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Download Templates

↓

Select Templates

↓

Verify Image Quality

↓

Calibration Complete
```

---

# Procedure

## Step 1 – Verify Detector Status

### Input

Connected detector.

### Process

- Verify detector state is Ready.
- Verify firmware version.
- Verify SDK version.
- Read detector temperature.
- Read detector humidity.

### Output

Detector verified.

### Acceptance Criteria

Detector operates normally.

### Exception Handling

Resolve connection or initialization problems before calibration. Use the [Connection DecisionTree](../09_DecisionTree/Connection/) and [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md) when the detector is not Ready.

---

## Step 2 – Select Calibration SubSet

### Input

Detector application mode.

### Process

- Select the appropriate Calibration SubSet.
- Verify the selected Application Mode.
- Confirm configuration parameters.

### Output

Calibration SubSet loaded.

### Acceptance Criteria

Correct SubSet selected.

### Exception Handling

Check `DynamicApplicationMode.ini` and `Cmd_SetCaliSubset` using the applicable [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md) workflow.

---

## Step 3 – Generate Offset Template

### Input

Detector Ready.

### Process

- Execute Offset Generation.
- Wait for task completion.
- Verify template generation.

### Output

Offset Template generated.

### Acceptance Criteria

Generation completed successfully.

### Exception Handling

Preserve `Detector.log`; use [Log Viewer](../17_Tools/LogViewer/) for repeated failures. Refer to the [Calibration DecisionTree](../09_DecisionTree/Calibration/) and applicable calibration error-code documentation.

---

## Step 4 – Generate Gain Template

### Input

Uniform X-ray exposure.

### Process

- Execute Gain Initialization.
- Acquire required images.
- Select images.
- Generate Gain Template.

### Output

Gain Template generated.

### Acceptance Criteria

Generation completed successfully.

### Exception Handling

Check:

- Generator output
- Image quantity
- Image quality

Use [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md) or [DTDI Tool](../17_Tools/SDKTool/DTDITool.md) according to the applicable product procedure. Preserve logs before repeated retries.

---

## Step 5 – Generate Defect Template

### Input

Calibration images.

### Process

- Execute Defect Initialization.
- Select calibration images.
- Generate Defect Template.

### Output

Defect Template generated.

### Acceptance Criteria

Generation completed successfully.

### Exception Handling

Verify the required calibration images and run the applicable [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md) procedure. For repeated failure, retain images, templates and `Detector.log`.

---

## Step 6 – Download Calibration Templates

### Input

Generated templates.

### Process

- Download Offset Template.
- Download Gain Template.
- Download Defect Template.
- Download PreOffset Template (if applicable).

### Output

Templates stored inside detector.

### Acceptance Criteria

Download completed successfully.

### Exception Handling

Verify communication first, then inspect template compatibility. Use [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md) and [Log Viewer](../17_Tools/LogViewer/) when an error is reported.

---

## Step 7 – Select Calibration Templates

### Input

Downloaded templates.

### Process

- Select Offset Template.
- Select Gain Template.
- Select Defect Template.
- Verify active template.

### Output

Templates activated.

### Acceptance Criteria

Detector reports successful selection.

### Exception Handling

Verify template type, compatibility and SubSet before replacing files.

---

## Step 8 – Verify Image Quality

### Input

Detector Ready.

### Process

- Acquire test image.
- Verify image uniformity.
- Verify defect correction.
- Verify image noise.
- Verify ghost artifacts.
- Verify line artifacts.

Use [Offset Viewer](../17_Tools/OffsetViewer/) when Offset-related abnormality is suspected.

### Output

Calibration verified.

### Acceptance Criteria

- Uniform image
- No obvious artifacts
- Normal detector response

### Exception Handling

Refer to:

- [Image Troubleshooting SOP](ImageTroubleshooting.md)
- [Image DecisionTree](../09_DecisionTree/Image/)
- [Calibration Stripe](../07_FailureKnowledge/ImageFailure/CalibrationStripe.md)

---

## Step 9 – Complete Calibration

### Input

Verified detector.

### Process

- Archive generated templates.
- Save Detector.log.
- Record firmware version.
- Record SDK version.
- Record calibration version.
- Record tools used and validation images.

### Output

Calibration completed.

---

# Acceptance Checklist

- Detector Ready
- Correct Calibration SubSet
- Offset Template generated
- Gain Template generated
- Defect Template generated
- Templates downloaded
- Templates selected
- Test image verified
- Detector.log archived
- Tool output retained when used for diagnosis

---

# Exception Matrix

| Symptom | Direction | Action |
|----------|-----------|--------|
| Offset generation failed | Detector state / interval / calibration process | Preserve log and follow Calibration DecisionTree |
| Gain generation failed | Exposure or calibration input | Verify generator output and input images |
| Defect generation failed | Image quantity or image selection | Reacquire required calibration images |
| Template download failed | Communication or template compatibility | Verify connection and inspect logs |
| Template selection failed | Template type / SubSet | Verify compatibility before replacement |
| Image artifacts remain | Calibration not effective or another fault class | Enter Image Troubleshooting and Image DecisionTree |

---

# Records

Record the following information:

- Customer Name
- Detector Model
- Detector Serial Number
- Calibration Date
- Operator
- SDK Version
- Firmware Version
- Calibration SubSet
- Template Version
- Detector.log
- Test Images
- Tool outputs used for diagnosis

---

# Notes

- For **dynamic detectors**, **Cmd_SetCaliSubset** must be executed before calibration and after a detector reset to ensure the correct Application Mode is loaded.
- If **HW_Gain** is used, the corresponding **PreOffset** template must also use hardware correction.
- Hardware calibration templates must be downloaded to the detector before they can be selected and used.
- During template generation, do not disconnect the detector or interrupt communication.
- If calibration fails repeatedly, preserve **Detector.log**, calibration images, and template files before escalating the issue.

---

# Related Documents

- [Calibration Module](../05_Calibration/README.md)
- [Calibration DecisionTree](../09_DecisionTree/Calibration/)
- [Calibration Cases](../11_Case/Calibration/)
- [Image Troubleshooting SOP](ImageTroubleshooting.md)
- [Image DecisionTree](../09_DecisionTree/Image/)
- [Calibration Stripe](../07_FailureKnowledge/ImageFailure/CalibrationStripe.md)
- [SDK Tool / iDetector](../17_Tools/SDKTool/iDetectorQuickTroubleshooting.md)
- [Calibration Tools](../17_Tools/SDKTool/CalibrationTools.md)
- [DTDI Tool](../17_Tools/SDKTool/DTDITool.md)
- [Offset Viewer](../17_Tools/OffsetViewer/)
- [Log Viewer](../17_Tools/LogViewer/)

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| v1.1 | 2026-08-10 | Added direct tool links and calibration-to-image verification flow |
| v1.0 | 2026-08-07 | Initial release |