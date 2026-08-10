# FailureKnowledge

Version: V2.1

Module: Failure Knowledge

Status: Released

Source Level:
- Engineering
- Service

Applicable Product:
- Wired Detector
- Wireless Detector

Related Modules:
- ../03_Hardware/
- ../04_Software/
- ../05_Calibration/
- ../06_Workflow/
- ../09_DecisionTree/
- ../10_SOP/
- ../11_Case/
- ../17_Tools/

---

# 1. Module Purpose

Failure Knowledge（故障知识库）用于建立数字平板探测器的系统化故障知识体系。

本模块重点回答：

> **为什么会发生该故障，以及该现象应关联到哪些诊断方向。**

现场执行路径由 DecisionTree、SOP 和 Tools 承接；真实验证经验由 Case 承接。

---

# 2. Module Structure

```text
07_FailureKnowledge/
├── README.md
├── FailureClassification.md
├── FailureAnalysisMethod.md
├── FailureCode.md
├── HardwareFailure/
├── SoftwareFailure/
├── ConnectionFailure/
├── CalibrationFailure/
├── ImageFailure/
├── EnvironmentFailure/
└── SystemFailure/
```

说明：以当前仓库实际目录为准；不要引用不存在的 `CommunicationFailure/` 或 `PowerFailure/` 目录。

---

# 3. Core Navigation

## Image Failure

- [Interference Stripe](ImageFailure/InterferenceStripe.md)
- [Packet Loss](ImageFailure/PacketLoss.md)
- [Calibration Stripe](ImageFailure/CalibrationStripe.md)
- [Defective Bar](ImageFailure/DefectiveBar.md)
- [Defect Pixel / Line](ImageFailure/DefectPixelLine.md)
- [Black Dot Artifact](ImageFailure/BlackDotArtifact.md)
- [TFT Damage](ImageFailure/TFTDamage.md)
- [Image Acquisition Failure](ImageFailure/ImageAcquisitionFailure.md)

Related DecisionTree:
- [Horizontal Line](../09_DecisionTree/Image/HorizontalLine.md)

Related SOP:
- [Image Troubleshooting](../10_SOP/ImageTroubleshooting.md)

Related Tools:
- [Tools Entry](../17_Tools/README.md)

## Connection Failure

- [Unable To Connect](ConnectionFailure/UnableToConnect.md)

Related DecisionTree:
- [Connection](../09_DecisionTree/Connection/)

Related SOP:
- [Network Configuration](../10_SOP/NetworkConfiguration.md)

Related Tools:
- [Ping](../17_Tools/Ping/)
- [Wireshark](../17_Tools/Wireshark/)

## Calibration Failure

Use this category together with:
- [Calibration Module](../05_Calibration/)
- [Calibration DecisionTree](../09_DecisionTree/Calibration/)
- [Calibration SOP](../10_SOP/Calibration.md)
- [SDK Tools](../17_Tools/SDKTool/)

---

# 4. Relationship Model

```text
Workflow
    ↓
Failure Knowledge
    ↓
DecisionTree
    ↓
SOP / Tool
    ↓
Verification
    ↓
Case or Escalation
```

Failure Knowledge provides the fault mechanism and diagnostic direction; DecisionTree provides the branching logic; SOP and Tools provide the execution method; Case stores verified field experience.

---

# 5. Case Feedback Rule

FailureKnowledge is not a substitute for a verified Case.

When a field issue is resolved:

1. Check `11_Case` for an existing matching case.
2. Confirm the final root cause and verification result.
3. Add a new Case only when the evidence is complete.
4. Update FailureKnowledge, DecisionTree, SOP, Tool links or Index only when the verified result changes reusable knowledge.

---

# 6. Maintenance Rules

Each failure document should maintain links to the applicable downstream modules when they exist:

- DecisionTree
- SOP
- Tool
- ErrorCode
- Case

Do not create a second diagnostic path when an existing DecisionTree already owns the main flow. Prefer adding a discriminating branch or cross-link.
