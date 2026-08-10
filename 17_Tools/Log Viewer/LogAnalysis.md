# Log Analysis

## Objective

Turn raw logs into traceable evidence without replacing observed facts with unsupported interpretation.

## Procedure

1. Define the symptom and reproduction time.
2. Locate the corresponding log time window.
3. Record connection state, command/event/error sequence visible in that window.
4. Compare with the operation being performed.
5. Link the finding to the relevant DecisionTree, ErrorCode or FailureKnowledge node.
6. Preserve the original log and record the interpretation separately.

## Output Format

- Time window
- Relevant event/error
- Observed operation
- Interpretation
- Related knowledge node

## Rule

A single log message is not automatically a root cause. Escalate contradictions or incomplete evidence as unresolved.

## Related Documents

- [Common Logs](CommonLogs.md)
- [ErrorCode](../../12_ErrorCode/)
- [Workflow Troubleshooting](../../06_Workflow/WorkflowTroubleshooting.md)
