# DTDITool

Version: V1.0

Module: 17_Tools / SDKTool

Status: Draft

Applicable Products:

- Pluto0900X Dynamic Detector
- Pluto Dynamic Series
- Dynamic Flat Panel Detector

Related Documents:

- README.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../06_Workflow/DynamicCorrectionWorkflow.md
- ../../06_Workflow/ImageGenerationWorkflow.md

---

# 1. Purpose

DTDITool（Dynamic TDI Tool）是 SDK 配套提供的动态图像离线处理工具，用于将动态探测器采集得到的连续 RAW 数据按照扫描方式重新排列、拼接，并结合 Defect Template 对图像进行坏点、坏线修正，最终生成完整图像。

DTDITool 主要用于以下场景：

- 动态平板图像拼接
- TDI 数据重建
- 图像质量分析
- Defect Template 验证
- 校准结果验证
- FAE 现场问题分析
- 研发算法验证

> **说明**
>
> DTDITool 不负责图像采集，仅对已采集完成的 RAW 数据进行离线处理。

---

# 2. Working Principle

动态平板通常采用连续采集方式，每一帧仅包含完整图像的一部分。

DTDITool 根据 Detector 的扫描方式，将连续帧重新排列并拼接。

处理流程如下：

```text
Detector

↓

Continuous RAW

↓

Frame Alignment

↓

Row Mapping

↓

Image Stitching

↓

Defect Correction

↓

Output RAW
```

工具内部主要完成：

- Frame 顺序计算
- 行位置映射
- 图像拼接
- Defect 修正
- RAW 输出

---

# 3. Supported File Formats

## Input

支持：

```text
*.raw
```

要求：

- 连续采集数据
- RAW 文件完整
- Frame 数正确
- 无明显丢帧

若 RAW 数据不完整，可能出现：

- 图像断裂
- 拼接失败
- 图像缺失
- Output 高度错误

---

## Output

输出格式：

```text
*.raw
```

建议始终保存为 RAW。

生成后的 RAW 可直接用于：

- SDK Viewer
- ImageJ
- Offset Viewer
- 图像分析软件

---

# 4. Interface Overview

DTDITool 主要参数如下：

| Parameter | Description |
|------------|-------------|
| Input Path | 输入 RAW 文件 |
| Output Path | 输出 RAW 文件 |
| Width | 输入图像宽度 |
| Height | 单帧高度 |
| Total Frames | 总帧数 |
| Output Width | 输出宽度 |
| Output Height | 输出高度 |
| Row Begin | 起始行 |
| Row End | 结束行 |
| Step Lines | 拼接步长 |
| Skip Frames | 跳过帧数 |
| Scan Direction | 扫描方向 |
| Defect Template Path | Defect 模板路径 |
| Convert | 开始拼接 |

---

# 5. Parameter Description

## 5.1 Input Path

待处理 RAW 数据。

要求：

- RAW 文件完整
- Frame 数正确
- ROI 与采集一致

---

## 5.2 Output Path

输出 RAW 保存位置。

建议：

文件扩展名保持：

```text
.raw
```

推荐命名：

```text
Detector_Model_ROI_Date_Output.raw
```

例如：

```text
Pluto0900X_2252x1260_Output.raw
```

---

## 5.3 Width

输入 RAW 每帧宽度。

单位：

```text
Pixel
```

必须与采集参数一致。

错误将导致：

- 图像错位
- 拼接失败

---

## 5.4 Height

输入 RAW 每帧高度。

例如：

```text
68
```

表示：

每帧仅包含 68 行数据。

---

## 5.5 Total Frames

RAW 总帧数。

例如：

```text
600
```

Frame 数不足：

可能导致：

- 图像缺失
- 输出高度异常
- 拼接失败

---

## 5.6 Output Width

通常保持与输入 Width 一致。

例如：

```text
2252
```

---

## 5.7 Output Height

最终拼接后的图像高度。

例如：

```text
1260
```

该值由：

- Height
- Step Lines
- Frame 数

共同决定。

---

## 5.8 Row Begin

拼接起始行。

### 工程推荐（Pluto0900X）

```text
Row Begin = 5
```

除特殊要求外，不建议修改。

---

## 5.9 Row End

拼接结束行。

一般根据 Height 自动确定。

---

## 5.10 Step Lines

每帧移动行数。

### 工程推荐

```text
Step Lines = 2
```

修改错误可能导致：

- 图像重叠
- 图像拉伸
- 图像错位
- 图像高度异常

---

## 5.11 Skip Frames

跳过前几帧。

默认：

```text
0
```

仅调试特殊情况使用。

---

## 5.12 Scan Direction

扫描方向：

- Left
- Right

必须与 Detector 实际扫描方向一致。

否则：

- 图像左右镜像
- 拼接方向错误
- 图像无法正确重建

---

## 5.13 Defect Template Path

Defect 模板文件。

作用：

- 坏点修正
- 坏线修正
- 双列坏线补偿

建议：

选择对应：

- Detector
- ROI
- PGA
- Calibration

生成的模板。

错误模板可能造成：

- 新坏点
- 换线异常
- 图像伪影

---

# 6. Standard Workflow

## Step 1

打开 DTDITool。

---

## Step 2

选择 Input RAW。

---

## Step 3

设置 Output Path。

建议：

保存为：

```text
*.raw
```

---

## Step 4

确认 Width。

确认与采集参数一致。

---

## Step 5

确认 Height。

例如：

```text
68
```

---

## Step 6

确认 Total Frames。

确保采集完整。

---

## Step 7

设置工程参数：

```text
Row Begin = 5

Step Lines = 2

Skip Frames = 0
```

---

## Step 8

