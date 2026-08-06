# Mosaic

Version: V1.0

Case ID: CASE-IMG-009

Module: 11_Case / Image

Status: Released

Severity: ★★★★★

Typical Frequency: ★★★☆☆

Applicable Products:

- Pluto Series
- Wired Dynamic Detector
- Wired Static Detector

Related Documents:

- ../../08_ImageDiagnosis/MosaicArtifact/
- ../../07_FailureKnowledge/ImageFailure/MosaicFailure.md
- ../../09_DecisionTree/Image/Mosaic.md
- ../../17_Tools/Wireshark/
- ../../17_Tools/Ping/
- ../../17_Tools/Log Viewer/

---

# 1. Case Summary

## Case Name

Mosaic Image Caused by Ethernet Packet Loss

---

# 2. Customer Information

Customer：

OEM Customer

Product：

Pluto0900X

Communication：

Gigabit Ethernet

Working Mode：

Continuous Acquisition

---

# 3. Fault Description

客户反馈：

动态图像出现明显马赛克。

异常特点：

- 图像块状错位
- 每次位置不同
- 有时恢复正常
- 高帧率时更容易出现
- 静态采图偶尔正常

客户认为：

Detector FPGA 已损坏。

---

# 4. Initial Customer Judgment

Customer Judgment：

- Detector Hardware Failure（√）
- FPGA Failure（？）
- SDK Failure（？）

FAE Initial Assessment：

优先排查网络数据完整性。

---

# 5. Evidence Collection

## Detector

- [ ] Detector SN
- [ ] Firmware Version

## Network

- [ ] 网卡型号
- [ ] Jumbo Frame
- [ ] MTU
- [ ] Driver Version
- [ ] 网卡节能设置

## Image

- [ ] RAW Image
- [ ] SDK Screenshot

## Logs

- [ ] SDK Log
- [ ] Wireshark 抓包
- [ ] Ping Result

---

# 6. FAE Investigation

## Step 1

连续采图。

结果：

图像马赛克位置随机。

判断：

不像固定硬件故障。

---

## Step 2

检查 SDK。

发现：

偶尔出现：

Image Loss。

---

## Step 3

检查网络配置。

确认：

- Jumbo Frame

结果：

未启用。

---

## Step 4

检查 MTU。

发现：

默认 1500 Bytes。

Detector 配置要求：

9000 Bytes。

---

## Step 5

修改：

- Jumbo Frame
- MTU

重新启动网卡。

重新采图。

异常明显减少。

---

## Step 6

继续检查：

网卡驱动。

发现：

驱动版本过旧。

升级驱动。

再次验证。

图像恢复正常。

---

# 7. Root Cause

由于网络数据包丢失，导致图像数据接收不完整，最终形成 Mosaic Artifact。

并非 Detector 图像采集异常。

---

# 8. Corrective Action

现场处理：

① 开启 Jumbo Frame。

② 修改 MTU。

③ 更新网卡驱动。

④ 关闭网卡节能。

⑤ 降低 Frame Rate 验证。

⑥ 使用 Wireshark 检查丢包。

---

# 9. Verification

验证结果：

- 连续采图正常
- 无 Mosaic
- 无 Image Loss
- 长时间运行稳定

客户确认恢复。

---

# 10. Preventive Action（CAPA）

建议：

① 安装 Detector 前确认 Jumbo Frame。

② 固定使用推荐驱动版本。

③ 禁止开启网卡节能。

④ 高帧率前验证网络稳定性。

⑤ 保存网络配置。

---

# 11. Lessons Learned

## Technical

Mosaic 多数属于数据传输异常，而不是 Detector 成像异常。

## Diagnostic

随机位置 Mosaic，应首先检查网络，而不是重新校准。

## Operation

修改 MTU 后必须重新连接 Detector。

## Maintenance

建议长期保存 Wireshark 抓包作为分析依据。

---

# 12. Field Experience

> **FAE现场经验**

若同时出现：

- Image Loss
- Mosaic

优先检查：

- Jumbo Frame
- MTU
- Driver
- 网卡节能

不要立即怀疑 FPGA。

---

# 13. Related Documents

Image Diagnosis：

- MosaicArtifact

Failure Knowledge：

- MosaicFailure.md

Decision Tree：

- Mosaic.md

Tools：

- Wireshark
- Ping
- Log Viewer

---

# 14. Revision History

| Version | Date | Description |
|----------|------|-------------|
| V1.0 | 2026-08 | 建立 Mosaic 图像异常现场案例。 |