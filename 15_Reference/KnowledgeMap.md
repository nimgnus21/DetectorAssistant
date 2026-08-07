# DetectorAssistant Knowledge Map

> Version: v1.0

---

# Knowledge Architecture

```
Customer Problem
        │
        ▼
11_Case
        │
        ▼
09_DecisionTree
        │
        ▼
08_ImageDiagnosis
        │
        ▼
07_FailureKnowledge
        │
        ▼
05_Calibration
        │
        ▼
03_Hardware
        │
        ▼
02_System
```

---

# Knowledge Flow

```
Customer Question

↓

Case

↓

Decision Tree

↓

Failure Knowledge

↓

Workflow

↓

Tool

↓

Reference

↓

Official Manual
```

---

# Engineering Workflow

```
Image

↓

Symptom

↓

Diagnosis

↓

Root Cause

↓

Solution

↓

Verification

↓

Experience

↓

Reply
```

---

# Module Dependency

## Image

Depends on

- Calibration
- Hardware
- Workflow
- SDK

---

## Calibration

Depends on

- Firmware
- SDK
- Detector Hardware

---

## SDK

Depends on

- Firmware
- Configuration
- Network

---

## Workflow

Depends on

- Tool
- SOP
- Case

---

# Knowledge Update Flow

```
Customer Case

↓

Field Experience

↓

Case

↓

Decision Tree

↓

Workflow

↓

Failure Knowledge

↓

FAQ

↓

Reply Template
```

---

# Knowledge Source

```
Official Manual

↓

Training

↓

FAE

↓

Project

↓

Customer

↓

DetectorAssistant
```

---

# Maintenance Principle

The DetectorAssistant knowledge base follows a layered architecture.

Layer 1

Customer Cases

↓

Layer 2

Engineering Diagnosis

↓

Layer 3

Engineering Knowledge

↓

Layer 4

Engineering Workflow

↓

Layer 5

Engineering Tools

↓

Layer 6

Official References

Each layer has a clear responsibility and should avoid duplication of content.