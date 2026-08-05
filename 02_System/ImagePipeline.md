# Image Pipeline

Version: V2.0

Module: System

Source Level:
- Fact
- Theory

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- DetectorArchitecture.md
- SignalDomain.md
- TimingArchitecture.md
- Communication.md
- ../05_Calibration/OffsetCalibration.md
- ../05_Calibration/GainCalibration.md
- ../05_Calibration/DefectCalibration.md
- ../04_Software/iDetector.md

---

# 1. Purpose

Image Pipeline 定义数字平板探测器数字图像从生成到输出的完整处理架构。

本文件描述数字图像在系统内部各处理阶段之间的关系、处理顺序及模块职责。

本文件不描述图像处理算法及校准步骤。

---

# 2. Scope

适用于所有数字平板探测器产品。

包括：

- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

适用于：

- 图像生成
- 图像校准
- 图像输出
- 图像异常分析
- 故障定位

---

# 3. Core Concept

Image Pipeline 以数字图像作为输入对象。

所有图像处理均发生于 Digital Domain。

处理完成后生成可用于显示、存储及传输的图像。

---

# 4. Pipeline Overview

```

Raw Image

↓

Offset Correction

↓

Gain Correction

↓

Defect Correction

↓

Image Validation

↓

Image Buffer

↓

Image Output

↓

Communication

↓

Workstation

```

---

# 5. Pipeline Stage

| Stage | Input | Output |
|---------|-------|--------|
| Raw Image | Digital Pixel Data | Raw Image |
| Offset Correction | Raw Image | Offset Corrected Image |
| Gain Correction | Offset Corrected Image | Gain Corrected Image |
| Defect Correction | Gain Corrected Image | Corrected Image |
| Image Validation | Corrected Image | Valid Image |
| Image Buffer | Valid Image | Image Frame |
| Image Output | Image Frame | Network Image |

---

# 6. Stage Definition

## 6.1 Raw Image

### Definition

ADC 输出的原始数字图像。

### Input

Digital Pixel Data

### Output

Raw Image

### Characteristics

未经校正。

包含固定模式误差。

作为所有校准处理输入。

Reference

SignalDomain.md

---

## 6.2 Offset Correction

### Definition

执行 Offset 校正。

### Input

Raw Image

### Output

Offset Corrected Image

### Purpose

补偿系统零点偏移。

Reference

../05_Calibration/OffsetCalibration.md

---

## 6.3 Gain Correction

### Definition

执行 Gain 校正。

### Input

Offset Corrected Image

### Output

Gain Corrected Image

### Purpose

补偿像素响应差异。

提高图像一致性。

Reference

../05_Calibration/GainCalibration.md

---

## 6.4 Defect Correction

### Definition

执行 Defect 校正。

### Input

Gain Corrected Image

### Output

Corrected Image

### Purpose

修正缺陷像素。

Reference

../05_Calibration/DefectCalibration.md

---

## 6.5 Image Validation

### Definition

完成图像完整性检查。

### Input

Corrected Image

### Output

Validated Image

### Purpose

确认图像满足输出条件。

---

## 6.6 Image Buffer

### Definition

缓存完整图像。

### Input

Validated Image

### Output

Image Frame

### Purpose

等待发送。

---

## 6.7 Image Output

### Definition

输出图像数据。

### Input

Image Frame

### Output

Network Image

### Purpose

发送至工作站。

Reference

Communication.md

---

# 7. Processing Sequence

Image Pipeline 必须按照固定顺序执行。

```

Raw Image

↓

Offset

↓

Gain

↓

Defect

↓

Validation

↓

Buffer

↓

Output

```

不得调整处理顺序。

---

# 8. Relationship With Signal Domain

Image Pipeline 起始于 Signal Domain 完成数字化之后。

Signal Domain 负责：

Digital Pixel Data

Image Pipeline 负责：

Digital Image Processing

Reference

SignalDomain.md

---

# 9. Relationship With Timing

Image Processing 开始于 Readout 完成之后。

结束于图像发送之前。

Reference

TimingArchitecture.md

---

# 10. Relationship With Calibration

Calibration 为 Image Pipeline 提供校正数据。

Image Pipeline 调用：

- Offset Calibration
- Gain Calibration
- Defect Calibration

Calibration 不负责图像输出。

Reference

../05_Calibration/

---

# 11. Relationship With Communication

Image Pipeline 输出图像。

Communication 完成图像传输。

Reference

Communication.md

---

# 12. Relationship With Software

Image Pipeline 输出的数据供软件调用。

包括：

- SDK
- iDetector

软件负责：

- 图像接收
- 图像显示
- 图像保存

Reference

../04_Software/

---

# 13. Engineering Characteristics

Image Pipeline 属于数字图像处理流程。

所有处理均基于数字图像。

图像处理顺序固定。

校准数据来源于 Calibration 模块。

图像输出完成后不得再次执行校正。

---

# 14. Failure Mapping

| Pipeline Stage | Possible Failure | Related Knowledge |
|----------------|------------------|-------------------|
| Raw Image | Raw Image Abnormal | FailureKnowledge |
| Offset Correction | Offset Calibration Failure | Calibration |
| Gain Correction | Gain Calibration Failure | Calibration |
| Defect Correction | Defect Calibration Failure | Calibration |
| Image Validation | Image Integrity Failure | FailureKnowledge |
| Image Buffer | Buffer Overflow | FailureKnowledge |
| Image Output | Image Transmission Failure | Communication |

---

# 15. Knowledge Relationship

```

DetectorArchitecture

↓

SignalDomain

↓

TimingArchitecture

↓

ImagePipeline

├────────► Calibration

├────────► Communication

├────────► Software

├────────► FailureKnowledge

└────────► ImageDiagnosis

```

---

# 16. Document Boundary

本文件负责：

- 图像处理架构
- 图像处理阶段
- 图像处理关系
- 图像处理顺序

本文件不负责：

- Offset 算法
- Gain 算法
- Defect 算法
- 图像增强算法
- 图像显示
- 软件操作
- 图像诊断

---

# 17. Reference

## Fact

- Mammo1012C 用户手册：数字平板探测器图像采集及系统组成说明。:contentReference[oaicite:0]{index=0}
- Mammo1012X 用户手册：设备运行及图像输出相关说明。:contentReference[oaicite:1]{index=1}

## Theory

- 数字 X 射线探测器培训资料：Raw Image、Offset Correction、Gain Correction、Defect Correction、数字图像生成流程。