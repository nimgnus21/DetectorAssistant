# DecisionTree

> 现场故障按“现象 → 分流 → 验证 → 处理 → 升级”执行。

---

# Main Categories

- `Image/`：图像异常
- `Connection/`：连接异常
- `Calibration/`：校准异常
- `Firmware/`：固件相关
- `Software/`：SDK / 软件异常

---

# Image Entry

对于“横纹 / 条带 / 线状异常”，不要直接判定单一根因。

优先按以下特征分流：

1. **固定横线、每张图重复出现**
   - `Image/HorizontalLine.md`
2. **暗场也有横纹，且移动探测器后状态变化**
   - `07_FailureKnowledge/ImageFailure/InterferenceStripe.md`
3. **多段数据缺失、条带宽度一致**
   - `07_FailureKnowledge/ImageFailure/PacketLoss.md`
4. **等宽、亮暗相间的规则条纹**
   - `07_FailureKnowledge/ImageFailure/CalibrationStripe.md`
5. **Mercu0606X1 异常条状区域**
   - `07_FailureKnowledge/ImageFailure/DefectiveBar.md`

---

# Evidence Before Escalation

优先收集：

- Detector Model / SN
- Firmware Version
- SDK / Application Version
- RAW Image
- Window Image
- Calibration Status
- Debug Log
- Network / Wireless Mode Information

---

# Case Feedback

DecisionTree 用于现场分流，不替代真实 Case。

问题解决后必须检查 `11_Case` 是否已有相同案例；确认根因和验证结果后，再沉淀新的 Case。
