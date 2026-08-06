# EMIFailure

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
- VibrationFailure.md
- PowerQualityFailure.md
- ../HardwareFailure/CommunicationFailure.md
- ../HardwareFailure/FPGAFailure.md
- ../HardwareFailure/ADCFailure.md
- ../ImageFailure/NoiseArtifact.md
- ../ImageFailure/ImageLoss.md
- ../../06_Workflow/ImageTransmissionWorkflow.md
- ../../09_DecisionTree/

---

# 1. Purpose

EMI Failure 描述数字平板探测器（Flat Panel Detector，FPD）由于电磁干扰（Electromagnetic Interference, EMI）导致的系统异常，包括通信错误、图像噪声、数据丢失、设备重启及系统运行不稳定等故障。

Detector 内部包含高灵敏度模拟电路、高速数字电路及无线/有线通信模块，当受到外部或内部电磁干扰时，可能导致图像质量下降甚至设备无法正常工作。

本文件回答的问题：

> **为什么 Detector 在特定环境下才出现异常？为什么靠近某些设备时图像出现噪声或通信异常？**

---

# 2. Scope

适用于：

- EMC Test
- EMI Verification
- Factory Test
- Field Service
- Technical Support

适用于：

- Conducted EMI
- Radiated EMI
- Electrostatic Discharge (ESD)
- High Frequency Interference
- Magnetic Field Interference

---

# 3. What is EMI Failure

EMI Failure 指：

**由于外部或内部电磁干扰影响 Detector 正常工作，导致模拟信号、数字信号或通信链路受到干扰，从而产生系统异常。**

主要表现：

- Random Noise
- Communication Error
- Image Loss
- Detector Restart
- FPGA Reset
- Calibration Failure
- Random Failure

---

# 4. Failure Classification

```text
EMI Failure

├── Conducted EMI
├── Radiated EMI
├── Electrostatic Discharge (ESD)
├── RF Interference
├── Magnetic Field Interference
└── Internal EMI
```

---

# 5. Typical Symptoms

## 5.1 Conducted EMI

特点：

- 电源接入后故障出现
- 多设备同时异常

可能原因：

- 电源线路干扰
- 接地不良

---

## 5.2 Radiated EMI

特点：

- 靠近大型设备时异常
- 更换位置后恢复正常

可能原因：

- 高频辐射
- 工业设备
- 高频电机

---

## 5.3 Electrostatic Discharge (ESD)

特点：

- 人员接触后设备异常
- 瞬间死机或重启

可能原因：

- 静电放电
- 接地不足

---

## 5.4 RF Interference

特点：

- 无线通信不稳定
- 数据包丢失

可能原因：

- Wi-Fi
- Bluetooth
- RFID
- 无线电设备

---

## 5.5 Magnetic Field Interference

特点：

- 图像周期性异常
- 通信偶发中断

可能原因：

- MRI
- 大功率变压器
- 电机

---

## 5.6 Internal EMI

特点：

- 高负载运行时异常
- 故障具有规律性

可能原因：

- FPGA
- DC/DC Converter
- Clock Circuit

---

# 6. Typical Root Causes

| Failure | Possible Root Cause |
|----------|---------------------|
| Random Noise | Radiated EMI |
| Image Loss | Communication Interference |
| Detector Restart | ESD |
| Communication Failure | RF Interference |
| Calibration Failure | Internal EMI |
| FPGA Reset | Power EMI |

---

# 7. Relationship with Hardware

| Hardware Module | Typical Symptom |
|-----------------|-----------------|
| FPGA | Reset / Logic Error |
| ADC | Noise Increase |
| Communication Board | Packet Loss |
| Main Board | Clock Disturbance |
| Power Module | Conducted EMI |

---

# 8. Relationship with Software

| Software Module | Typical Symptom |
|-----------------|-----------------|
| Firmware | Unexpected Reset |
| Driver | Communication Timeout |
| SDK | Data Reception Failure |
| Communication Service | Packet Retry |

---

# 9. Relationship with Image Failure

EMI Failure 可导致：

- Noise Artifact
- Line Artifact
- Image Loss
- Image Distortion
- Random Pixel Noise

---

# 10. Diagnostic Workflow

```text
Random Failure

↓

Occurs Only in Specific Environment？

↓

YES

↓

Remove EMI Source

↓

Recovered？

↓

YES

↓

EMI Failure

↓

NO

↓

Check Grounding

↓

Check Shielding

↓

Hardware Analysis
```

---

# 11. Detection Methods

## Environmental Investigation

检查：

- 是否靠近 MRI
- 是否靠近高频设备
- 是否靠近大型电机

---

## EMI Isolation Test

关闭：

- Wi-Fi
- Bluetooth
- Radio Device
- Industrial Equipment

观察故障是否消失。

---

## Ground Verification

检查：

- Ground Resistance
- Protective Earth
- Shield Ground

---

## Shield Inspection

检查：

- Shield Cable
- Shield Cover
- Shield Connection

---

## EMC Test

进行：

- Conducted Immunity Test
- Radiated Immunity Test
- ESD Test

验证 Detector EMC 性能。

---

# 12. Common Failure Scenarios

| Scenario | Description |
|----------|-------------|
| Noise Near MRI Room | Magnetic Interference |
| Communication Lost Near Motor | EMI |
| Detector Restarts After ESD | Static Discharge |
| Image Noise During RF Transmission | RF Interference |
| Random Failure in Factory | Industrial EMI |
| Calibration Occasionally Fails | Internal EMI |

---

# 13. Engineering Recommendations

建议：

- 确保 Detector 按 EMC 要求正确接地。
- 避免与大功率电机、变频器、MRI 等强干扰源距离过近。
- 定期检查屏蔽层及接地连接状态。
- 使用屏蔽网线或符合规范的通信线缆。
- ESD 敏感区域应采取静电防护措施。
- 使用 DecisionTree 完成最终 Root Cause Analysis。

---

# 14. Relationship with Other Modules

## CommunicationFailure

EMI 是通信异常的重要外部原因。

---

## NoiseArtifact

EMI 可直接导致随机噪声及条纹噪声。

---

## PowerQualityFailure

传导干扰通常与供电质量密切相关。

---

## FPGAFailure

强电磁干扰可能导致 FPGA 异常复位。

---

## DecisionTree

EMI Failure 是环境故障诊断的重要分析节点。

---

# 15. Knowledge Graph

```text
EMI Failure

├── Conducted EMI
├── Radiated EMI
├── ESD
├── RF Interference
├── Magnetic Interference
└── Internal EMI

↓

Environment Verification

↓

Ground Verification

↓

Shield Verification

↓

Hardware Analysis

├── FPGA
├── ADC
├── Communication
├── Main Board
└── Power

↓

Root Cause Analysis

↓

DecisionTree
```

---

# 16. Summary

EMI Failure 是 Flat Panel Detector 现场应用中常见的环境类故障，主要包括传导干扰、辐射干扰、静电放电、射频干扰、磁场干扰及设备内部电磁干扰。其典型表现为随机噪声、通信异常、图像丢失、系统重启及间歇性故障。通过环境调查、EMI 隔离测试、接地检查、屏蔽检查及 EMC 验证，可快速判断电磁干扰是否为故障根因，并结合 Hardware Failure、Image Failure、Power Quality Failure 与 DecisionTree 建立完整的 EMI 故障分析体系。