# DefectFAQ

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
- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectFailure.md
- DefectTroubleshooting.md
- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationFlow.md
- ../../07_FailureKnowledge/
- ../../09_DecisionTree/

---

# 1. Purpose

Defect FAQ 汇总 Defect Calibration 过程中最常见的问题，并提供统一的技术说明。

本文件用于帮助现场工程师、售后工程师及技术支持人员快速理解 Defect Calibration、Defect Template 及 Defect Correction 的基本概念、执行要求及常见问题。

本文件不替代 Workflow、Troubleshooting 或 SOP。

---

# 2. Frequently Asked Questions

---

## Q1：为什么需要执行 Defect Calibration？

### Answer

Defect Calibration 用于识别 Detector 中响应异常的 Pixel，并生成 Defect Template。

Defect Template 在图像处理中用于 Defect Correction，以降低异常 Pixel 对图像质量的影响。

---

## Q2：Defect Calibration 必须在 Offset Calibration 和 Gain Calibration 之后执行吗？

### Answer

必须。

标准 Calibration 顺序为：

```text
Offset Calibration

↓

Gain Calibration

↓

Defect Calibration
```

Offset Data 与 Gain Data 是 Defect Detection 的基础。

---

## Q3：Defect Calibration 的最终输出是什么？

### Answer

Defect Calibration 完成后生成：

- Defect Template
- Defect Pixel List
- Defect Line List
- Defect Map
- Calibration Data Update

上述数据参与后续 Defect Correction。

---

## Q4：什么是 Defect Template？

### Answer

Defect Template 是 Defect Calibration 的核心输出。

其中保存 Detector 当前识别出的异常 Pixel、异常 Line 及相关校正信息，供 Image Pipeline 在 Defect Correction 阶段使用。

---

## Q5：Factory Template 与 User Template 有什么区别？

### Answer

Factory Template 为出厂校准生成，记录出厂时确认的异常 Pixel。

User Template 为现场重新 Calibration 或人工编辑后生成，用于记录后续新增的异常 Pixel。

最终参与图像处理的是 Active Template。

---

## Q6：什么是 Template Overlay？

### Answer

Template Overlay 是将多个 Defect Template 按照系统规则组合，生成最终 Active Template 的过程。

Overlay 完成后，新的 Active Template 将参与 Defect Correction。

---

## Q7：为什么 Defect Calibration 成功后图像仍存在坏点？

### Answer

可能原因包括：

- Active Template 未更新
- Template Upload 未完成
- Template Overlay 未完成
- Calibration Data 未正确加载
- 图像中的异常并非 Defect Pixel

应结合 DefectTroubleshooting.md 进一步分析。

---

## Q8：Defect Calibration 会修复 Bad Pixel 吗？

### Answer

不会修复硬件。

Defect Calibration 仅识别异常 Pixel，并通过 Defect Correction 对图像进行补偿。

若 Pixel 已发生硬件损坏，Calibration 不会恢复其物理功能。

---

## Q9：为什么需要上传或下载 Defect Template？

### Answer

Template Upload 用于将新的 Defect Template 写入 Detector。

Template Download 用于：

- 数据备份
- 数据恢复
- 技术分析
- 故障定位

上传或下载完成后，应确认 Template Version 一致。

---

## Q10：修改 Defect Template 后为什么图像没有变化？

### Answer

可能原因包括：

- Template 未保存
- Upload 未完成
- Active Template 未切换
- Calibration Data 未更新
- 图像未重新采集

应确认新的 Active Template 已参与图像处理。

---

## Q11：Defect Calibration 是否需要定期执行？

### Answer

根据产品维护规范执行。

通常在以下情况建议重新 Calibration：

- Detector 更换
- Detector 维修
- 新增异常 Pixel
- Calibration Data 更新
- 图像质量下降
- 系统维护要求

---

## Q12：Defect Template 可以人工修改吗？

### Answer

可以。

支持根据产品功能进行：

- Add Defect Pixel
- Delete Defect Pixel
- Add Defect Line
- Delete Defect Line

修改完成后，应重新保存并更新 Active Template。

---

## Q13：重新执行 Defect Calibration 会覆盖原来的 Template 吗？

### Answer

根据产品的软件实现方式，新的 Calibration 结果可能更新当前 Defect Template。

若系统支持 Template 管理或 Overlay，应确认 Factory Template、User Template 及 Active Template 的关系，避免误覆盖有效数据。

---

## Q14：Defect Calibration 会影响 Offset Data 或 Gain Data 吗？

### Answer

不会。

Defect Calibration 仅生成 Defect Template，并更新相关 Calibration Data。

Offset Data 与 Gain Data 保持不变。

---

## Q15：Defect Calibration 成功是否表示 Detector 完全正常？

### Answer

不一定。

Defect Calibration 成功仅表示 Defect Calibration 流程完成。

仍需结合：

- Offset Calibration
- Gain Calibration
- 测试图像
- Detector Self Test

综合判断 Detector 工作状态。

---

# 3. Quick Troubleshooting Guide

| Symptom | Recommended Check |
|----------|-------------------|
| Defect Calibration Failed | Detector、Communication、Offset、Gain |
| Template Generation Failed | Calibration Image、Detection Module |
| Template Upload Failed | Communication、Calibration Data |
| Template Overlay Failed | Factory Template、User Template、Active Template |
| Bad Pixel Still Visible | Active Template、Defect Correction |
| Calibration Success but Image Abnormal | Template、Calibration Data、Image Diagnosis |

---

# 4. Related Documents

Calibration：

- DefectWorkflow.md
- DefectParameter.md
- DefectTemplate.md
- DefectFailure.md
- DefectTroubleshooting.md

Theory：

- ../CalibrationTheory/DefectTheory.md
- ../CalibrationTheory/CalibrationFlow.md

Knowledge：

- ../../07_FailureKnowledge/

Decision：

- ../../09_DecisionTree/

---

# 5. Document Boundary

本文件负责：

- Defect Calibration 常见问题
- Defect Template 基本说明
- 标准技术解释
- 快速故障查询
- FAQ 索引

本文件不负责：

- Calibration 操作流程
- Detection Algorithm
- Template 生命周期管理细节
- 软件界面说明
- SDK API

详细内容分别由对应文档说明。

---

# 6. Summary

Defect FAQ 为现场工程师提供 Defect Calibration 与 Defect Template 的快速参考。

遇到复杂问题时，应结合：

- DefectTroubleshooting.md
- DefectFailure.md
- FailureKnowledge
- DecisionTree
- SOP

进行进一步分析与处理。