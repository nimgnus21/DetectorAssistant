# FailureKnowledge

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Modules:
- ../03_Hardware/
- ../04_Software/
- ../05_Calibration/
- ../06_Workflow/
- ../08_Service/
- ../09_DecisionTree/

---

# 1. Module Purpose

Failure Knowledge（故障知识库）用于建立数字平板探测器（Flat Panel Detector，FPD）的系统化故障知识体系。

本模块关注故障的形成机理、影响范围、典型表现、诊断依据及关联模块，为研发、测试、售后及现场工程师提供统一的故障分析参考。

本模块回答的问题是：

> **为什么会发生该故障？**

而不是：

- 正常工作流程（Workflow）
- 现场排查步骤（Decision Tree）
- 维修操作方法（Service）

---

# 2. Module Scope

本模块覆盖 Detector 全生命周期中的主要故障类型，包括：

- Hardware Failure
- Software Failure
- Communication Failure
- Calibration Failure
- Image Failure
- Power Failure
- Environmental Failure
- System Failure

适用于：

- Factory Debug
- Clinical Installation
- Field Service
- Product Verification
- Failure Analysis
- Technical Training

---

# 3. Module Objectives

Failure Knowledge 的主要目标包括：

- 建立统一故障分类体系
- 解释故障产生机理
- 描述故障表现形式
- 分析故障影响范围
- 建立故障关联关系
- 为 Decision Tree 提供理论依据

---

# 4. Module Structure

```text
07_FailureKnowledge/

README.md

FailureClassification.md

FailureAnalysisMethod.md

FailureCode.md

HardwareFailure/

SoftwareFailure/

CalibrationFailure/

CommunicationFailure/

ImageFailure/

EnvironmentFailure/

PowerFailure/

SystemFailure/
```

---

# 5. Knowledge Architecture

整个模块采用统一知识结构：

```text
Failure

↓

Cause

↓

Mechanism

↓

Symptoms

↓

Impact

↓

Detection

↓

Related Module

↓

Reference
```

每一种故障均按照相同结构进行组织，便于横向比较与快速检索。

---

# 6. Failure Classification

故障按来源划分为以下类别：

| Category | Description |
|----------|-------------|
| Hardware Failure | 硬件器件故障 |
| Software Failure | 软件及固件故障 |
| Communication Failure | 网络与通信故障 |
| Calibration Failure | 校准相关故障 |
| Image Failure | 图像质量异常 |
| Power Failure | 电源及供电故障 |
| Environment Failure | 环境因素导致的故障 |
| System Failure | 多模块耦合系统故障 |

详细分类参见：

- FailureClassification.md

---

# 7. Relationship with Workflow

Workflow 描述：

> Detector 如何正常工作。

Failure Knowledge 描述：

> Workflow 为什么失败。

关系如下：

```text
Workflow

↓

Failure Occurred

↓

Failure Knowledge

↓

Decision Tree

↓

Root Cause
```

---

# 8. Relationship with DecisionTree

Failure Knowledge：

解释：

- 为什么发生
- 会产生什么影响
- 哪些模块有关

Decision Tree：

负责：

- 如何判断
- 如何定位
- 如何排查
- 如何恢复

两者关系：

```text
Failure Knowledge

↓

Theory

↓

Decision Tree

↓

Engineering Diagnosis
```

---

# 9. Relationship with Hardware Module

Hardware Module：

介绍：

- 结构
- 原理
- 工作方式

Failure Knowledge：

介绍：

- 损坏方式
- 故障模式
- 故障影响

例如：

```text
Hardware

Photodiode

↓

Failure Knowledge

Photodiode Failure
```

---

# 10. Relationship with Calibration Module

Calibration 模块负责：

- Offset
- Gain
- Defect
- Template

Failure Knowledge 负责：

- Offset Failure
- Gain Failure
- Defect Failure
- Template Failure

重点分析校准失败的原因及影响，而非校准流程本身。

---

# 11. Relationship with Service Module

Service 模块负责：

- 更换部件
- 软件升级
- 校准操作
- 维修流程

Failure Knowledge 不涉及维修步骤，仅提供理论分析和故障解释。

---

# 12. Relationship with DecisionTree Module

DecisionTree 以 Failure Knowledge 为理论基础。

例如：

```text
Image Noise

↓

Failure Knowledge

Noise Cause

↓

Decision Tree

Noise Troubleshooting
```

Failure Knowledge 解释"为什么"，DecisionTree回答"怎么办"。

---

# 13. Recommended Reading Order

建议阅读顺序：

```text
03_Hardware

↓

06_Workflow

↓

07_FailureKnowledge

↓

09_DecisionTree

↓

08_Service
```

对于现场工程师，建议阅读：

```text
Workflow

↓

FailureKnowledge

↓

DecisionTree
```

---

# 14. Applicable Personnel

适用于：

| Role | Purpose |
|------|---------|
| R&D Engineer | 故障机理分析 |
| Test Engineer | 产品验证 |
| Service Engineer | 故障定位 |
| Technical Support | 技术支持 |
| Application Engineer | 客户问题分析 |
| Training Engineer | 技术培训 |

---

# 15. Design Principles

本模块遵循以下原则：

- 以故障机理为核心。
- 每篇文档仅描述一种故障主题。
- 不重复 Workflow 内容。
- 不包含维修操作步骤。
- 保持与 Hardware、Calibration、Workflow 模块的一一对应关系。
- 所有故障均可关联至 DecisionTree。

---

# 16. Navigation

建议阅读路径：

```text
README

↓

FailureClassification

↓

FailureAnalysisMethod

↓

FailureCode

↓

Specific Failure

↓

DecisionTree

↓

Service
```

---

# 17. Knowledge Graph

```text
Hardware

↓

Workflow

↓

Failure

├── Hardware Failure
├── Software Failure
├── Calibration Failure
├── Communication Failure
├── Image Failure
├── Environment Failure
├── Power Failure
└── System Failure

↓

DecisionTree

↓

Service
```

---

# 18. Summary

Failure Knowledge 是 DetectorAssistant 的故障理论中心，负责建立完整、统一的故障知识体系。通过对故障类型、形成机理、典型表现、影响范围及关联模块的系统整理，为 Workflow、DecisionTree 与 Service 模块提供理论支撑，实现从**正常工作**、**故障分析**到**现场诊断**的完整知识闭环。