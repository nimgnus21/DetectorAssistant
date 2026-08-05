# CalibrationFlow

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
- CalibrationTiming.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md
- CalibrationData.md
- ../../02_System/ImagePipeline.md
- ../../02_System/TimingArchitecture.md

---

# 1. Purpose

Calibration Flow 描述数字平板探测器校准的完整执行流程，以及各类 Calibration 之间的逻辑关系。

Calibration Flow 用于说明：

- Calibration 的整体执行顺序
- Calibration 数据的生成过程
- Calibration 数据在图像处理中的使用方式
- 各类 Calibration 之间的依赖关系

本文件不涉及具体校准算法及软件操作。

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

Calibration Flow 是指探测器完成图像校准所经历的完整流程。

整个流程包括：

- Offset Calibration
- Gain Calibration
- Defect Calibration

完成 Calibration 后，生成 Calibration Data，并参与后续图像处理。

---

# 4. Overall Workflow

Calibration 的总体流程如下：

```text
Detector Ready

↓

Offset Calibration

↓

Gain Calibration

↓

Defect Calibration

↓

Calibration Data Generation

↓

Calibration Data Storage

↓

Image Processing

↓

Corrected Image
```

---

# 5. Offset Calibration Stage

目的：

建立 Offset Data。

输入：

Dark Image。

输出：

Offset Table。

作用：

消除 Pixel 固定偏移。

Reference：

- OffsetTheory.md

---

# 6. Gain Calibration Stage

目的：

建立 Gain Data。

输入：

Uniform Exposure Image。

输出：

Gain Table。

作用：

提高 Pixel Response 一致性。

Reference：

- GainTheory.md

---

# 7. Defect Calibration Stage

目的：

识别异常 Pixel。

输入：

Calibration Image。

输出：

Defect Map。

作用：

补偿异常 Pixel。

Reference：

- DefectTheory.md

---

# 8. Calibration Data Generation

完成三类 Calibration 后，系统生成 Calibration Data。

Calibration Data 包括：

- Offset Data
- Gain Data
- Defect Data

Calibration Data 用于后续图像校正。

Reference：

- CalibrationData.md

---

# 9. Relationship with Image Processing

Calibration 不直接生成诊断图像。

Calibration Data 在图像处理阶段参与校正。

流程如下：

```text
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

Calibration Data 在整个图像处理过程中持续发挥作用。

Reference：

- ../../02_System/ImagePipeline.md

---

# 10. Calibration Dependency

各 Calibration 存在先后依赖关系。

```text
Offset

↓

Gain

↓

Defect
```

其中：

- Gain Calibration 建立在 Offset Correction 基础上。
- Defect Calibration 建立在 Offset 与 Gain Calibration 完成之后。

---

# 11. Calibration Update

Calibration Data 并非永久有效。

以下情况可能需要重新执行 Calibration：

- Detector 维修
- Hardware 更换
- Calibration 数据异常
- 图像质量异常
- 系统维护要求

具体执行条件以产品维护规范为准。

---

# 12. Failure Influence

Calibration Flow 中任一环节异常均可能影响后续图像质量。

例如：

- Offset Calibration Failure
- Gain Calibration Failure
- Defect Calibration Failure
- Calibration Data Error

可能导致：

- 图像背景异常
- 图像均匀性下降
- Bad Pixel 未补偿
- 图像伪影

---

# 13. Relationship with Other Documents

Theory：

- CalibrationOverview.md
- PixelResponse.md
- OffsetTheory.md
- GainTheory.md
- DefectTheory.md
- CalibrationTiming.md

Data：

- CalibrationData.md

System：

- ../../02_System/ImagePipeline.md
- ../../02_System/TimingArchitecture.md

---

# 14. Knowledge Graph

```text
Detector Ready

↓

Offset Calibration

↓

Offset Data

↓

Gain Calibration

↓

Gain Data

↓

Defect Calibration

↓

Defect Data

↓

Calibration Data

↓

Image Processing

↓

Corrected Image
```

---

# 15. Document Boundary

本文件负责：

- Calibration 总流程
- 三类 Calibration 顺序
- Calibration Data 生成流程
- Calibration 与图像处理关系
- Calibration 生命周期

本文件不负责：

- Offset Calibration 操作
- Gain Calibration 操作
- Defect Calibration 操作
- Calibration 参数配置
- Calibration 文件格式

上述内容由对应文档说明。

---

# 16. Reference

## Fact

- 产品培训资料关于探测器 Calibration 流程及图像处理流程。
- 产品用户手册关于 Calibration 操作流程。

## Theory

- Calibration Flow 是 Offset、Gain、Defect 三类 Calibration 的整体执行框架。
- Calibration Data 在图像处理阶段参与图像校正。