# Detector Assistant Object Model

Version: V1.0

---

# 1. Purpose

Object Model（对象模型）用于定义 Detector Assistant 知识系统中的所有知识对象。

所有知识必须归属于某一种 Object Type。

任何新增文档、SOP、案例、故障、图片、参数，都必须先确定所属 Object，再建立关联关系。

Object Model 是整个知识系统的数据基础。

---

# 2. Design Principles

## 2.1 One Concept One Object

一个对象只描述一个概念。

例如：

Gate Driver

Readout ASIC

Gain Calibration

Dead Pixel

Connection Failure

不能把多个知识写在同一个 Object 中。

---

## 2.2 Everything is an Object

整个知识系统中的任何知识，都应该属于某一个 Object。

例如：

产品

硬件

软件

工作流

参数

故障

图像异常

SOP

案例

日志

错误码

模板

---

## 2.3 Relationship First

Object 不允许孤立存在。

每个 Object 都必须建立关联。

例如：

Gate Driver

↓

TFT Array

↓

Bad Row

↓

Row Banding

↓

Troubleshooting SOP

---

## 2.4 Single Source of Truth

每个知识点只能存在一个正式定义。

其它文档采用引用方式，不重复描述。

例如：

Gate Driver 的定义

只能存在：

03_Hardware/Gate_Driver

其它文档引用即可。

---

# 3. Object Type

整个知识系统采用以下 Object 分类。

---

## Product

表示产品型号。

例如：

Mercu1717V

Mercu1212X

Mars1717X

Jupi1212X

Venu1717X

---

## System

表示系统级知识。

例如：

Detector Architecture

Signal Flow

Image Pipeline

Communication

Power Architecture

---

## Hardware

表示硬件模块。

例如：

Scintillator

Photodiode

TFT Array

Gate Driver

Readout ASIC

ADC

FPGA

DDR

WiFi

Battery

Power Board

---

## Software

表示软件模块。

例如：

Home

Acquire

Detector

Calibrate

SDK

Settings

Log

Upgrade

---

## Workflow

表示工程流程。

例如：

Installation

Activation

Connection

Configuration

Acquisition

Calibration

Acceptance

Maintenance

---

## Calibration

表示校准对象。

例如：

Offset

Gain

Defect

Template

Calibration Theory

---

## Failure

表示故障对象。

例如：

Connection Failure

Exposure Failure

Image Failure

Calibration Failure

Power Failure

Network Failure

Software Failure

Hardware Failure

---

## Image Artifact

表示图像异常。

例如：

Dead Pixel

Bad Pixel

Bad Row

Bad Column

Banding

Ghost

Lag

Noise

NonUniformity

---

## SOP

表示标准操作流程。

例如：

Installation SOP

Calibration SOP

Maintenance SOP

Upgrade SOP

Troubleshooting SOP

---

## Case

表示现场案例。

例如：

Case001

Case002

Case003

---

## Error Code

表示错误代码。

例如：

E1001

E2003

Timeout

Detector Disconnect

---

## Parameter

表示参数。

例如：

Exposure Time

Frame Rate

Trigger Mode

Gain

Offset

Temperature

Battery Level

IP Address

MAC Address

---

## Document

表示厂家文档。

例如：

User Manual

Service Manual

SDK Manual

Release Note

Specification

---

# 4. Object Metadata

每个 Object 必须包含以下 Metadata。

Name

Type

Description

Version

Status

Applicable Product

Related Object

Reference Document

Keywords

Last Update

---

# 5. Object Relationship

Object 之间允许建立以下关系。

Depends On

Part Of

Contains

Uses

Controls

Produces

Causes

References

Related To

Resolved By

Verified By

---

# 6. Relationship Example

Gate Driver

Depends On

↓

FPGA

Controls

↓

TFT Array

Causes

↓

Bad Row

Related To

↓

Banding

Resolved By

↓

Gate Driver Troubleshooting SOP

Verified By

↓

Case023

---

# 7. Knowledge Hierarchy

Object

↓

Relationship

↓

Document

↓

Workflow

↓

Failure

↓

Decision Tree

↓

Case

---

# 8. Future Extension

后续可增加新的 Object Type，例如：

Firmware

Driver

SDK API

Communication Protocol

Image Algorithm

Test Tool

Production

QA

Service Record

Training Course

---

# 9. Naming Rule

Object Name 使用统一英文名称。

例如：

Gate_Driver

Readout_ASIC

PowerBoard

DeadPixel

BadRow

Offset

Gain

ConnectionFailure

InstallationSOP

Case001

---

# 10. Notes

Object Model 是整个知识系统最高层规范。

所有 Markdown 文档、Drawio 架构图、Decision Tree、SOP、Case 都必须符合本规范。

未经 Object Model 定义的对象，不允许直接加入知识系统。