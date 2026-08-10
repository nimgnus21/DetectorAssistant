# DefectPixelLine

Version: V1.0

Module: Failure Knowledge

Status: Released

Applicable Product:
- Mercu0606X1
- Other supported detector products

---

# 1. Phenomenon

图像中出现固定坏点、坏线或局部固定异常像素。

---

# 2. First-line Direction

优先进入 Defect / Correction 方向检查，不与随位置变化的环境干扰或网络丢包混淆。

---

# 3. Field Handling

1. 确认异常位置是否固定。
2. 连续采集多幅图像验证重复性。
3. 检查 Defect 相关校正状态。
4. 按适用产品流程执行 Defect Generation 或相关校正。
5. 重新采图验证。
6. 仍无法恢复时，保留异常图像并升级分析。

---

# 4. Distinction

| Phenomenon | Direction |
|---|---|
| 固定点状异常 | Defect Pixel |
| 固定线状异常 | Defect Line |
| 条纹随位置变化 | Interference |
| 多段缺失数据 | Packet Loss |

---

# 5. Reference

Source: Mercu0606X1 Trouble Shooting Guide Line（2026.08）
