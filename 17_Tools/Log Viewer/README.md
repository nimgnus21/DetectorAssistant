# Log Viewer

## Purpose

用于查看和关联探测器、SDK、连接、校正及升级过程中的日志异常时间点。

## Use When

- 连接失败或状态异常
- 校正重复失败
- 固件升级失败、超时或回退
- 需要把异常事件与现场操作时间关联

## Standard Input

- Detector.log 或适用日志文件
- 操作时间
- Detector Model / SN
- Firmware / SDK Version

## Output

- 异常时间点
- 关键事件或错误码
- 与现场操作的对应关系

## Related Documents

- [Image Troubleshooting SOP](../../10_SOP/ImageTroubleshooting.md)
- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [Calibration SOP](../../10_SOP/Calibration.md)
- [Firmware Upgrade SOP](../../10_SOP/FirmwareUpgrade.md)
- [ErrorCode](../../12_ErrorCode/)
