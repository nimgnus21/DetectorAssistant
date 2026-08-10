# ConfigurationWorkflow

Version: V1.1

Module: Workflow

Status: Released

Source Level:

- Engineering
- Firmware
- SDK
- FPGA

Applicable Product:

- Static Detector
- Dynamic Detector
- Wired Detector
- Wireless Detector

Related Documents:

- InitializationWorkflow.md
- ConnectionWorkflow.md
- TimingWorkflow.md
- ModeWorkflow.md
- DynamicAcquisitionWorkflow.md
- CalibrationWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- ImageGenerationWorkflow.md
- ../17_Tools/SDKTool/ModeConfiguration.md

---

# 1. Purpose

Configuration Workflow 描述探测器（Flat Panel Detector，FPD）在开始图像采集之前，各类运行参数的配置、加载、验证及生效流程。

Detector 的所有采集行为均依赖于正确的配置，包括：

- Detector Configuration
- Firmware Configuration
- SDK Configuration
- Acquisition Parameters
- Calibration Template
- Communication Parameters

Configuration Workflow 的目标是确保 Detector 在进入 Ready 状态之前，所有配置均已正确加载并完成一致性验证。

---

# 2. Scope

适用于：

- Detector Initialization
- Detector Configuration
- Dynamic Detector
- Static Detector
- Factory Calibration
- Clinical Acquisition
- SDK Development
- Firmware Development
- FAE
- Technical Support

---

# 3. Configuration Workflow Overview

Detector 配置流程如下：

```text
Power On
↓
Detector Initialization
↓
Read Hardware Information
↓
Load Configuration
↓
Load Mode
↓
Load Calibration Templates
↓
Verify Configuration
↓
Initialize Runtime Parameters
↓
Detector Ready
```

只有 Configuration Verification 成功后，Detector 才允许进入采集状态。

---

# 4. Configuration Architecture

Detector Configuration 主要由以下几部分组成：

```text
Configuration
├── Detector Information
├── Hardware Configuration
├── Firmware Configuration
├── SDK Configuration
├── Acquisition Configuration
├── Calibration Configuration
├── Communication Configuration
├── Runtime Configuration
└── Diagnostic Configuration
```

---

# 5. Detector Configuration

主要读取 Detector 基本信息：

- Detector Model
- Serial Number
- Detector Type
- Hardware Revision
- Firmware Version
- FPGA Version
- MAC Address

验证内容：

- 型号是否匹配
- Firmware 是否兼容
- FPGA 是否兼容

---

# 6. Mode Configuration

Mode 决定 Detector 工作方式。

典型参数：

- Acquisition Mode
- Trigger Mode
- Exposure Mode
- Readout Mode
- Frame Rate
- Dynamic Mode
- Swap Mode

Mode 加载完成后进入 Runtime Configuration。

当出现 Mode 无法加载、特定采集模式失败、ROI / Frame Rate / Trigger 配置异常、Mode 与 Calibration 不匹配等问题时，使用 [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md) 作为参数检查与配置恢复入口。

---

# 7. ROI Configuration

ROI（Region of Interest）决定采集区域。

主要参数：

- Width
- Height
- Start X
- Start Y

工程要求：

- ROI 最小尺寸应符合产品规格要求。
- ROI Width 应满足硬件对齐要求。
- ROI Height 应满足硬件对齐要求。
- ROI 不得超出 Detector 有效成像区域。

> **工程经验（来源于培训笔记）**
>
> 对于当前动态平板平台：
>
> - 推荐最小 ROI：256 × 256
> - ROI Width 为 8 的整数倍
> - ROI Height 为 8 的整数倍
>
> 实际限制应以当前 Firmware、SDK 及硬件平台规格为准。

---

# 8. Frame Rate Configuration

Frame Rate 决定动态图采集速度。

主要参数：

- Target FPS
- Maximum FPS
- Exposure Time
- Readout Time

配置要求：

Frame Period 必须满足：

```text
Frame Period
≥
Exposure Time
+
Readout Time
+
Processing Time
```

否则可能导致：

- Image Loss
- Frame Drop
- Timeout

参数检查可参考 [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md) 中的 Frame Rate、Readout 和 Trigger 配置项。

---

# 9. Trigger Configuration

支持：

- Internal Trigger
- External Trigger
- Software Trigger
- Hardware Trigger

主要配置：

- Trigger Source
- Trigger Edge
- Trigger Delay
- Trigger Timeout

配置错误可能导致：

- Detector No Response
- Exposure Failure
- Timeout

