# DecisionTree

> 现场故障按“现象 → 分流 → 证据 → 验证 → 处理 → 升级”执行。

---

# Main Categories

- [Image](Image/)
- [Connection](Connection/)
- [Calibration](Calibration/)
- [Firmware](Firmware/)
- [Software](Software/)

---

# Image Entry

对于“横纹 / 条带 / 线状异常”，不要直接判定单一根因。

1. **固定横线、每张图重复出现**
   - [HorizontalLine](Image/HorizontalLine.md)
2. **其他图像异常**
   - 从 [Image DecisionTree](Image/) 按具体现象进入对应分支。

Execution:
- [Image Troubleshooting SOP](../10_SOP/ImageTroubleshooting.md)
- [Image Tools](../17_Tools/README.md)

---

# Connection Entry

- [Connection DecisionTree](Connection/)
- [Network Configuration SOP](../10_SOP/NetworkConfiguration.md)
- [Ping / Wireshark Tools](../17_Tools/README.md)

---

# Calibration Entry

Use the existing calibration branch together with:

- [Calibration DecisionTree](Calibration/)
- [Calibration SOP](../10_SOP/Calibration.md)
- [SDK Tools](../17_Tools/SDKTool/)
- [FailureKnowledge](../07_FailureKnowledge/README.md)

---

# Firmware Entry

- [Firmware DecisionTree](Firmware/)
- [Firmware Upgrade SOP](../10_SOP/FirmwareUpgrade.md)
- [Firmware Upgrade Tool Guidance](../17_Tools/SDKTool/FirmwareUpgrade.md)
- [Error Code Module](../12_ErrorCode/)

---

# Software Entry

- [Software DecisionTree](Software/)
- [Log Collection](../04_Software/Log/LogCollection.md)
- [SDK Tool Guidance](../17_Tools/SDKTool/README.md)
- [Error Code Module](../12_ErrorCode/)

---

# Evidence Before Escalation

Collect when applicable:

- Detector Model / SN
- Firmware Version
- SDK / Application Version
- RAW / Corrected / Dark Image
- Calibration Status
- Debug Log
- Network / Wireless Mode Information
- Steps already tried

Use the available evidence and case templates under [13_Template](../13_Template/).

---

# Case Feedback

DecisionTree is for field branching and does not replace a verified Case.

After resolution:

1. Search the relevant case category under [11_Case](../11_Case/).
2. Reuse an existing verified case when applicable.
3. Create a new Case only after phenomenon, investigation, final cause or treatment, and verification are recorded.
4. Feed verified reusable knowledge back to FailureKnowledge, DecisionTree, SOP, Tools, ErrorCode or Index as needed.
