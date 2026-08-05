# System Writing Standard

Version: V1.0

Applicable Directory:

02_System

---

# 1. Purpose

本规范定义 02_System 目录下所有文档的编写原则、职责边界、引用规则及统一结构。

目标：

建立统一、可维护、可扩展、适用于 AI 检索与工程维护的系统层知识。

---

# 2. System Layer Definition

System 层用于描述数字平板探测器整体架构。

职责包括：

- 系统组成
- 系统关系
- 系统流程
- 模块职责
- 数据流向
- 信号流向
- 时序关系

System 不负责描述模块内部实现。

---

# 3. Design Principle

System Layer 采用 Relationship First 原则。

即：

首先描述模块之间的关系。

其次描述数据流向。

最后引用详细知识。

禁止在 System 层重复描述 Hardware、Software、Calibration 内部内容。

---

# 4. Single Responsibility Principle

每篇文档只回答一个核心问题。

| Document | Question |
|----------|----------|
| DetectorArchitecture | 系统由什么组成（What） |
| SignalFlow | 信号如何变化（Signal） |
| TimingArchitecture | 系统何时工作（When） |
| ImagePipeline | 图像如何处理（Image Process） |
| Communication | 数据如何传输（Transport） |
| PowerArchitecture | 能量如何分配（Power） |

不得跨越职责范围。

---

# 5. Reference Principle

System 文档必须引用下层知识。

不得复制下层知识。

例如：

SignalFlow

↓

引用

03_Hardware/ADC

而不是解释 ADC 工作原理。

Calibration

↓

引用

05_Calibration/Offset

而不是描述 Offset 校准步骤。

---

# 6. Knowledge Boundary

System 层允许描述：

✓ 系统结构

✓ 数据流

✓ 信号流

✓ 工作流程

✓ 模块关系

✓ 调用关系

✓ 生命周期

System 层禁止描述：

✗ 电路设计

✗ 芯片工作原理

✗ 软件实现

✗ 校准算法

✗ 图像算法

✗ 故障维修步骤

✗ SOP 操作步骤

---

# 7. Knowledge Layer Dependency

System

↓

Hardware

↓

Software

↓

Calibration

↓

Workflow

↓

FailureKnowledge

↓

ImageDiagnosis

↓

DecisionTree

↓

Case

↓

SOP

所有引用保持单向。

下层不得反向定义上层。

---

# 8. Unified Document Structure

所有 System 文档统一采用以下结构。

# 1. Purpose

# 2. Scope

# 3. Core Concept

# 4. Architecture

# 5. Functional Relationship

# 6. Process Flow

# 7. Dependency

# 8. Engineering Characteristics

# 9. Failure Mapping

# 10. Knowledge Relationship

# 11. Reference

不得随意调整章节顺序。

---

# 9. Diagram Principle

每篇文档至少包含：

一张总体关系图。

流程图使用：

↓

表示单向流程。

系统关系使用：

├──

表示层级。

禁止混用。

---

# 10. Naming Convention

模块名称统一使用英文。

说明统一使用中文。

例如：

Readout ASIC

Gate Driver

Timing Controller

Communication

Power Board

保持与目录名称一致。

---

# 11. Reference Rule

每个模块第一次出现时必须引用对应知识。

例如：

Readout ASIC

Reference：

03_Hardware/Readout_ASIC

Offset Calibration

Reference：

05_Calibration/Offset

---

# 12. Source Classification

所有知识必须标注来源。

Fact

产品资料直接说明。

Theory

培训资料理论说明。

Engineering

现场经验。

Inference

依据 Fact 和 Theory 推导得到。

禁止将推导内容标记为 Fact。

---

# 13. Engineering Requirement

System 文档应满足：

- 新员工能够理解系统组成。
- 售后工程师能够定位知识入口。
- 售前工程师能够解释系统结构。
- AI 能够完成知识导航。
- 后续文档能够直接引用。

---

# 14. Maintenance Rule

新增内容必须满足：

不重复。

可引用。

职责单一。

如涉及 Hardware、Software、Calibration 等内容，应新增对应引用，而非扩写 System 文档。

---

# 15. Version Management

重大结构调整：

Version +1.0

内容补充：

Version +0.1

文字修订：

Revision 更新。

---

# 16. Final Principle

System Layer 是整个知识库的导航层。

它建立知识之间的关系。

它不是知识终点。

任何需要深入理解的内容，应跳转至对应专业模块。