涉及 Mode 参数时使用 [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md) 复核 Trigger 与当前 Mode 的一致性。

---

# 10. Exposure Configuration

主要参数：

- Exposure Mode
- Enable Time
- Integration Time
- Pulse Width
- Trigger Delay

要求：

Exposure Window 必须与当前 Mode 保持一致。

---

# 11. PGA Configuration

PGA（Programmable Gain Amplifier）决定模拟信号放大倍数。

配置内容：

- Gain Level
- Analog Gain
- Digital Gain

注意：

不同 PGA 通常对应不同 Calibration Template。

---

# 12. Calibration Configuration

加载：

- Offset Template
- Gain Template
- Defect Template

动态模式还可能包括：

- Ghost Correction Parameters
- Lag Correction Parameters
- Swap Parameters

模板必须与当前配置一致。

---

# 13. Communication Configuration

根据产品类型加载：

## Wired Detector

- IP Address
- Subnet Mask
- Gateway
- Jumbo Frame
- MTU
- Packet Size

## Wireless Detector

- AP Mode
- STA Mode
- SSID
- Channel
- Security

配置异常可能导致：

- Detector Offline
- Image Loss
- Communication Timeout

---

# 14. Runtime Configuration

运行阶段初始化：

- Buffer
- Memory
- Queue
- Thread
- DMA
- FPGA Buffer

完成后：

Detector 进入 Ready 状态。

---

# 15. Configuration Verification

配置完成后执行一致性验证。

主要检查：

✓ Detector Model
✓ Firmware Version
✓ FPGA Version
✓ SDK Compatibility
✓ Mode
✓ ROI
✓ Frame Rate
✓ Trigger
✓ Calibration Template
✓ Communication Parameters

任何一项失败均应终止采集流程。

Mode、ROI、Frame Rate 或 Trigger 无法确认时，回到 [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md) 完成参数复核，再重新验证 Configuration。

---

# 16. Engineering Notes

## Firmware Version

升级 Firmware 前必须保存：

- Factory Parameters
- Calibration Parameters
- Detector Configuration

升级完成后：

- 重新上电
- 验证 Firmware Version
- 验证 Configuration 是否恢复正常

---

## Calibration Template

只有满足以下条件时，可共用 Gain / Defect Template：

- Detector 相同
- ROI 相同
- PGA 相同
- Binning 相同

否则应重新生成模板。

---

## Dynamic Configuration

动态模式除基础参数外，还需配置：

- Mode
- Frame Rate
- Trigger
- Swap
- Ghost Correction
- Lag Correction

涉及具体 Mode 参数检查时使用 [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md)。

---

# 17. Common Configuration Errors

| Error | Possible Cause |
|--------|----------------|
| Detector Offline | Network Configuration Error |
| Image Loss | Frame Rate Too High |
| Timeout | Trigger Configuration Error |
| Wrong Brightness | Gain Configuration Error |
| Calibration Failed | Template Mismatch |
| Mode Error | Unsupported Mode |
| Ghost Artifact | Dynamic Correction Configuration Error |

---

# 18. Configuration Checklist

开始采集前建议确认：

- □ Detector Online
- □ Firmware Version 正确
- □ FPGA Version 正确
- □ SDK Version 匹配
- □ Mode 正确
- □ ROI 正确
- □ Frame Rate 正确
- □ Trigger 正确
- □ Offset Template 正确
- □ Gain Template 正确
- □ Defect Template 正确
- □ Communication 正常

全部通过后方可开始图像采集。

---

# 19. Related Documents

- InitializationWorkflow.md
- ConnectionWorkflow.md
- TimingWorkflow.md
- ModeWorkflow.md
- DynamicAcquisitionWorkflow.md
- DynamicCorrectionWorkflow.md
- CalibrationWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- ImageGenerationWorkflow.md
- [Mode Configuration Tool](../17_Tools/SDKTool/ModeConfiguration.md)

---

# 20. Summary

Configuration Workflow 是 Detector 进入采集状态前最重要的准备流程，负责完成硬件识别、Firmware 初始化、Mode 加载、ROI 配置、Frame Rate 配置、Calibration Template 加载、通信参数配置及一致性验证。`ModeConfiguration.md` 已作为具体配置工具接入 Mode、ROI、Frame Rate、Trigger 与动态参数复核，用于在配置异常时提供可执行的反向入口。

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.1 | 2026-08-10 | Linked Mode Configuration Tool to configuration verification and troubleshooting |
| V1.0 | 2026-08 | Initial release |