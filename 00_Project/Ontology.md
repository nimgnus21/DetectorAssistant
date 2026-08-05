# Detector Assistant Ontology

Version: V1.0

---

# 1. Purpose

Ontology（知识本体）定义整个 Detector Assistant 工程知识系统中：

- Object（对象）
- Attribute（属性）
- Relationship（关系）
- Rule（规则）
- Constraint（约束）

Ontology 是整个知识系统的推理基础。

ObjectModel 定义"有哪些对象"。

Ontology 定义"对象之间如何关联"。

---

# 2. Knowledge Hierarchy

Knowledge System

↓

Object

↓

Attribute

↓

Relationship

↓

Rule

↓

Decision

↓

SOP

↓

Case

---

# 3. Core Objects

Knowledge System 包含以下核心对象：

Product

System

Hardware

Software

Calibration

Workflow

Failure

Image Artifact

Decision Tree

SOP

Case

Error Code

Parameter

Document

Reference

---

# 4. Object Attributes

每一个 Object 都拥有以下标准属性。

Name

Description

Type

Category

Version

Status

Applicable Product

Input

Output

Dependency

Reference

Keyword

Owner

Created Date

Updated Date

---

# 5. Relationship Type

Ontology 允许以下关系。

## Structural Relationship（结构关系）

Part Of

Contains

Belongs To

Instance Of

Subclass Of

---

## Dependency Relationship（依赖关系）

Depends On

Required By

Initialized By

Configured By

Powered By

Triggered By

---

## Signal Relationship（信号关系）

Input To

Output From

Receives

Transmits

Converts

Stores

Processes

---

## Functional Relationship（功能关系）

Controls

Monitors

Measures

Calculates

Generates

Acquires

Transfers

Corrects

Displays

---

## Failure Relationship（故障关系）

Causes

Results In

Influences

Related Failure

Symptom Of

Failure Source

Failure Level

---

## Troubleshooting Relationship（排查关系）

Diagnosed By

Verified By

Resolved By

Recovered By

Prevented By

---

## Engineering Relationship（工程关系）

Installed By

Configured By

Calibrated By

Maintained By

Tested By

Validated By

---

## Documentation Relationship（文档关系）

Described In

Referenced By

Explained In

Recorded In

---

# 6. Rule

所有知识必须遵守以下规则。

---

Rule 1

Every Object Must Have Type

每个对象必须属于一种 Object Type。

---

Rule 2

Every Object Must Have Relationship

任何对象都不能孤立存在。

---

Rule 3

Every Failure Must Have Cause

所有故障必须存在原因。

---

Rule 4

Every Failure Must Have Solution

所有故障必须对应解决方法。

---

Rule 5

Every SOP Must Reference Workflow

所有 SOP 必须关联 Workflow。

---

Rule 6

Every Image Artifact Must Reference Hardware

所有图像异常必须关联至少一个硬件模块。

---

Rule 7

Every Calibration Must Reference Software

所有校准必须关联软件操作。

---

Rule 8

Every Case Must Reference Failure

所有案例必须对应故障对象。

---

Rule 9

Every Parameter Must Belong To Object

所有参数必须属于某一个对象。

---

Rule 10

Every Document Must Have Source

所有知识必须具有来源。

来源包括：

User Manual

Service Manual

SDK Manual

Engineering Experience

Case

Lab Test

---

# 7. Inference Rule

AI 推理采用以下顺序。

Customer Question

↓

Workflow

↓

Failure

↓

Decision Tree

↓

Hardware

↓

Software

↓

Calibration

↓

Case

↓

Solution

---

# 8. Constraint

整个知识系统遵循以下约束。

---

Single Source Of Truth

每一个知识点只能存在一个正式定义。

---

One Topic One Document

一个文档只描述一个主题。

---

Relationship First

优先建立关系，再补充内容。

---

Fact First

事实优先。

经验必须标注。

推测必须标注。

---

No Duplicate Knowledge

禁止重复维护同一个知识。

---

Source Required

所有结论必须注明来源。

---

# 9. Knowledge Lifecycle

Create

↓

Review

↓

Approve

↓

Release

↓

Update

↓

Archive

---

# 10. AI Reasoning Path

AI 不直接搜索文档。

AI 按以下顺序推理：

Object

↓

Relationship

↓

Workflow

↓

Failure

↓

Decision Tree

↓

Case

↓

Solution

---

# 11. Future Extension

后续允许新增 Ontology。

Firmware

Driver

SDK API

Network Protocol

Communication Stack

Image Algorithm

AI Model

Production

Quality Control

Manufacturing

Training

Service Report

---

# 12. Ontology Principles

Object 不等于文档。

Relationship 比文档更重要。

Workflow 比参数更重要。

Failure 必须可追溯。

Decision 必须可验证。

Case 必须可复现。

Knowledge 必须持续演进。

---

End of Ontology