# ImageAcquisitionFailure

Version: V1.0

Module: Failure Knowledge

Status: Released

Applicable Product:
- Mercu0606X1
- Mars1717V3
- Venu1717X

---

# 1. Phenomenon

探测器连接完成后无法正常获得图像，或曝光后图像未正常返回。

---

# 2. Diagnostic Sequence

按以下顺序缩小范围：

1. 确认探测器连接状态。
2. 确认应用模式和采图模式配置。
3. 确认曝光是否实际触发。
4. 检查图像接收与网络传输状态。
5. 检查校正及相关配置状态。
6. 导出日志用于进一步分析。

---

# 3. Evidence Collection

建议保留：

- 采图界面截图
- 异常图像或原始图像
- Detector Interface 信息
- Firmware Version
- SDK Version
- Debug Log

---

# 4. Reference

Source:
- Mercu0606X1 Trouble Shooting Guide Line（2026.08）
- Mars1717V3 & Venu1717X 使用及故障排查指南
