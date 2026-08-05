# CalibrationTiming

Version: V2.0

Module: Calibration Theory

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- CalibrationOverview.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md
- CalibrationFlow.md
- ../../02_System/TimingArchitecture.md
- ../../02_System/ImagePipeline.md

---

# 1. Purpose

Calibration Timing 描述数字平板探测器校准在整个系统生命周期中的执行时机及各类 Calibration 的时序关系。

Calibration Timing 用于说明：

- Calibration 在何时执行
- Calibration 与正常曝光的关系
- Calibration 与图像采集流程的关系
- Calibration 数据在何时参与图像处理

本文件不涉及具体校准算法及操作流程。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

---

# 3. Definition

Calibration Timing 是指各类校准在系统运行过程中的执行阶段。

Calibration 不属于正常曝光流程，而属于系统维护及图像质量保证流程。

Calibration 可发生于：

- 出厂阶段
- 维修阶段
- 系统维护阶段
- 用户主动执行阶段

完成 Calibration 后，生成的校准数据参与后续图像处理。

---

# 4. Relationship with Detector Workflow

Calibration 位于正常成像流程之外。

系统生命周期如下：

```text
Power On

↓

System Initialization

↓

Detector Ready

↓

Calibration（Required）

↓

Exposure

↓

Image Acquisition

↓

Image Processing

↓

Communication
```

Calibration 完成后，Detector 进入正常工作状态。

---

# 5. Relationship with Exposure

Calibration 与正常曝光存在区别。

Calibration：

用于建立校准数据。

Exposure：

用于获取诊断图像。

Calibration 不用于临床图像采集。

---

# 6. Timing of Different Calibration Types

不同类型 Calibration 的执行时机如下：

## Offset Calibration

执行条件：

无 X-Ray 曝光。

目的：

建立 Offset Data。

---

## Gain Calibration

执行条件：

均匀 X-Ray 曝光。

目的：

建立 Gain Data。

---

## Defect Calibration

执行条件：

依据系统要求完成异常 Pixel 检测。

目的：

建立 Defect Data。

---

# 7. Timing Relationship

理论执行顺序如下：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

前序 Calibration 结果为后续 Calibration 提供基础数据。

---

# 8. Relationship with Image Pipeline

Calibration 数据不参与曝光。

Calibration Data 在图像处理阶段参与修正。

流程如下：

```text
Exposure

↓

Image Acquisition

↓

Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Corrected Image
```

---

# 9. Calibration Data Lifecycle

Calibration Data 生命周期包括：

```text
Calibration

↓

Calibration Data Generation

↓

Calibration Data Storage

↓

Image Processing

↓

Calibration Update（When Required）
```

Calibration Data 在多次曝光过程中重复使用。

---

# 10. Image Influence

Calibration Timing 不正确可能导致：

- 使用旧 Calibration Data
- Calibration Data 与当前系统状态不一致
- 图像均匀性下降
- Fixed Pattern Noise
- Defect Compensation Failure

---

# 11. Diagnostic Significance

分析图像异常时，应确认：

- 当前 Calibration 是否完成
- Calibration Data 是否有效
- Calibration 是否与当前 Detector 匹配
- Calibration 是否需要重新执行

---

# 12. Relationship with Other Documents

Calibration Theory：

- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md

Workflow：

- CalibrationFlow.md

System：

- TimingArchitecture.md
- ImagePipeline.md

---

# 13. Knowledge Graph

```text
Power On

↓

Initialization

↓

Calibration

├────────► Offset

├────────► Gain

└────────► Defect

↓

Calibration Data

↓

Image Processing

↓

Corrected Image
```

---

# 14. Document Boundary

本文件负责：

- Calibration 执行时机
- Calibration 生命周期
- Calibration 与 Exposure 的关系
- Calibration 数据参与时机
- Calibration 顺序

本文件不负责：

- Calibration 算法
- Calibration 操作步骤
- Calibration 参数
- Calibration 文件格式

上述内容分别由对应文档说明。

---

# 15. Reference

## Fact

- 产品培训资料关于探测器校准流程及图像处理流程。
- 产品用户手册关于校准操作及设备维护要求。

## Theory

- Calibration 在系统生命周期中的执行时机。
- Calibration Data 在图像处理阶段参与图像校正。