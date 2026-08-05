# OffsetFAQ

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
- OffsetWorkflow.md
- OffsetParameter.md
- OffsetFailure.md
- OffsetTroubleshooting.md
- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Offset FAQ 汇总现场工程师、售后工程师及技术支持人员在执行 Offset Calibration 过程中最常遇到的问题，并提供统一、标准的技术解答。

本文件作为 Offset Calibration 的快速查询文档，不替代 Workflow、Troubleshooting 或 SOP。

---

# 2. Frequently Asked Questions

---

## Q1：为什么需要进行 Offset Calibration？

### Answer

Offset Calibration 用于建立 Detector 在无 X-Ray 条件下的暗场响应（Offset Data）。

Offset Data 用于消除每个 Pixel 固有的固定偏移，提高图像背景一致性，并为 Gain Calibration 和 Defect Calibration 提供基础数据。

---

## Q2：什么时候需要重新执行 Offset Calibration？

### Answer

建议在以下情况重新执行：

- 首次安装 Detector
- 更换 Detector
- 更换 FPGA、Readout ASIC 等关键硬件
- Detector 长时间停用后重新启用
- Firmware 升级后（依据产品要求）
- Calibration Data 损坏
- 图像出现固定背景异常
- Gain Calibration 或 Defect Calibration 前（依据产品流程）

---

## Q3：Offset Calibration 必须在无曝光条件下执行吗？

### Answer

必须。

Offset Calibration 采集的是 Dark Image。

执行过程中不得进行 X-Ray 曝光，也应避免杂散射线进入 Detector。

否则生成的 Offset Data 将失效。

---

## Q4：Offset Calibration 失败后可以直接重新执行吗？

### Answer

不建议。

应首先确认失败原因，包括：

- Detector 状态
- 网络通信
- Dark Image 是否正常采集
- Calibration Data 是否正常保存

确认故障原因后再重新执行 Calibration。

---

## Q5：Offset Calibration 会影响临床图像吗？

### Answer

会。

Offset Calibration 生成的新 Offset Data 会参与后续所有图像处理。

若 Offset Data 异常，可能导致：

- 图像背景异常
- Fixed Pattern Noise
- 图像整体偏亮
- 图像整体偏暗

---

## Q6：Offset Calibration 是否会改变 Detector 硬件状态？

### Answer

不会。

Offset Calibration 仅读取 Detector 当前响应状态并生成 Calibration Data。

不会修改 Detector 硬件参数或电路状态。

---

## Q7：Offset Calibration 与 Gain Calibration 有什么关系？

### Answer

Offset Calibration 是 Gain Calibration 的基础。

标准执行顺序为：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

未完成 Offset Calibration 时，不建议继续执行 Gain Calibration。

---

## Q8：Offset Calibration 完成后为什么图像仍然异常？

### Answer

可能原因包括：

- Gain Calibration 未完成
- Defect Calibration 未完成
- Calibration Data 未正确加载
- Detector 存在硬件异常
- 图像异常来源并非 Offset

应结合 Gain、Defect 及 Image Diagnosis 进一步分析。

---

## Q9：Offset Calibration 成功是否表示 Detector 一定正常？

### Answer

不一定。

Offset Calibration 成功仅表示 Offset Calibration 流程正常完成。

仍需结合：

- Gain Calibration
- Defect Calibration
- 测试图像
- Detector Self Test

综合判断 Detector 状态。

---

## Q10：为什么重复执行 Offset Calibration，结果会有差异？

### Answer

轻微差异属于正常现象。

若差异明显，应检查：

- Detector 温度变化
- 电源稳定性
- 网络稳定性
- 是否存在 X-Ray 干扰
- Detector 工作状态

---

## Q11：Offset Calibration 会修复 Bad Pixel 吗？

### Answer

不会。

Offset Calibration 仅补偿 Pixel 的固定偏移。

Bad Pixel 的识别与补偿由 Defect Calibration 完成。

---

## Q12：Offset Calibration 是否可以单独执行？

### Answer

可以。

Offset Calibration 可独立执行。

但若需要完成完整 Calibration，建议按以下顺序执行：

```text
Offset

↓

Gain

↓

Defect
```

---

## Q13：Offset Calibration 是否会影响 Gain Data？

### Answer

会间接影响。

Gain Calibration 建立在 Offset Correction 基础之上。

若 Offset Data 不正确，则 Gain Data 可能失效。

---

## Q14：Offset Calibration 是否需要定期执行？

### Answer

根据产品维护规范执行。

通常在以下情况建议重新 Calibration：

- 定期维护
- 维修后
- Firmware 升级后（依据产品要求）
- 图像质量下降
- Calibration Data 更新需求

---

## Q15：Offset Calibration 的最终输出是什么？

### Answer

完成 Calibration 后生成：

- Offset Data
- Offset Table
- Calibration Data Update

这些数据将在后续图像处理中用于 Offset Correction。

---

# 3. Quick Troubleshooting Guide

| Symptom | Recommended Check |
|----------|-------------------|
| Calibration Failed | Detector、Communication、Calibration Command |
| Background Offset | Offset Data、Calibration Data |
| Fixed Pattern Noise | Offset Data、Gain Calibration |
| Calibration Timeout | Network、Detector Status |
| Calibration Success but Image Abnormal | Gain、Defect、Image Diagnosis |

---

# 4. Related Documents

Calibration：

- OffsetWorkflow.md
- OffsetParameter.md
- OffsetFailure.md
- OffsetTroubleshooting.md

Theory：

- ../CalibrationTheory/OffsetTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 5. Document Boundary

本文件负责：

- Offset Calibration 常见问题
- 标准技术解答
- 快速故障查询
- FAQ 索引

本文件不负责：

- Calibration 操作流程
- Calibration 参数配置
- 故障详细分析
- SOP
- SDK API

详细内容分别由对应文档说明。

---

# 6. Summary

Offset FAQ 为现场工程师提供 Offset Calibration 的快速参考。

遇到复杂故障时，应结合：

- OffsetTroubleshooting.md
- FailureKnowledge
- DecisionTree
- SOP

进行进一步分析和处理。