# ImageDistortion

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- ImageArtifact.md
- UniformityFailure.md
- ImageLoss.md
- ../HardwareFailure/FPGAFailure.md
- ../HardwareFailure/ReadoutASICFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../SoftwareFailure/FirmwareFailure.md
- ../../06_Workflow/ImageGenerationWorkflow.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Image Distortion 描述数字平板探测器（Flat Panel Detector，FPD）图像几何失真（Image Distortion）的典型表现、形成机理、故障来源、检测方法及根因分析。

Image Distortion 是指图像的几何结构、比例关系或像素排列发生异常，使实际物体不能按照真实尺寸、真实位置进行显示。

与 Noise、Ghost 等灰度异常不同，Image Distortion 属于**几何结构异常（Geometric Image Failure）**。

本文件回答的问题：

> **为什么图像发生拉伸、压缩、错位、重复或变形？如何快速定位图像畸变的根因？**

---

# 2. Scope

适用于：

- Factory Test
- Engineering Debug
- Technical Support
- Field Service

适用于：

- Geometric Distortion
- Image Stretch
- Image Compression
- Image Shift
- Image Rotation
- Image Duplication
- Pixel Mapping Error

---

# 3. What is Image Distortion

Image Distortion 指：

**由于图像数据读出、重建、映射或传输异常，导致图像几何关系发生改变。**

主要特点：

- 图像比例异常
- 图像位置异常
- 图像重复
- 图像断裂
- 图像错位
- 图像旋转
- 图像镜像

---

# 4. Classification

```text
Image Distortion

├── Image Stretch
├── Image Compression
├── Image Shift
├── Image Rotation
├── Image Mirror
├── Image Duplication
├── Block Misalignment
├── Pixel Mapping Error
└── Frame Misalignment
```

---

# 5. Image Characteristics

## 5.1 Image Stretch

特点：

- 图像沿 X 或 Y 方向拉长
- 比例失真

可能原因：

- Pixel Mapping Error
- FPGA Processing Error

---

## 5.2 Image Compression

特点：

- 图像压缩
- 比例缩小

可能原因：

- Timing Error
- Incorrect Pixel Count

---

## 5.3 Image Shift

特点：

- 图像整体偏移
- 左右或上下移动

可能原因：

- Frame Synchronization Error
- FPGA Address Offset

---

## 5.4 Image Rotation

特点：

- 图像旋转 90°、180° 或 270°

可能原因：

- Firmware Configuration Error
- Image Processing Error

---

## 5.5 Image Mirror

特点：

- 左右镜像
- 上下翻转

可能原因：

- Firmware Parameter Error
- Software Configuration Error

---

## 5.6 Image Duplication

特点：

- 图像局部重复
- 图像内容复制

可能原因：

- DDR Memory Error
- FPGA Frame Buffer Error

---

## 5.7 Block Misalignment

特点：

- 图像分块错位
- 块与块之间存在偏移

可能原因：

- Readout ASIC Error
- FPGA Block Reconstruction Error

---

## 5.8 Pixel Mapping Error

特点：

- Pixel 排列错误
- 图像出现锯齿或规则错位

可能原因：

- Pixel Address Error
- Mapping Table Error

---

## 5.9 Frame Misalignment

特点：

- 连续图像位置变化
- Frame 对齐失败

可能原因：

- Frame Synchronization Error
- Communication Timing Error

---

# 6. Typical Root Causes

| Distortion Type | Possible Root Cause |
|-----------------|---------------------|
| Stretch | FPGA |
| Compression | Timing Error |
| Shift | Frame Address Error |
| Rotation | Firmware Configuration |
| Mirror | Software Configuration |
| Duplication | DDR Memory |
| Block Misalignment | Readout ASIC |
| Pixel Mapping Error | FPGA Mapping |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| FPGA | Image Distortion |
| Readout ASIC | Block Misalignment |
| DDR Memory | Image Duplication |
| Main Board | Data Synchronization Error |
| Communication Interface | Frame Shift |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Rotation / Mirror |
| SDK | Pixel Mapping Error |
| Configuration | Wrong Display Orientation |
| Image Processing | Reconstruction Error |

