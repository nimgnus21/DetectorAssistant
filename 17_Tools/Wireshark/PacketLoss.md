# Wireshark Packet Loss Analysis

## Purpose

Capture and preserve packet-level evidence when acquisition, image transmission or network behavior suggests packet loss.

## Procedure

1. Identify the correct active network interface.
2. Start capture before reproducing the problem.
3. Record the reproduction start time and detector/host IP information.
4. Reproduce the issue once under controlled conditions when possible.
5. Stop capture and save the original capture file without modification.
6. Correlate timestamps with SDK/Detector logs and acquisition behavior.

## Output

- Capture file
- Capture interface
- Time window
- Host/detector addressing
- Reproduction result

## Related Documents

- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [Packet Loss Knowledge](../../07_FailureKnowledge/ImageFailure/PacketLoss.md)
