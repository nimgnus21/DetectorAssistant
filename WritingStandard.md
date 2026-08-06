# Knowledge Base Writing Standard

Version: V1.0

Status: Released

Last Update: 2026-08

---

# 1. Purpose

本文档用于统一整个技术知识库的编写规范。

目标：

- 保证所有文档风格一致
- 避免重复内容
- 建立统一引用关系
- 降低维护成本
- 提高检索效率
- 形成模块化知识体系

本文档适用于整个 Knowledge Base。

---

# 2. Design Philosophy

整个知识库遵循：

> **One Knowledge, One Location**

即：

**一个知识点只能有一个权威来源（Single Source of Truth，SSOT）。**

其它文档仅进行引用。

禁止：

- 重复解释
- 重复绘制流程
- 重复分析原因
- 大段复制内容

---

# 3. Knowledge Architecture

整个知识库采用模块化设计。

每个一级目录仅负责回答一个问题。

| Directory | Core Question |
|------------|---------------|
| 01_Product | 产品是什么？ |
| 02_Hardware | 硬件如何组成？ |
| 03_Software | 软件如何组成？ |
| 04_Theory | 为什么能够工作？ |
| 05_Calibration | 如何完成校准？ |
| 06_Workflow | 标准流程是什么？ |
| 07_FailureKnowledge | 为什么会失败？ |
| 08_ImageDiagnosis | 图像代表什么？ |
| 09_DecisionTree | 下一步检查哪里？ |
| 10_FAE | 如何提供现场支持？ |
| 11_Case | 现场发生了什么？ |
| 12_FAQ | 常见问题有哪些？ |
| 13_Principles | 底层工作原理是什么？ |
| 14_Interface | 接口如何定义？ |
| 15_Development | 软件开发相关内容 |
| 16_Test | 如何验证？ |
| 17_Tools | 工具如何使用？ |

任何文档不得超出所属模块职责。

---

# 4. Responsibility Definition

## 05_Calibration

负责：

- 校准目的
- 校准流程
- 校准要求
- 校准参数

禁止：

- 大量案例
- 故障分析
- 图像诊断

---

## 06_Workflow

负责：

标准 SOP。

包括：

- 输入
- 输出
- 执行步骤
- 判断节点

禁止：

- 原理分析
- 案例分析

---

## 07_FailureKnowledge

负责：

解释：

**为什么发生。**

包括：

- Root Cause
- Failure Mechanism
- Failure Classification
- Failure Principle

禁止：

- 大量现场案例
- SOP
- 工具说明

---

## 08_ImageDiagnosis

负责：

解释：

**图像说明什么。**

包括：

- 图像特点
- 图像规律
- 图像形成原因
- 相似 Artifact 对比

禁止：

- 维修流程
- 工具操作

---

## 09_DecisionTree

负责：

回答：

> 下一步检查哪里？

采用：

YES / NO

树状结构。

禁止：

- 长篇解释
- 原理分析

---

## 11_Case

负责：

记录：

真实现场案例。

重点：

- 发生经过
- 排查过程
- 最终解决
- 经验总结

禁止：

- 重复编写 FailureKnowledge
- 重复 Workflow
- 重复 Theory

---

## 17_Tools

负责：

工具使用。

包括：

- 安装
- 参数
- 使用方法
- 输出结果

禁止：

- 故障分析
- 产品原理

---

# 5. Single Source of Truth

知识库采用：

SSOT（Single Source of Truth）

例如：

Ghost 原理：

唯一位置：

```
07_FailureKnowledge
```

Ghost 图像：

唯一位置：

```
08_ImageDiagnosis
```

Ghost 案例：

唯一位置：

```
11_Case
```

Ghost 校准：

唯一位置：

```
05_Calibration
```

Ghost Workflow：

唯一位置：

```
06_Workflow
```

其它文档仅引用。

---

# 6. Cross Reference Rules

文档之间采用引用关系。

例如：

```
Related Documents

- ../../07_FailureKnowledge/...
- ../../06_Workflow/...
- ../../17_Tools/...
```

禁止复制整段内容。

---

# 7. Case Writing Standard

Case 不属于教材。

Case 应记录：

真实事件。

统一模板：

```
1. Case Summary

2. Customer Environment

3. Fault Description

4. Troubleshooting Timeline

5. Root Cause

6. Solution

7. Verification

8. Lessons Learned

9. Related Documents
```

Root Cause：

仅一句话。

详细分析：

引用：

```
07_FailureKnowledge
```

---

# 8. Workflow Writing Standard

Workflow 必须采用：

```
Input

↓

Process

↓

Decision

↓

Output
```

每一步：

- 一个动作
- 一个目的

禁止解释原理。

---

# 9. FailureKnowledge Writing Standard

统一结构：

```
Definition

↓

Failure Mechanism

↓

Root Cause

↓

Typical Scenario

↓

Detection Method

↓

Countermeasure

↓

Reference
```

重点：

解释：

为什么。

---

# 10. ImageDiagnosis Writing Standard

统一结构：

```
Definition

↓

Image Feature

↓

Typical Appearance

↓

Formation Mechanism

↓

Possible Cause

↓

Differential Diagnosis

↓

Reference
```

重点：

识别。

而不是维修。

---

# 11. DecisionTree Writing Standard

统一采用：

```
Question

↓

YES

↓

NO
```

每个节点：

只判断一件事情。

禁止：

超过一句解释。

---

# 12. Naming Rules

文件：

采用：

PascalCase。

例如：

```
Ghost.md

Lag.md

Noise.md

ConnectionFailed.md
```

禁止：

空格。

禁止：

中文文件名。

---

# 13. Language Standard

统一使用：

专业术语。

例如：

使用：

- Offset
- Gain
- Defect
- ROI
- Frame Rate

避免：

口语化描述。

第一次出现时：

可增加中文说明。

之后统一使用英文术语。

---

# 14. Revision Principle

修改原则：

新增内容：

优先修改：

原知识所属文档。

禁止：

复制到其它模块。

所有修改应保持：

Single Source of Truth。

---

# 15. Final Principle

整个知识库遵循以下原则：

- Single Source of Truth
- Low Coupling
- High Cohesion
- Modular Design
- Standard Naming
- Cross Reference
- Easy Maintenance
- Easy Expansion

目标：

建立可持续维护的企业级技术知识库。