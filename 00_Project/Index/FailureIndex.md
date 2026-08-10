# Failure Index

> Purpose: 快速定位故障知识、决策树与关联模块。

---

# Image Failure

| Symptom | Primary Knowledge | Diagnostic Direction |
|---|---|---|
| 异常横纹，随位置变化 | `07_FailureKnowledge/ImageFailure/InterferenceStripe.md` | 环境 / 外部干扰 |
| 多段数据缺失、条带宽度一致 | `07_FailureKnowledge/ImageFailure/PacketLoss.md` | 网络传输 / 丢包 |
| 每幅图等宽亮暗规则条纹 | `07_FailureKnowledge/ImageFailure/CalibrationStripe.md` | 校正模板 / 失校正 |
| 异常条状区域 | `07_FailureKnowledge/ImageFailure/DefectiveBar.md` | 先重新校正 |
| 固定坏点或坏线 | `07_FailureKnowledge/ImageFailure/DefectPixelLine.md` | Defect 校正 / 升级分析 |
| 黑点伪影 | `07_FailureKnowledge/ImageFailure/BlackDotArtifact.md` | 图像伪影方向 |
| 固定横线 | `09_DecisionTree/Image/HorizontalLine.md` | Offset → Gain → 固定位置 → 硬件 |
| TFT 损伤相关异常 | `07_FailureKnowledge/ImageFailure/TFTDamage.md` | 硬件损伤方向 |
| 采图失败 | `07_FailureKnowledge/ImageFailure/ImageAcquisitionFailure.md` | 采集链路 |

---

# Connection Failure

| Symptom | Knowledge |
|---|---|
| 探测器无法连接 | `07_FailureKnowledge/ConnectionFailure/UnableToConnect.md` |
| 无线 AP / Client 配置 | `04_Software/Settings/WirelessMode.md` |

---

# Tool and Evidence

- `17_Tools/SDKTool/iDetectorQuickTroubleshooting.md`
- `04_Software/Log/ExportLog.md`
- `04_Software/Log/LogCollection.md`

---

# Error Code

- `12_ErrorCode/Mercu0606X1CommonError.md`

---

# Entry Rule

处理现场问题时：

1. 先按现象进入本索引。
2. 优先阅读对应 FailureKnowledge 或 DecisionTree。
3. 收集文档要求的证据。
4. 完成处理后检查 `11_Case` 是否已有相同案例。
5. 若无案例且根因已确认，再新增真实 Case。
