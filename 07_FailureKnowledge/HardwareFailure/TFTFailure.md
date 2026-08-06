# TFTFailure

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- README.md
- PhotodiodeFailure.md
- GateDriverFailure.md
- ../../03_Hardware/TFT.md
- ../../06_Workflow/AcquisitionWorkflow.md
- ../../06_Workflow/ReadoutWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

TFT Failure 描述数字平板探测器（Flat Panel Detector，FPD）中 Thin Film Transistor（TFT）阵列的典型故障模式、形成机理、图像表现、检测方法及根因分析。

TFT 是 Flat Panel Detector 每个 Pixel 的电子开关，其主要作用是在 Gate Driver 控制下，将 Photodiode 积累的电荷连接至 Data Line，由 Readout ASIC 完成读出。

TFT 的工作状态直接决定 Detector 是否能够正确完成电荷保持（Charge Storage）与电荷读出（Charge Readout），因此是影响图像质量最重要的硬件之一。

本文件回答的问题：

> **TFT 为什么会发生故障？故障后会导致哪些图像异常？**

---

# 2. Scope

适用于：

- a-Si Flat Panel Detector
- Wired Detector
- Wireless Detector
- Factory Test
- Engineering Debug
- Field Service

适用于所有 TFT Array 相关故障分析。

---

# 3. TFT Overview

TFT（Thin Film Transistor）位于每一个 Pixel 内。

主要职责：

- 控制 Pixel Charge 是否输出
- 保持曝光期间电荷
- 在 Gate Pulse 到来时导通
- 将 Pixel Charge 输出到 Data Line

工作过程：

```text
X-ray

↓

Scintillator

↓

Photodiode

↓

Charge Storage

↓

Gate Pulse

↓

TFT ON

↓

Data Line

↓

Readout ASIC
```

正常情况下：

- Gate=OFF
  - Charge Storage
  - Pixel Isolation

- Gate=ON
  - Charge Readout
  - Pixel Reset

---

# 4. Failure Modes

TFT 常见故障模式如下：

| Failure Mode | Description |
|--------------|-------------|
| Open Circuit | TFT 开路 |
| Short Circuit | TFT 短路 |
| Gate Leakage | 栅极漏电 |
| Drain Leakage | 漏极漏电 |
| Source Leakage | 源极漏电 |
| Threshold Voltage Shift | 阈值漂移 |
| Switching Failure | 无法导通或关断 |
| Charge Retention Failure | 电荷保持能力下降 |
| Aging | 老化 |
| Radiation Damage | 辐射损伤 |

---

# 5. Failure Mechanisms

## 5.1 Open Circuit

TFT 无法导通。

影响：

- Charge 无法输出
- Pixel 永久失效

典型表现：

- Dead Pixel
- Dark Pixel

---

## 5.2 Short Circuit

TFT 长期保持导通。

影响：

- Charge 无法存储
- Pixel 持续放电

典型表现：

- Bright Pixel
- Pixel Saturation
- Fixed Response

---

## 5.3 Leakage

TFT OFF 状态仍存在漏电。

影响：

- Charge Loss
- Offset Drift
- SNR 降低

典型表现：

- Image Noise
- Uniformity Degradation

---

## 5.4 Threshold Voltage Shift

长期工作导致 TFT Threshold Voltage 漂移。

影响：

- 导通时间改变
- 输出幅度变化

典型表现：

- Gain Drift
- Pixel Response Difference

---

## 5.5 Switching Failure

TFT 导通速度下降或无法完全导通。

影响：

- Readout Incomplete
- Charge Transfer Efficiency 降低

典型表现：

- Image Brightness Difference
- Line Artifact

---

## 5.6 Charge Retention Failure

Pixel 无法保持曝光期间积累的 Charge。

影响：

- Charge Decay
- Signal Loss

典型表现：

- Low Signal
- Dark Area
- Low Contrast

---

## 5.7 Aging

长期工作导致 TFT 参数退化。

包括：

- Mobility 降低
- Threshold Shift
- Leakage Increase

属于渐进式故障。

---

## 5.8 Radiation Damage

长期高剂量 X-ray 辐照导致 TFT 特性变化。

影响：

- Leakage Increase
- Threshold Drift
- Pixel Instability

---

# 6. Typical Image Symptoms

