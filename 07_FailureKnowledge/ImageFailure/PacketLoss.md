# PacketLoss

Version: V1.0

Module: Failure Knowledge

Status: Released

Applicable Product:
- Network Detector
- Wireless Detector

Related Documents:
- InterferenceStripe.md
- CalibrationStripe.md

---

# 1. Phenomenon

图像出现多段数据缺失或条带状异常区域，异常条带宽度可能保持一致。

---

# 2. Diagnostic Direction

当异常表现为数据段缺失时，优先进入网络传输方向，而不是直接判定为探测器成像缺陷。

---

# 3. Field Troubleshooting

1. 保存异常图像并确认异常条带形态。
2. 确认异常是否表现为多段数据缺失。
3. 检查当前网络连接状态。
4. 优先改善网络环境后重新采图验证。
5. 若改善网络后现象消失，记录为网络传输异常方向。

---

# 4. Distinction

| Phenomenon | Primary Direction |
|---|---|
| 多段缺失数据、条带宽度一致 | Packet Loss / Network |
| 条纹随探测器位置变化 | Interference |
| 每幅图固定规则亮暗条纹 | Calibration Template |
| 固定位置异常线 | Defect Line / Hardware |

---

# 5. Reference

Source: Mars1717V3 & Venu1717X 使用及故障排查指南
