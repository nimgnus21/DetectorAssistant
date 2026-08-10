# GigE Analysis

## Scope

Use this procedure when detector communication uses Gigabit Ethernet and basic Ping/connection checks do not explain intermittent transmission behavior.

## Checkpoints

- Correct capture interface
- Link state and speed
- Host and detector IP information
- Reproduction timing
- Packet sequence and retransmission/repetition behavior visible in the capture

## Workflow

1. Verify basic connectivity with Ping.
2. Start capture on the active adapter.
3. Reproduce one acquisition cycle.
4. Save the capture and correlate it with SDK/Detector logs.
5. Escalate with the original capture rather than screenshots alone when detailed analysis is required.

## Related Documents

- [Packet Loss](PacketLoss.md)
- [Log Export](../SDKTool/LogExport.md)
- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
