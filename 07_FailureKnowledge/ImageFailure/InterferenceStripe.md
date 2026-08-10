# InterferenceStripe

Version: V2.0

Module: Failure Knowledge

Status: Released

Source Level:
- Service
- Field Troubleshooting

Applicable Product:
- Wired Detector
- Wireless Detector

Related Documents:
- LineArtifact.md
- NoiseArtifact.md
- OffsetArtifact.md
- ../../09_DecisionTree/

---

# 1. Purpose

Interference Stripe（干扰条纹）用于描述由外部或环境干扰导致的图像横向条纹，并与固定坏线、失校正条纹及数据丢包进行区分。

本文件回答的问题：

> 图像出现异常横纹时，如何判断是否属于环境干扰？

---

# 2. Typical Characteristics

- 暗场图中也可能出现横纹。
- 条纹位置或形态会随探测器位置变化而变化，甚至消失。
- 条纹方向通常以横向为主。
- 现象可能具有环境相关性和位置相关性。

---

# 3. Diagnostic Principle

改变探测器位置，在多个位置重复采集暗场图。

- 条纹随位置变化或消失：优先判断为外部干扰或环境相关问题。
- 条纹位置固定：转入固定线状伪影或坏线方向排查。
- 每幅图出现等宽、亮暗相间规则条纹：优先检查校正模板是否加载或失效。
- 图像出现多段缺失数据、条带宽度一致：优先检查网络丢包。

---

# 4. Diagnostic Flow

```text
Image Stripe
    ↓
Acquire Dark Image
    ↓
Dark Image Contains Stripe?
    ├── No → Check exposure/correction chain
    └── Yes
          ↓
Move Detector and Acquire Again
          ↓
Stripe Changes or Disappears?
    ├── Yes → Interference / Environment Direction
    └── No  → Fixed Line / Defect / Hardware Direction
```

---

# 5. Field Action

1. 在当前位置采集暗场图。
2. 移动探测器至不同位置。
3. 在每个位置重复采集暗场图。
4. 比较条纹方向、位置和形态。
5. 若条纹随位置变化，记录现场环境和可能干扰源。
6. 若条纹固定不变，转入 Line Artifact / Defect Line 排查。

---

# 6. Related Knowledge

| Phenomenon | Primary Direction |
|---|---|
| 暗场横纹随位置变化 | Interference / Environment |
| 固定位置横线 | Line Artifact / Gate / Readout |
| 规则等宽亮暗条纹 | Calibration Template |
| 多段数据缺失条带 | Network Packet Loss |

---

# 7. Reference

Source: Mars1717V3 & Venu1717X 使用及故障排查指南
