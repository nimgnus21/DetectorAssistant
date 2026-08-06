# VibrationFailure

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
- TemperatureFailure.md
- HumidityFailure.md
- EMIFailure.md
- PowerQualityFailure.md
- ../HardwareFailure/MainBoardFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../HardwareFailure/TFTFailure.md
- ../ImageFailure/LineArtifact.md
- ../ImageFailure/ImageLoss.md
- ../../06_Workflow/StartupWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

Vibration Failure 描述数字平板探测器（Flat Panel Detector，FPD）由于运输、安装、跌落、机械振动或持续冲击导致的各种故障，包括连接器松动、PCB 损伤、焊点开裂、结构变形及图像异常等问题。

Detector 属于高精密医疗设备，其内部包含 TFT 面板、Scintillator、Photodiode、ASIC、FPGA 及多种精密连接器。机械冲击或长期振动可能导致设备性能下降，甚至引起永久性硬件损坏。

本文件回答的问题：

> **为什么 Detector 在运输或跌落后出现间歇性故障？为什么轻微敲击设备会导致图像或通信异常？**

---

# 2. Scope

适用于：

- Factory Test
- Transportation Verification
- Installation Inspection
- Reliability Test
- Technical Support
- Field Service

适用于：

- Transportation Vibration
- Mechanical Shock
- Drop Impact
- Installation Vibration
- Continuous Mechanical Stress

---

# 3. What is Vibration Failure

Vibration Failure 指：

**由于外部机械应力导致 Detector 内部结构、电路连接或器件受到影响，从而产生系统异常或图像异常。**

主要表现：

- Detector Offline
- Random Restart
- Communication Error
- Intermittent Failure
- Image Artifact
- Loose Connector
- Hardware Damage

---

# 4. Failure Classification

```text
Vibration Failure

├── Transportation Damage
├── Drop Impact
├── Continuous Vibration
├── Connector Loosening
├── PCB Mechanical Damage
├── Solder Joint Crack
└── Internal Structural Damage
```

---

# 5. Typical Symptoms

## 5.1 Transportation Damage

特点：

- 运输后首次开机异常
- 包装存在撞击痕迹

可能原因：

- Internal Mechanical Damage
- Connector Displacement

---

## 5.2 Drop Impact

特点：

- 跌落后立即发生故障
- 图像或通信异常

可能原因：

- PCB Crack
- TFT Damage
- Housing Deformation

---

## 5.3 Continuous Vibration

特点：

- 振动环境下故障频繁
- 停止振动后恢复正常

可能原因：

- Connector Loosening
- Cable Fatigue

---

## 5.4 Connector Loosening

特点：

- 间歇性通信异常
- 重新插拔后恢复

可能原因：

- Connector Not Fully Seated
- Lock Mechanism Failure

---

## 5.5 PCB Mechanical Damage

特点：

- 无法启动
- 随机重启
- 局部功能失效

可能原因：

- PCB Crack
- Copper Trace Damage

---

## 5.6 Solder Joint Crack

特点：

- 故障具有随机性
- 按压设备时故障变化

可能原因：

- BGA Solder Crack
- Cold Solder Joint
- Fatigue Failure

---

## 5.7 Internal Structural Damage

特点：

- 图像局部异常
- 长期无法恢复

可能原因：

- Scintillator Damage
- TFT Panel Damage
- Mechanical Deformation

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Transportation Failure | Shipping Shock |
| Drop Damage | Mechanical Impact |
| Communication Failure | Loose Connector |
| Random Restart | PCB Crack |
| Image Artifact | Internal Structural Damage |
| Intermittent Failure | Solder Joint Crack |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| Main Board | PCB Crack |
| Communication Board | Connector Failure |
| TFT Panel | Panel Damage |
| FPGA | BGA Solder Crack |
| Power Module | Loose Connector |

---

# 8. Relationship with Image Failure

Vibration Failure 可导致：

- Line Artifact
- Noise Artifact
- Image Loss
- Bad Pixel Artifact
- Image Distortion

---

# 9. Relationship with Calibration

机械冲击可能导致：

- Offset Drift
- Gain Drift
- Calibration Failure

发生跌落或维修后，应重新验证 Calibration。

---

# 10. Diagnostic Workflow

```text
Failure After Transportation？

↓

YES

↓

Visual Inspection

↓

Connector Inspection

↓

Image Test

↓

Mechanical Damage？

↓

YES

↓

Repair / Replace

↓

NO

↓

Repeat Test

↓

Still Failed？

↓

Hardware Analysis
```

---

# 11. Detection Methods

## Appearance Inspection

检查：

- 外壳裂纹
- 变形
- 碰撞痕迹

---

## Connector Inspection

检查：

- 是否松动
- 是否脱落
- 是否损坏

---

## PCB Inspection

检查：

- 裂纹
- 焊点
- 元件松动

---

## Functional Test

执行：

- Startup Test
- Communication Test
- Image Acquisition Test

验证设备功能。

---

## Vibration Reproduction Test

模拟：

- 轻微振动
- 轻敲设备

观察故障是否复现。

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Detector Fails After Shipping | Transportation Damage |
| Communication Restored After Reconnecting Cable | Connector Loosening |
| Random Restart After Drop | PCB Damage |
| Image Abnormal After Impact | TFT / Scintillator Damage |
| Failure Changes When Device Is Pressed | Solder Joint Crack |
| Intermittent Failure During Mobile Use | Continuous Vibration |

---

# 13. Engineering Recommendations

建议：

- 搬运和运输过程中使用符合规范的防震包装。
- 安装完成后检查所有连接器锁止状态。
- 跌落后禁止直接投入临床使用，应完成全面功能检查。
- 出现随机故障时，检查是否存在虚焊或连接器松动。
- 更换硬件后重新执行 Calibration。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## MainBoardFailure

PCB 裂纹可能导致主板故障。

---

## CommunicationFailure

连接器松动是通信异常的重要原因。

---

## TFTFailure

机械冲击可能损坏 TFT Panel。

---

## CalibrationFailure

硬件位置变化可能影响 Calibration 结果。

---

## DecisionTree

Vibration Failure 是运输及安装故障的重要诊断入口。

---

# 15. Knowledge Graph

```text
Vibration Failure

├── Transportation Damage
├── Drop Impact
├── Continuous Vibration
├── Connector Loosening
├── PCB Damage
├── Solder Joint Crack
└── Structural Damage

↓

Mechanical Inspection

↓

Connector Inspection

↓

Functional Verification

↓

Hardware Analysis

├── Main Board
├── TFT
├── FPGA
├── Communication
└── Power

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

Vibration Failure 是 Flat Panel Detector 在运输、安装及现场使用过程中常见的环境类故障，主要由运输冲击、跌落、持续振动、连接器松动、PCB 裂纹及焊点疲劳等因素引起。典型表现包括通信异常、随机重启、图像伪影、间歇性故障及硬件损坏。通过外观检查、连接器检查、PCB 检查、功能验证及振动复现测试，可快速确认机械因素是否为故障根因，并结合 Hardware Failure、Calibration Failure 与 DecisionTree 建立完整的机械环境故障分析体系。