| Image Symptom | Possible TFT Failure |
|---------------|----------------------|
| Dead Pixel | Open Circuit |
| Bright Pixel | Short Circuit |
| Cluster Defect | Local TFT Damage |
| Horizontal Line | Gate Related / TFT Row |
| Vertical Line | Data Line Related |
| Image Noise | Leakage |
| Uniformity Failure | Threshold Drift |
| Image Lag | Charge Retention Failure |
| Bright/Dark Area | Local TFT Failure |

说明：

上述症状并非 TFT 独有，应结合 Gate Driver、Readout ASIC 及 Calibration 综合分析。

---

# 7. Failure Impact

TFT Failure 对系统的影响：

| Module | Impact |
|---------|--------|
| Acquisition | Charge Readout 异常 |
| Readout | Pixel Data 错误 |
| Calibration | Gain / Defect 校正受影响 |
| Image Generation | 图像质量下降 |
| Clinical Diagnosis | 图像可靠性下降 |

---

# 8. Detection Methods

推荐检测方法：

## Offset Image

检查：

- Dead Pixel
- Bright Pixel
- Fixed Pattern

---

## Gain Image

检查：

- Pixel Response
- Uniformity

---

## Defect Map

观察：

- Pixel 数量变化
- Cluster 增长趋势

---

## Long Exposure Test

观察：

- Charge Leakage
- Image Lag
- Response Stability

---

## Electrical Verification

建议检查：

- Gate Voltage
- TFT Switching Timing
- Data Line Signal
- Leakage Current

---

# 9. Root Cause Analysis

推荐分析流程：

```text
Image Abnormal

↓

Single Pixel ?

├── YES

│      ↓

│   Dead Pixel ?

│      ↓

│   Check Offset

│      ↓

│   Check Gain

│      ↓

│   Exclude Photodiode

│      ↓

│   Confirm TFT

└── NO

       ↓

Row / Column ?

       ↓

Check Gate Driver

↓

Check Readout ASIC
```

---

# 10. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Manufacturing Defect | TFT 制造缺陷 |
| Aging | 长期使用老化 |
| Radiation Damage | 高剂量照射 |
| Leakage Increase | 漏电增加 |
| Process Variation | 工艺偏差 |
| Pixel Drift | 参数漂移 |

---

# 11. Failure Severity

| Level | Description |
|-------|-------------|
| Minor | 少量 Pixel 异常 |
| Moderate | Cluster Defect |
| Major | 大面积 TFT 异常 |
| Critical | Detector 无法正常采集 |

---

# 12. Engineering Recommendations

建议：

- 定期统计 Dead Pixel 与 Bright Pixel 数量。
- 定期更新 Defect Template。
- 长期监测 Pixel Response Drift。
- 对异常 Detector 建立趋势分析。
- 在确认 TFT 故障前，应排除 Photodiode、Gate Driver、Readout ASIC 及 Calibration 的影响。

---

# 13. Relationship with Other Modules

## PhotodiodeFailure

Photodiode 负责产生 Charge。

TFT 负责控制 Charge 输出。

---

## GateDriverFailure

Gate Driver 控制 TFT 导通。

若 Gate Driver 异常，可表现为整行 TFT 不工作。

---

## ReadoutASICFailure

Readout ASIC 负责接收 TFT 输出的数据。

应区分：

- Pixel Failure（TFT）
- Readout Failure（ASIC）

---

## Calibration

TFT 漂移可能影响：

- Gain Calibration
- Defect Calibration
- Uniformity

---

## DecisionTree

TFT Failure 是以下诊断的重要节点：

- Dead Pixel
- Bright Pixel
- Cluster Defect
- Image Lag
- Uniformity
- Noise

---

# 14. Knowledge Graph

```text
Photodiode

↓

Charge Storage

↓

TFT

├── Open
├── Short
├── Leakage
├── Threshold Drift
├── Switching Failure
├── Charge Retention Failure
├── Aging
└── Radiation Damage

↓

Data Line

↓

Readout ASIC

↓

Image Symptoms

↓

Failure Analysis

↓

DecisionTree
```

---

# 15. Summary

TFT Failure 是 Flat Panel Detector 最关键的硬件故障之一，其主要表现为开路、短路、漏电、阈值漂移、开关异常及电荷保持能力下降。由于 TFT 位于 Pixel 电荷读出的核心位置，其故障通常表现为 Dead Pixel、Bright Pixel、Cluster Defect、Noise、Uniformity 异常及 Image Lag 等图像问题。故障分析应结合 Offset、Gain、Defect Template、Gate Driver、Readout ASIC 及 Workflow 进行综合判断，确保准确定位根因，并为 DecisionTree 和 Service 提供可靠的理论依据。