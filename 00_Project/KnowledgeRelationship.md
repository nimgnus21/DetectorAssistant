# Detector Assistant Knowledge Relationship

Version: V1.0

---

# 一、系统总体关系

```
Detector
│
├── Product
│
├── System
│      │
│      ├── Detector Architecture
│      ├── Signal Flow
│      ├── Image Pipeline
│      ├── Communication
│      └── Power Architecture
│
├── Hardware
│      │
│      ├── Scintillator
│      ├── TFT Array
│      ├── Gate Driver
│      ├── Readout ASIC
│      ├── ADC
│      ├── FPGA
│      ├── DDR
│      ├── WiFi
│      ├── Battery
│      └── Power Board
│
├── Software
│      │
│      ├── Home
│      ├── Detector
│      ├── Acquire
│      ├── Calibrate
│      ├── SDK
│      ├── Settings
│      ├── Log
│      └── Upgrade
│
├── Calibration
│      │
│      ├── Offset
│      ├── Gain
│      ├── Defect
│      └── Template
│
├── Workflow
│
├── Failure
│
├── Image Artifact
│
├── SOP
│
└── Case
```

---

# 二、知识依赖关系

Detector Architecture

↓

Signal Flow

↓

Hardware

↓

Software

↓

Calibration

↓

Workflow

↓

Failure

↓

Decision Tree

↓

SOP

↓

Case

---

# 三、AI推理顺序

Customer Problem

↓

Workflow

↓

Failure Classification

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

# 四、文档引用规则

System
    ↑
Hardware
    ↑
Software
    ↑
Calibration
    ↑
Workflow
    ↑
Failure
    ↑
Decision Tree
    ↑
SOP
    ↑
Case
