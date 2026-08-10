# Common Logs

## Purpose

Identify the minimum log set required to correlate a support event.

## Collect When Available

- Detector log
- SDK/application log
- Firmware and FPGA version information
- SDK version
- Error code and timestamp
- Configuration relevant to the failure

## Collection Rule

Preserve the original files before clearing, reinstalling, resetting or repeatedly retrying the operation.

## Output

A timestamped evidence package that can be correlated with the observed symptom.

## Related Documents

- [Log Analysis](LogAnalysis.md)
- [Log Export](../SDKTool/LogExport.md)
- [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)
