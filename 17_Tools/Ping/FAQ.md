# Ping FAQ

## Ping succeeds, but detector cannot connect

Ping verifies basic IP reachability only. Continue with SDK connection state, configuration and logs.

## Ping intermittently loses packets

Record the test conditions and compare cable, network adapter and network topology. Use [Wireshark](../Wireshark/README.md) when packet-level evidence is required.

## Ping fails after changing IP

Recheck the host and detector IP/subnet and confirm the target address before changing additional parameters.

## Is one successful reply enough?

No. For troubleshooting, retain a repeatable result over the verification window and compare before/after configuration changes.
