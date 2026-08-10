# CalibrationStripe

Version: V1.0

Module: Failure Knowledge

Status: Released

Applicable Product:
- Mars1717V3
- Venu1717X
- Other products using correction templates

Related Documents:
- InterferenceStripe.md
- PacketLoss.md
- 05_Calibration/

---

# 1. Phenomenon

每幅图像均出现等宽、亮暗相间的规则条纹。

---

# 2. Primary Cause Direction

优先检查校正模板是否已加载，以及校正模板是否失效或异常。

该现象属于失校正方向，应与环境干扰条纹、网络丢包条带和固定坏线区分。

---

# 3. Diagnostic Flow

```text
Regular Stripe on Every Image
        ↓
Check Stripe Width and Repeatability
        ↓
Equal-width Bright/Dark Alternating?
        ├── No → Check Interference / Packet Loss / Defect Line
        └── Yes
              ↓
Check Correction Template
              ↓
Template Loaded and Valid?
        ├── No → Reload / Restore Correction Direction
        └── Yes → Continue Calibration Data Investigation
```

---

# 4. Field Check

1. 确认现象是否每幅图重复出现。
2. 确认是否为等宽、亮暗相间的规则条纹。
3. 检查校正模板加载状态。
4. 检查模板有效性。
5. 完成处理后重新采集图像验证。

---

# 5. Reference

Source: Mars1717V3 & Venu1717X 使用及故障排查指南
