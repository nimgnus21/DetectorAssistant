# Jumbo Frame Verification

## Purpose

Verify whether Jumbo Frame configuration is consistent across the active network path when this configuration is required by the deployment.

## Procedure

1. Record the current host adapter setting before changes.
2. Confirm the expected detector/network requirement from the applicable product configuration.
3. Verify all relevant devices in the active path support the selected setting.
4. Change one parameter set at a time.
5. Repeat connection and acquisition verification.
6. Record before/after results and restore the previous setting if the change is not validated.

## Warning

Do not assume a larger MTU is always correct. A mismatch can create a different communication problem.

## Related Documents

- [Network Configuration SOP](../../10_SOP/NetworkConfiguration.md)
- [GigE Analysis](GigEAnalysis.md)
