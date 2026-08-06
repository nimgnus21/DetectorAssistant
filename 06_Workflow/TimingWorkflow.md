# TimingWorkflow

Version: V1.0

Module: Workflow

Status: Released

---

# 1. Purpose

Timing Workflow 用于描述动态平板（Dynamic Flat Panel Detector）在一次图像采集过程中，各控制信号、曝光窗口及图像读出的完整时序关系。

本章节用于理解：

- Trigger 如何启动采集
- Enable 如何控制曝光窗口
- X-Ray 在何时照射
- Detector 在何时 Readout
- Frame 如何连续采集
- 不同 Mode 的 Timing 如何变化

---

# 2. Scope

适用于：

- Dynamic Detector
- Static Detector（部分适用）
- Pulsed Acquisition
- Continuous Acquisition

适用于：

- FPGA 开发
- Firmware 开发
- SDK 开发
- FAE
- 售后分析

---

# 3. Timing Overview

一个完整采集周期主要包含以下阶段：

```text
Trigger

↓

Preparation

↓

Enable

↓

Exposure

↓

Readout

↓

Image Generation

↓

Transmission

↓

Next Frame
```

---

# 4. Signal Timing

主要涉及以下信号：

| Signal | Description |
|---------|-------------|
| Acquire Cmd | SDK开始采集命令 |
| Sync In | 外部同步输入 |
| FrameReq | 请求采集一帧 |
| FPD Enable | 开启探测器积分窗口 |
| X-Ray | X射线曝光 |
| Readout | 图像读出 |
| Stop Cmd | 停止采集 |

---

# 5. Timing Sequence

典型动态采集流程：

```text
Acquire Cmd
      │
      ▼
Sync In
      │
      ▼
FrameReq
      │
      ▼
FPD Enable
      │
      ▼
X-Ray Exposure
      │
      ▼
Readout
      │
      ▼
Image Output
      │
      ▼
Next Frame
```

---

# 6. Timing Parameters

## T0 — Preparation Time

定义：

从收到 Trigger 到 Detector 开始响应所需时间。

作用：

- FPGA 初始化
- Firmware 状态切换
- Detector 准备

---

## T1 — Exposure Window

定义：

Enable 有效期间。

X-Ray 必须位于 Enable Window 内。

特点：

- 决定曝光时间
- Enable 结束后不能继续曝光

---

## T2 — Readout Time

定义：

Detector 完成当前 Frame 数据读出的时间。

影响因素：

- ROI
- Frame Rate
- Detector 型号
- Binning

---

## T3 — Idle Time

定义：

当前 Frame 完成后，到下一 Trigger 到来之前的等待时间。

---

# 7. Relationship Between Timing Parameters

一个 Frame 周期满足：

```text
Frame Period

=

T0

+

T1

+

T2

+

T3
```

其中：

- Frame Period 由 Frame Rate 决定。
- T2 越长，可用于曝光的时间越短。
- ROI 越小，Readout Time 越短。
- Binning 可缩短 Readout Time。

---

# 8. Engineering Notes

## Trigger Frequency

Trigger 输入频率不得高于当前 Mode 配置的最大 Frame Rate。

否则：

- Trigger 被忽略
- 无法响应
- 出现丢帧

---

## Exposure Window

X-Ray 必须完全位于 Enable Window 内。

否则可能导致：

- 图像亮度不足
- 图像截断
- 曝光异常

---

## Readout

Readout 未完成时禁止开始下一次读出。

否则可能出现：

- Frame Loss
- Image Loss
- 数据错乱

---

# 9. Common Problems

## Image Loss

可能原因：

- Trigger 过快
- Readout 未完成
- 网络丢包
- Frame Buffer 满

---

## Timeout

可能原因：

- Trigger 未到达
- Enable 未开启
- Firmware 卡死

---

## Wrong Exposure

可能原因：

- Enable 配置错误
- Trigger 延迟
- X-Ray Timing 错误

---

# 10. Related Documents

- AcquisitionWorkflow.md
- ExposureWorkflow.md
- ReadoutWorkflow.md
- ImageGenerationWorkflow.md
- DynamicAcquisitionWorkflow.md
- ModeWorkflow.md
- WorkflowTroubleshooting.md

---

# 11. Summary

Timing Workflow 是动态平板工作流程的核心基础。所有图像采集均依赖 Trigger、Enable、Exposure、Readout 等关键时序信号协同完成。理解 Timing Workflow 有助于分析 Image Loss、Timeout、曝光异常及动态图像采集失败等问题，并为 Mode 配置、Firmware 开发及现场故障诊断提供理论依据。