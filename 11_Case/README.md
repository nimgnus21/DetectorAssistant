# Case

Version: V1.1

Module: 11_Case

Status: Released

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector
- Pluto Series
- Veterinary DR
- Medical DR
- Industrial Detector（部分案例适用）

Related Documents:

- [Case Template](../00_Project/Templates/CaseTemplate.md)
- [Case Index](../00_Project/Index/CaseIndex.md)
- [Failure Knowledge](../07_FailureKnowledge/README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [SOP](../10_SOP/README.md)
- [ErrorCode](../12_ErrorCode/)
- [Tools](../17_Tools/README.md)

---

# 1. Overview

Case 模块用于沉淀 FAE（Field Application Engineer）在现场安装、调试、维修、培训及客户支持过程中积累的**真实案例**。

与其他模块不同：

- Workflow 描述标准操作流程。
- FailureKnowledge 介绍故障现象、机理和排查方向。
- DecisionTree 提供故障定位路径。
- SOP 规定标准执行步骤。
- Tools 提供具体执行工具。
- **Case 记录经过验证的现场/实验室问题、处理过程与结果。**

Case 是技术支持知识库的反馈层：已有知识用于处理问题，处理完成后将新的、经过验证的经验反向沉淀到知识库。

---

# 2. Objectives

Case 模块目标：

- 沉淀真实现场经验
- 提高故障定位效率
- 避免重复踩坑
- 建立标准案例库
- 为新人培训提供参考
- 为研发提供现场反馈依据
- 识别 FailureKnowledge / DecisionTree / SOP 的知识缺口

---

# 3. Module Structure

```text
11_Case

├── README.md
│
├── Communication
├── Calibration
├── Image
├── Firmware
├── Software
└── Customer
```

说明：

- **Communication**：连接、网络及通信相关案例。
- **Calibration**：Offset、Gain、Defect、Ghost 等校准案例。
- **Image**：图像异常及处理案例。
- **Firmware**：固件升级、版本管理及兼容性案例。
- **Software**：SDK、License、软件配置案例。
- **Customer**：送样、OQC、客户支持及现场服务案例。

未建立真实案例前，不为填充目录而创建虚构 Case。

---

# 4. Case Classification

所有 Case 按实际问题归入最主要的故障域。一个 Case 可以关联多个知识模块，但只保留一个主分类目录，避免同一案例重复复制。

- Communication：连接、网络、通信、超时、图像传输问题
- Calibration：Offset、Gain、Defect、Ghost、Dynamic Calibration
- Image：横纹、坏点/坏线、噪点、Lag、Ghost、Image Shift 等
- Firmware：升级、版本不匹配、启动或恢复问题
- Software：SDK、License、配置、Mode、API/Exception
- Customer：Sample、OQC、培训、RMA、现场服务

---

# 5. Case Admission Rules

## 5.1 Required Evidence

正式 Case 必须至少具备：

1. **现象**：客户或实验室观察到的实际问题。
2. **环境**：产品型号、关键版本、必要配置。
3. **排查过程**：实际执行过的步骤，而不是理论建议。
4. **最终处理或已验证根因**：至少其中一项经过验证。
5. **验证结果**：恢复、未恢复或现象变化的客观结果。

缺少以上信息时，不应标记为“已解决真实 Case”。

## 5.2 Case Status

每个新 Case 应使用以下状态之一：

| Status | Definition |
|---|---|
| `Verified` | 根因或处理措施已通过现场/实验室验证 |
| `Resolved` | 问题恢复，但根因未完全确认 |
| `Unresolved` | 已完成排查但尚未解决 |
| `Hypothesis` | 仅存在推断，不得作为正式技术结论 |
| `Archived` | 已过期，仅供历史追溯 |

`Hypothesis` 可以保存为排查记录，但不得作为 FailureKnowledge、DecisionTree 或 SOP 的正式结论来源。

---

# 6. Standard Case Template

新 Case 必须优先使用：[Case Template](../00_Project/Templates/CaseTemplate.md)。

核心结构：

```text
Case ID / Status
    ↓
Problem Description
    ↓
Applicable Product / Environment
    ↓
Fault Phenomenon
    ↓
Diagnostic Process
    ↓
Verified Root Cause / Treatment
    ↓
Verification Result
    ↓
Related Knowledge
    ↓
Feedback Required?
```

---

# 7. Case Feedback Mechanism

Case 完成后必须检查是否需要反向更新知识库。

```text
Customer / Lab Problem
        ↓
Search Existing Knowledge
        ↓
FailureKnowledge / DecisionTree / SOP / Tools
        ↓
Execute and Verify
        ↓
Create or Update Case
        ↓
Knowledge Gap Review
   ┌────┼────┬────┐
   ↓    ↓    ↓    ↓
Failure Tree SOP Tool/ErrorCode
        ↓
Update Index and Related Links
```

## 7.1 Mandatory Feedback Check

每个 `Verified` 或 `Resolved` Case 完成后检查：

- 是否发现新的故障现象？ → `07_FailureKnowledge`
- 是否存在新的诊断分流条件？ → `09_DecisionTree`
- 是否需要修改标准执行步骤？ → `10_SOP`
- 是否需要新增工具使用场景？ → `17_Tools`
- 是否发现错误码或版本相关信息？ → `12_ErrorCode`
- 是否需要统一新术语？ → `14_Glossary`
- 是否需要增加检索入口？ → `00_Project/Index`

如果无需更新，也应在 Case 中记录“Knowledge Feedback: No update required”，避免后续重复审查。

---

# 8. Case Writing Principles

## 真实性

案例来源应为：

- 客户现场
- 公司实验室
- 培训记录
- 内部验证

不得把通用排查文档改写为虚构 Case。

## 可复现

应尽量描述：

- 操作步骤
- 环境条件
- 软件版本
- Firmware 版本
- Detector 型号

## 可验证

解决方案必须具有明确验证方式，例如：

- 图像恢复正常
- 校准成功
- 通信恢复
- 日志无异常
- 连续运行稳定

## 可追溯

建议记录：

- 日期
- 产品型号
- Detector SN（如允许）
- Firmware Version
- SDK Version
- 作者
- 来源

---

# 9. Relationship with Other Modules

Case 不独立存在，应形成可追溯闭环：

```text
FailureKnowledge
        ↓
DecisionTree
        ↓
SOP
        ↓
Tools
        ↓
Field Verification
        ↓
Case
        ↓
Knowledge Feedback
        ├── FailureKnowledge
        ├── DecisionTree
        ├── SOP
        ├── Tools
        ├── ErrorCode
        └── Index
```

Case 中的 `Related Documents` 应优先链接到具体文件，而不是只写目录名称。

---

# 10. Engineering Experience

经过验证的工程经验可以记录在 Case 中，但必须注明：

- 适用产品/型号
- 适用版本
- 验证环境
- 验证结果

例如，产品专属校正步骤不能自动推广到其他型号。

---

# 11. Continuous Maintenance

Case 属于持续更新模块。

新增 Case：

- 新产品问题
- 新 Firmware / SDK 问题
- 新客户现场问题
- 已验证的新故障模式

更新已有 Case：

- 新版本解决方案
- 新增验证结果
- 新的预防措施
- 关联知识更新

建议每季度或重大版本发布后复审 Case 状态和关联链接。

---

# 12. References

- [Case Template](../00_Project/Templates/CaseTemplate.md)
- [Case Index](../00_Project/Index/CaseIndex.md)
- [FailureKnowledge](../07_FailureKnowledge/README.md)
- [DecisionTree](../09_DecisionTree/README.md)
- [SOP](../10_SOP/README.md)
- [Tools](../17_Tools/README.md)

---

# 13. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Added case admission status and mandatory knowledge feedback mechanism |
| V1.0 | 2026-08 | Established Case module navigation and writing principles |