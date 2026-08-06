# CalibrationTools

Version: V1.0

Module: 17_Tools / SDKTool

Status: Draft

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Pluto Series Detector
- SDK_AIO Platform

Related Documents:

- README.md
- DTDITool.md
- ModeConfiguration.md
- FirmwareUpgrade.md
- ../../06_Workflow/CalibrationWorkflow.md
- ../../06_Workflow/DynamicCorrectionWorkflow.md
- ../../06_Workflow/ConfigurationWorkflow.md
- ../../07_FailureKnowledge/CalibrationFailure/README.md

---

# 1. Purpose

Calibration Tools 用于完成探测器校准（Calibration）相关工作，包括 Offset、Gain、Defect 及动态校准模板的生成、验证、更新和管理。

Calibration 是保证图像质量的重要步骤，其目标包括：

- 消除暗电流影响
- 消除像素响应差异
- 修正坏点、坏线
- 提高图像均匀性
- 降低动态图像残影（Ghost）
- 降低动态残留（Lag）

Calibration Tool 通常由 SDK 提供，与 Detector、Firmware 及 Mode 配合使用。

---

# 2. Calibration Overview

探测器校准通常包括以下几类：

```text
Calibration

├── Offset Calibration
├── Gain Calibration
├── Defect Calibration
├── Dynamic Calibration
│      ├── Ghost
│      ├── Lag
│      └── Swap
└── Calibration Verification
```

各模板共同参与最终图像生成。

---

# 3. Offset Calibration

## Purpose

Offset Calibration 用于消除探测器暗电流及电子零点偏移。

生成：

```text
Offset Template
```

处理流程：

```text
Dark Image

↓

Offset Calculation

↓

Offset Template

↓

Save
```

Offset Template 在采图时参与实时校正。

---

## 使用条件

通常要求：

- 无 X-Ray
- 环境稳定
- Detector 温度稳定

---

## 应用

Offset Template 用于：

- Static Detector
- Dynamic Detector
- Continuous Acquisition

---

# 4. Gain Calibration

## Purpose

Gain Calibration 用于补偿 Pixel Sensitivity 差异。

生成：

```text
Gain Template
```

流程：

```text
Flat Field Image

↓

Gain Calculation

↓

Gain Template
```

最终：

使整幅图像亮度均匀。

---

## Flat Field 要求

要求：

- 曝光均匀
- 无遮挡
- 剂量稳定

否则：

Gain Template 将失效。

---

# 5. Defect Calibration

## Purpose

Defect Calibration 用于生成：

```text
Defect Template
```

主要包括：

- Bad Pixel
- Bad Line
- Cluster Defect

处理流程：

```text
Acquire Image

↓

Detect Defect

↓

Generate Template

↓

Save
```

---

## 手动维护

若发现：

- 新坏点
- 换线

可通过工具：

手动添加：

- Pixel
- Line

重新生成 Defect Template。

---

# 6. Dynamic Calibration

动态图除基础校准外，还包括：

- Ghost Correction
- Lag Correction
- Swap Calibration

主要用于：

- Dynamic Detector
- Fluoroscopy
- DSA

---

## Ghost

来源：

Scintillator Afterglow。

---

## Lag

来源：

Detector Electronics。

---

## Swap

利用：

- Pre Offset
- Post Offset

降低动态图残影。

---

# 7. Calibration Workflow

标准流程：

```text
Detector Ready

↓

Generate Offset

↓

Generate Gain

↓

Generate Defect

↓

Verify Templates

↓

Load Templates

↓

Acquire Test Image

↓

Calibration Complete
```

---

# 8. Template Management

Calibration Template 应统一管理。

建议记录：

- Detector SN
- Firmware Version
- ROI
- PGA
- Binning
- Calibration Date
- Operator

模板命名建议：

```text
SN_ROI_PGA_Gain.dat

SN_ROI_PGA_Offset.dat

SN_ROI_PGA_Defect.dat
```

---

# 9. Engineering Experience

## 9.1 Pluto0900X 校准注意事项

### 现场经验

进行彩图校正时：

SDK 在采集过程中：

当第三组彩图采集到：

```text
63
```

时：

**不要停止曝光。**

必须继续保持曝光。

直到：

SDK 自动完成：

```text
64
```

张图像采集。

之后：

再结束曝光。

---

### 原因（依据现场培训）

SDK 在第 63 张之后会执行一次内部校验/处理流程。

若提前停止曝光：

可能导致：

- Calibration Failure
- Template Generation Failed
- 校准数据不完整

> **说明**
>
> 当前经验适用于 **Pluto0900X SDK**。其它平台是否具有相同行为，应以对应 SDK 文档或研发说明为准。

---

## 9.2 多 Mode 共用 Template

满足以下条件：

- ROI 相同
- PGA 相同
- Binning 相同

可以共用：

- Gain Template
- Defect Template

无需重复生成。

---

## 9.3 Offset 更新

动态采集过程中：

建议：

及时更新 Offset。

避免：

- Brightness Drift
- Residual Offset

---

## 9.4 Template 备份

建议：

每次重新校准后：

备份：

- Offset
- Gain
- Defect

避免：

重新校准失败造成数据丢失。

---

# 10. Common Problems

## Offset Generation Failed

检查：

- Detector 状态
- 环境光
- 曝光状态

---

## Gain Failed

检查：

- Flat Field
- X-Ray 剂量
- ROI

---

## Defect Failed

检查：

- 图像质量
- Detector 状态

---

## Calibration Failed

检查：

- Firmware Version
- SDK Version
- ROI
- PGA
- Template

---

## Ghost Still Exists

检查：

- Swap 是否开启
- Dynamic Calibration 是否正常

---

# 11. Troubleshooting

建议排查顺序：

```text
Detector

↓

Firmware

↓

SDK

↓

ROI

↓

PGA

↓

Offset

↓

Gain

↓

Defect

↓

Dynamic Calibration

↓

Acquire Image
```

---

# 12. Best Practices

建议：

- 校准前确认 Firmware 正确
- 校准前确认 ROI 正确
- 保证 Flat Field 均匀
- 定期备份 Calibration Template
- 修改 Mode 后重新验证 Calibration
- 动态平台按照对应 SDK 要求完成完整校准流程

---

# 13. FAQ

## Q1：什么时候需要重新校准？

建议情况：

- Firmware 升级
- 更换 Detector
- 修改 ROI
- 修改 PGA
- 更换 X-Ray 系统
- 图像明显异常

---

## Q2：哪些 Template 可以共用？

满足以下条件：

- ROI 相同
- PGA 相同
- Binning 相同

通常可以共用：

- Gain
- Defect

---

## Q3：为什么 Pluto0900X 要采到第 64 张？

根据现场培训：

SDK 在第 63 张后执行内部处理。

因此：

不要在第 63 张停止曝光。

应等待：

第 64 张采集完成。

---

## Q4：Offset 是否需要定期更新？

建议：

动态系统：

应根据实际工作模式及时更新 Offset。

静态系统：

一般按照维护计划更新即可。

---

# 14. References

- SDK Calibration Guide
- Calibration Workflow
- Dynamic Detector Training Materials
- FAE Engineering Experience
- Internal Development Training

---

# 15. Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| V1.0 | 2026-08 | Initial Release | 建立 Calibration Tools 文档，整理 Offset、Gain、Defect、Dynamic Calibration 及现场工程经验。 |