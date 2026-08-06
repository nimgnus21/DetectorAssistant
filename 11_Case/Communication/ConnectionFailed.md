# ConnectionFailed

Version: V1.0

Module: 11_Case / Communication

Status: Released

Severity: ★★★★★

Typical Frequency: ★★★★★（现场高频）

Applicable Products:

- Static Flat Panel Detector
- Dynamic Flat Panel Detector
- Wired Detector
- Wireless Detector（AP Mode）
- Pluto Series

Related Documents:

- ../../06_Workflow/ConnectionWorkflow.md
- ../../07_FailureKnowledge/SystemFailure/CommunicationFailure.md
- ../../09_DecisionTree/Connection/
- ../../17_Tools/Ping/
- ../../17_Tools/Wireshark/

---

# 1. Case Summary

## Case Name

Connection Failed

## Description

PC 无法正常连接探测器，SDK 无法识别设备或无法建立通信。

该问题属于现场最常见的通信类故障之一。

常见表现包括：

- Detector Offline
- Connect Failed
- Device Not Found
- Connection Timeout
- Cannot Open Detector
- SDK 无法发现设备

---

# 2. Applicable Products

适用于：

- 有线探测器
- 无线探测器（AP Mode）
- SDK_AIO
- Pluto 系列
- 所有基于 Gigabit Ethernet 通信的探测器

---

# 3. Environment

## Wired

```text
PC

↓

Ethernet

↓

Detector
```

或

```text
PC

↓

Switch

↓

Detector
```

---

## Wireless (AP Mode)

```text
PC

↓

Wireless Adapter

↓

Detector(AP)
```

---

# 4. Fault Phenomenon

现场可能出现以下现象：

- SDK 搜索不到 Detector
- Detector Offline
- Ping 不通
- 无法建立连接
- Acquisition Failed
- Timeout
- Detector 图标为灰色
- 软件一直提示等待连接

---

# 5. Root Cause Analysis

根据现场经验，Connection Failed 通常可分为以下几类。

## 5.1 Network Configuration

网络配置错误：

- IP 地址错误
- 子网掩码错误
- 网卡选择错误
- AP 模式配置错误

属于现场最高频原因。

---

## 5.2 Physical Connection

硬件连接异常：

- 网线损坏
- 网口接触不良
- 交换机异常
- PoE 异常（如适用）

---

## 5.3 Detector Status

探测器自身异常：

- 未启动
- Firmware 异常
- 系统未完成初始化

---

## 5.4 Software Configuration

软件配置错误：

- SDK 配置错误
- Detector 配置错误
- License 问题
- 软件版本不匹配

---

## 5.5 Firewall / Security

Windows Firewall

杀毒软件

第三方网络安全软件

阻止 SDK 通信。

---

# 6. Diagnostic Process

建议按照以下顺序排查。

---

## Step 1

确认 Detector 是否正常供电。

检查：

- 电源指示灯
- Link 指示灯
- ACT 指示灯

---

## Step 2

确认 PC 使用正确网卡。

不要修改其它网卡。

仅修改当前连接 Detector 的网卡。

> 现场经验：
>
> 当 Detector 连接失败时，
> **只需要修改当前连接探测器的网卡 IP。**
>
> 其它网卡保持默认配置。

若使用 AP Mode：

修改无线网卡配置。

---

## Step 3

检查 IP 配置。

确认：

- IP 地址
- Subnet Mask

符合产品要求。

---

## Step 4

使用 Ping。

确认：

- 是否能够 Ping 通 Detector
- 是否存在大量丢包
- 是否响应稳定

---

## Step 5

确认 SDK 是否能够搜索到 Detector。

若仍失败：

继续检查：

- License
- Firmware
- Detector Configuration

---

## Step 6

若通信正常但 SDK 无法连接。

建议：

- 重启 SDK
- 重启 Detector
- 重启 PC

再次测试。

---

# 7. Typical Field Experience

## Case 1

### Phenomenon

Connection Failed

### Cause

连接了错误网卡。

### Solution

修改当前连接 Detector 的网卡 IP。

恢复正常。

---

## Case 2

### Phenomenon

无线连接失败。

### Cause

修改了有线网卡。

### Solution

AP Mode 下应修改：

无线网卡配置。

恢复正常。

---

## Case 3

### Phenomenon

SDK 无法发现 Detector。

### Cause

Windows Firewall 阻止通信。

### Solution

关闭 Firewall。

恢复正常。

---

# 8. Verification

满足以下条件：

- Ping 正常
- Detector Online
- SDK 成功连接
- Acquisition 成功
- 图像采集正常

即可判定恢复。

---

# 9. Engineering Experience

## Experience 1

Connection Failed 时：

不要修改所有网卡。

只修改：

**当前连接 Detector 的网卡。**

---

## Experience 2

AP 模式：

修改无线网卡。

不要修改有线网卡。

---

## Experience 3

若 Ping 已正常：

优先检查：

- SDK
- License
- Firmware

而不是继续修改网络。

---

## Experience 4

现场修改网络配置后：

建议重新启动 SDK。

部分 SDK 不会自动刷新网络状态。

---

# 10. Prevention

建议现场安装时：

- 固定网卡配置
- 禁止自动切换网络
- 保留网络配置记录
- 使用固定质量网线
- 定期检查交换机状态

---

# 11. Related Documents

Workflow：

- ConnectionWorkflow.md

Failure Knowledge：

- CommunicationFailure.md

Decision Tree：

- Connection/

Tools：

- Ping
- Wireshark

---

# 12. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 初版建立，整理 Connection Failed 现场案例及排查经验。 |
---

# 15. Field Cases

## Case 01 – Incorrect Jumbo Frame Configuration

### Product

Mercu1616TE

### Customer

OEM Customer

### Symptom

- Detector could be discovered successfully.
- SDK connected to the detector normally.
- Image acquisition could not be started.
- Acquisition timed out after triggering.

### Investigation

The following items were verified:

- Detector communication: Normal
- Network cable: Normal
- IP configuration: Normal
- SDK version: Compatible
- Firmware version: Compatible

No hardware abnormalities were found.

Further inspection of the Ethernet adapter configuration showed that the Jumbo Frame setting did not meet the detector communication requirements.

### Root Cause

Incorrect Jumbo Frame configuration on the host network adapter prevented normal image data transmission.

The detector itself operated normally.

### Corrective Action

1. Open the Ethernet adapter properties.
2. Check the Jumbo Frame parameter.
3. Configure the value according to the product communication requirements.
4. Restart the network adapter if required.
5. Reconnect the detector and perform image acquisition.

### Verification

After correcting the Jumbo Frame configuration:

- Detector communication remained normal.
- Image acquisition resumed successfully.
- No timeout occurred during continuous acquisition.

### Lessons Learned

Communication failures are not always caused by detector hardware.

When the detector can be connected but image acquisition fails, network adapter configuration (including Jumbo Frame) should be verified before replacing hardware.