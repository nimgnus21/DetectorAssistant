# GainFAQ

Version: V2.0

Module: Calibration

Source Level:
- Engineering
- FAQ

Applicable Product:
- Pluto Series
- Mercu Series
- Jupi Series
- Mammo Series

Related Documents:
- GainWorkflow.md
- GainParameter.md
- GainFailure.md
- GainTroubleshooting.md
- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Gain FAQ 汇总 Gain Calibration 过程中最常见的问题，并提供统一的技术解释。

本文件用于帮助现场工程师、售后工程师及技术支持人员快速理解 Gain Calibration 的目的、执行条件及常见故障。

本文件不替代 Workflow、Troubleshooting 或 SOP。

---

# 2. Frequently Asked Questions

---

## Q1：为什么需要执行 Gain Calibration？

### Answer

Gain Calibration 用于建立 Detector 的 Gain Data。

Gain Data 用于补偿各 Pixel 之间的响应差异，提高图像整体均匀性，减少由于 Pixel Sensitivity 不一致导致的图像亮度差异。

---

## Q2：Gain Calibration 必须在 Offset Calibration 之后执行吗？

### Answer

必须。

Gain Calibration 依赖 Offset Calibration 生成的 Offset Data。

标准 Calibration 顺序为：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

---

## Q3：为什么 Gain Calibration 必须进行均匀曝光？

### Answer

Gain Calibration 需要采集 Flat Field Image。

Flat Field Image 应满足：

- X-Ray 覆盖整个 Detector
- Beam 分布均匀
- 曝光稳定
- 图像完整

只有在均匀曝光条件下，才能正确计算各 Pixel 的 Gain。

---

## Q4：Gain Calibration 可以在没有 X-Ray 的情况下执行吗？

### Answer

不可以。

Gain Calibration 必须使用均匀 X-Ray 曝光。

无曝光条件下无法获得 Flat Field Image，也无法建立 Gain Data。

---

## Q5：Gain Calibration 完成后为什么图像仍然不均匀？

### Answer

可能原因包括：

- Flat Field Image 不均匀
- Gain Data 未正确更新
- Calibration Data 未正确加载
- Offset Calibration 数据异常
- Detector 硬件异常

应结合 GainTroubleshooting.md 进一步分析。

---

## Q6：Gain Calibration 是否会修改 Detector 硬件参数？

### Answer

不会。

Gain Calibration 仅生成新的 Gain Data，并更新 Calibration Data。

不会修改 Detector 的硬件配置或电路参数。

---

## Q7：Gain Calibration 会影响临床图像吗？

### Answer

会。

Gain Data 会参与后续所有图像处理。

若 Gain Data 异常，可能导致：

- 图像均匀性下降
- Bright Area
- Dark Area
- Image Artifact

---

## Q8：Gain Calibration 成功是否表示 Detector 正常？

### Answer

不一定。

Gain Calibration 成功仅表示 Gain Calibration 流程完成。

仍需结合：

- Offset Calibration
- Defect Calibration
- 测试图像
- Detector Self Test

综合判断 Detector 工作状态。

---

## Q9：Gain Calibration 为什么会失败？

### Answer

常见原因包括：

- Detector 未 Ready
- Offset Calibration 未完成
- 通信异常
- 曝光条件异常
- Flat Field Image 采集失败
- Gain Calculation 异常
- Calibration Data 更新失败

---

## Q10：重复执行 Gain Calibration，结果为什么会不同？

### Answer

轻微差异属于正常现象。

若差异较大，应检查：

- X-Ray 输出稳定性
- 曝光参数一致性
- Beam 均匀性
- Detector 温度
- Detector 工作状态

---

## Q11：Gain Calibration 会修复 Bad Pixel 吗？

### Answer

不会。

Gain Calibration 用于补偿 Pixel Response 差异。

Bad Pixel 的识别与补偿由 Defect Calibration 完成。

---

## Q12：Gain Calibration 是否可以单独执行？

### Answer

可以。

但应确保 Offset Calibration 已完成。

若需要完成完整 Calibration，建议按照：

```text
Offset

↓

Gain

↓

Defect
```

依次执行。

---

## Q13：Gain Calibration 是否需要定期执行？

### Answer

根据产品维护规范执行。

通常在以下情况建议重新 Calibration：

- Detector 更换
- Detector 维修
- Firmware 升级（依据产品要求）
- Calibration Data 更新
- 图像均匀性下降
- 系统维护要求

---

## Q14：Gain Calibration 的最终输出是什么？

### Answer

完成 Calibration 后生成：

- Gain Data
- Gain Table
- Calibration Data Update

上述数据用于图像处理阶段的 Gain Correction。

---

## Q15：Gain Calibration 与 Image Uniformity 有什么关系？

### Answer

Gain Calibration 的主要目标就是提高图像均匀性。

Gain Data 用于补偿不同 Pixel 的响应差异，使 Detector 输出更加一致。

若 Gain Data 异常，图像可能出现局部亮区、暗区或整体均匀性下降。

---

# 3. Quick Troubleshooting Guide

| Symptom | Recommended Check |
|----------|-------------------|
| Gain Calibration Failed | Detector、Communication、Offset Status |
| Calibration Timeout | Network、Detector Status |
| Flat Field Image Error | Exposure、Beam Uniformity |
| Bright/Dark Area | Gain Data、Calibration Data |
| Image Nonuniformity | Exposure、Gain Data、Detector Status |
| Calibration Success but Image Abnormal | Offset、Gain、Defect、Image Diagnosis |

---

# 4. Related Documents

Calibration：

- GainWorkflow.md
- GainParameter.md
- GainFailure.md
- GainTroubleshooting.md

Theory：

- ../CalibrationTheory/GainTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 5. Document Boundary

本文件负责：

- Gain Calibration 常见问题
- 标准技术解释
- 快速故障查询
- FAQ 索引

本文件不负责：

- Calibration 操作流程
- 参数配置
- 故障详细分析
- SOP
- SDK API

详细内容分别由对应文档说明。

---

# 6. Summary

Gain FAQ 为现场工程师提供 Gain Calibration 的快速参考。

遇到复杂问题时，应结合：

- GainTroubleshooting.md
- FailureKnowledge
- DecisionTree
- SOP

进行进一步分析与处理。