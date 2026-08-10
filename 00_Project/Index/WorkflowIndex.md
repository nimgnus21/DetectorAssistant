# Workflow Index

## Purpose

提供探测器技术支持工作流的统一入口，用于按现场阶段定位执行流程。

## Core Workflows

- [Workflow Module](../../06_Workflow/README.md)
- [Power On Workflow](../../06_Workflow/PowerOnWorkflow.md)
- [Communication Workflow](../../06_Workflow/CommunicationWorkflow.md)
- [Connection Workflow](../../06_Workflow/ConnectionWorkflow.md)
- [Image Generation Workflow](../../06_Workflow/ImageGenerationWorkflow.md)
- [Configuration Workflow](../../06_Workflow/ConfigurationWorkflow.md)
- [Shutdown Workflow](../../06_Workflow/ShutdownWorkflow.md)
- [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)

## Operational Flow

```text
Power On
    ↓
Configuration
    ↓
Connection
    ↓
Communication
    ↓
Image Generation
    ↓
Troubleshooting / Verification
    ↓
Shutdown
```

## Related SOP

- [SOP Module](../../10_SOP/)

## Maintenance Rule

新增现场工作流后，应补充本索引，并确认 Workflow、DecisionTree 与 SOP 的边界一致。