加载 Defect Template。

选择对应 Detector 的 defect 模板。

---

## Step 9

点击：

```text
Convert
```

开始拼接。

---

## Step 10

输出 RAW。

使用 ImageJ、SDK Viewer 或其它工具验证拼接结果。
---

# 7. Engineering Experience

本章节记录 FAE 现场及研发培训过程中积累的工程经验，作为标准流程的补充。

> **说明**
>
> 以下内容主要来源于现场使用经验，仅适用于对应平台或 SDK 版本。如后续 SDK 版本更新，请以最新版本为准。

---

## 7.1 Pluto0900X 推荐参数

目前 Pluto0900X 平台推荐参数如下：

| Parameter | Recommended Value |
|------------|------------------|
| Row Begin | 5 |
| Step Lines | 2 |
| Skip Frames | 0 |

除研发特殊要求外，建议保持以上默认值。

---

## 7.2 Defect Template 选择原则

DTDITool 拼接过程中应选择与当前 Detector 完全匹配的 Defect Template。

建议确认：

- Detector SN
- Detector Model
- ROI
- PGA
- Binning
- Calibration Version

避免使用其它探测器生成的 Defect Template。

否则可能出现：

- 坏点增加
- 换线异常
- 图像伪影
- 局部亮度异常

---

## 7.3 Output 文件建议

建议输出：

```text
*.raw
```

不要转换为 BMP、PNG、JPEG 等格式。

RAW 保留原始灰度数据，方便后续：

- ImageJ
- SDK Viewer
- 图像算法分析
- Defect 分析
- 校准验证

---

## 7.4 图像尺寸验证

完成拼接后建议确认：

- Output Width
- Output Height
- 图像比例
- 是否存在拉伸
- 是否存在重叠
- 是否存在黑边

若尺寸异常，应优先检查：

- Width
- Height
- Step Lines
- Total Frames

---

## 7.5 拼接完成后的检查项目

建议确认：

□ 图像完整

□ 无明显断层

□ 无明显重复区域

□ 无明显重叠

□ 无明显拉伸

□ 无明显黑边

□ 无明显换线

□ 无新增坏点

---

# 8. Common Problems

## 8.1 Convert Failed

现象：

点击 Convert 后处理失败。

可能原因：

- Input RAW 不完整
- Output 路径不存在
- 文件被占用
- 参数错误

建议：

重新确认：

- RAW 文件
- 输出目录
- Width
- Height

---

## 8.2 Image Misalignment

现象：

图像上下错位。

可能原因：

- Row Begin 设置错误
- Step Lines 设置错误
- Frame 顺序错误

建议：

恢复推荐参数：

```text
Row Begin = 5

Step Lines = 2
```

---

## 8.3 Image Stretch

现象：

图像高度异常。

可能原因：

- Output Height 错误
- Height 设置错误
- Step Lines 错误

---

## 8.4 Image Overlap

现象：

图像重复。

可能原因：

- Step Lines 设置过小
- Total Frames 设置错误

---

## 8.5 Missing Area

现象：

图像缺失。

可能原因：

- RAW 数据采集不完整
- Skip Frames 设置错误
- Frame 丢失

---

## 8.6 Defect Still Exists

现象：

拼接后坏点仍存在。

可能原因：

- Defect Template 不匹配
- 使用旧模板
- Template 未加载

建议：

重新加载正确模板。

---

# 9. Troubleshooting

建议按照以下顺序排查：

```text
RAW 文件

↓

Width

↓

Height

↓

Frame 数

↓

Row Begin

↓

Step Lines

↓

Scan Direction

↓

Defect Template

↓

Output RAW

↓

重新拼接
```

通常可以解决绝大多数 DTDITool 使用问题。

---

# 10. FAQ

## Q1：为什么推荐 Row Begin = 5？

A：

根据当前 Pluto0900X 平台的工程实践，该参数能够正确对应当前扫描方式。若研发未特别说明，不建议修改。

---

## Q2：为什么 Step Lines 推荐为 2？

A：

Step Lines 决定每帧拼接移动的行数。

设置错误容易导致：

- 图像重叠
- 图像断层
- 图像拉伸

---

## Q3：为什么必须选择正确的 Defect Template？

A：

Defect Template 与 Detector 校准结果绑定。

若使用不同：

- Detector
- ROI
- PGA
- Binning

生成的模板，容易产生新的图像异常。

---

## Q4：Output 为什么建议保存 RAW？

A：

RAW 保留完整原始数据，便于：

- ImageJ 分析
- SDK Viewer 查看
- 图像算法验证
- 后续校准分析

---

## Q5：拼接完成后最先检查什么？

建议依次确认：

1. 图像尺寸是否正确。
2. 图像是否完整。
3. 是否存在重叠或断层。
4. Defect 是否正常修正。
5. 是否存在明显新增伪影。

---

# 11. References

参考资料：

- Detector SDK User Manual
- Detector Calibration Workflow
- Dynamic Acquisition Workflow
- 内部研发培训资料
- FAE 工程经验总结

---

# 12. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 DTDITool 使用说明，包含参数说明、标准流程、工程经验及常见问题。 |

---

## FrameNo Verification

### Purpose

Verify whether image frames are received sequentially during continuous acquisition.

### Check Items

- FrameNo increases continuously.
- No duplicated FrameNo.
- No skipped FrameNo.
- Callback execution is stable.
- Image buffer is released correctly.

### Typical Symptoms

- Frozen image
- Missing frames
- Frame synchronization errors
- Continuous acquisition instability

### Recommendation

If FrameNo is abnormal while detector communication remains normal, compare the application behavior with the official SDK demo to determine whether the issue originates from the application layer.