---

# 9. Relationship with Workflow

Image Distortion 主要发生于：

```text
Readout

↓

FPGA Processing

↓

Image Reconstruction

↓

Image Generation

↓

Image Transmission
```

因此重点关联：

- ReadoutWorkflow
- ImageGenerationWorkflow
- ImageTransmissionWorkflow

---

# 10. Diagnostic Workflow

```text
Image Distorted

↓

Whole Image？

↓

YES

↓

Stretch？

↓

FPGA

↓

Compression？

↓

Timing

↓

Rotation？

↓

Firmware

↓

Mirror？

↓

Configuration

↓

Partial？

↓

Block Misalignment

↓

ASIC

↓

Repeated？

↓

DDR Memory

↓

Pixel Disorder？

↓

FPGA Mapping
```

---

# 11. Detection Methods

## Geometric Phantom Test

使用标准几何 Phantom：

检查：

- 长宽比例
- 几何尺寸
- 图像中心位置

---

## Grid Test

观察：

- 网格是否弯曲
- 网格是否错位
- 网格间距是否一致

---

## Multi-frame Test

连续采集：

观察：

- 是否存在 Frame Shift
- 是否存在 Block Misalignment

---

## Firmware Verification

检查：

- Rotation Parameter
- Mirror Parameter
- Pixel Mapping Configuration

---

## FPGA Verification

检查：

- Pixel Mapping
- Address Generator
- Frame Buffer
- DDR Memory

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Whole Image Stretched | FPGA Pixel Mapping Error |
| Whole Image Shifted | Address Offset |
| Rotated Image | Firmware Configuration Error |
| Mirror Image | Wrong Display Configuration |
| Repeated Block | DDR Memory Error |
| Image Split into Blocks | Readout ASIC Failure |

---

# 13. Engineering Recommendations

建议：

- 首先确认是否属于几何异常，而非灰度异常。
- 使用标准 Phantom 验证图像比例。
- 检查 Firmware 配置是否正确。
- 验证 FPGA Pixel Mapping 是否正常。
- 检查 DDR Memory 与 Readout ASIC 是否存在异常。
- 使用 DecisionTree 完成最终定位。

---

# 14. Relationship with Other Modules

## FPGAFailure

Image Distortion 最主要的硬件来源。

---

## ReadoutASICFailure

负责 Block Misalignment 等局部畸变。

---

## FirmwareFailure

负责 Rotation、Mirror 等软件配置异常。

---

## ImageGenerationWorkflow

Image Distortion 多发生于图像生成阶段。

---

## DecisionTree

Image Distortion 是图像几何异常的重要诊断入口。

---

# 15. Knowledge Graph

```text
Image Distortion

├── Stretch
├── Compression
├── Shift
├── Rotation
├── Mirror
├── Duplication
├── Block Misalignment
├── Pixel Mapping Error
└── Frame Misalignment

↓

Image Reconstruction

↓

Hardware Analysis

├── FPGA
├── ASIC
├── DDR Memory
├── Main Board
└── Communication

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Image Distortion 是 Flat Panel Detector 图像处理过程中典型的几何异常，主要表现为图像拉伸、压缩、偏移、旋转、镜像、重复、分块错位及 Pixel Mapping 错误。其根因通常涉及 FPGA 图像重建、Readout ASIC 数据读出、DDR Memory 缓存、Firmware 配置及通信同步等模块。通过几何 Phantom 测试、Grid 测试、多帧验证及 FPGA/Firmware 检查，可快速定位图像畸变来源，并结合 Workflow、HardwareFailure 与 DecisionTree 建立标准化故障分析流程。