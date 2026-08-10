# Ping Network Diagnosis

## Purpose

Verify basic IP reachability between host and detector and collect repeatable connectivity evidence.

## Procedure

1. Record host IP and detector IP.
2. Confirm both endpoints use the expected subnet configuration.
3. Run a continuous or repeated Ping test for the defined verification window.
4. Record reply status, packet loss and latency variation.
5. If Ping fails, check physical link and IP/subnet before changing other parameters.
6. If Ping is stable but acquisition still fails, continue with SDK connection checks and, when packet-level evidence is needed, [Wireshark](../Wireshark/README.md).

## Output

- Ping target
- Test duration/count
- Packet loss result
- Representative latency result

## Related Documents

- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [Connection DecisionTree](../../09_DecisionTree/Connection/)
