---
title: Update the Max Number Concurrent Jobs Field
description: "Remove LSAM checkpoint and tracking files and restart the agent after changing the maximum concurrent jobs configuration value."
tags:
  - Procedural
  - System Administrator
  - System Configuration
  - Agents
---

# Update the "Max Number Concurrent Jobs" Field

## What is it?

This page explains the mandatory steps required after changing the "Max number concurrent jobs" configuration value, specifically removing the checkpoint files and tracking file before restarting the MCP Agent to prevent fatal startup errors. It provides the exact MARC/CANDE REMOVE commands needed to clear these files.

- Use this page whenever the maximum concurrent jobs value is adjusted to ensure the MCP Agent starts cleanly without the segment array or assertion failure errors described in the MCP Known Issues topic.
- Use this page to verify that all active jobs have completed before stopping the MCP Agent and removing the checkpoint and tracking files.

If the "Max number concurrent jobs" configuration variable is changed, remove the agent's checkpoint files and tracking file before restarting the MCP Agent. The value sizes the agent's internal arrays and the records in these files; starting the agent with files built for the previous value causes a fatal error.

When you save a new value on the SMAVAR screen, SMA/MANAGER confirms the change with this message:

```

Changes saved. REMOVE TRACKING AND CHECKPOINT FILES.

```

## Startup Errors Caused by Skipping These Steps

If the agent is restarted before the files are removed, the module that reaches the mismatch first ends abnormally. Any of the following may appear, depending on the module and the agent version:

| Error | Module |
| ----- | ------ |
| SEG ARRAY ERR @178600 | \*SMA/MCP/INTERFACE/xxx |
| F-DS INVALID INDEX @ 02412000 | \*SMA/MCP/INTERFACE/xxx |
| INVALID INDEX @ (04637000) | \*SMA/MCP/INTERFACE/xxx |
| ASSERTION FAILURE ON RANGE TEST @ (Expression out of range 91700) | \*SMA/COMM/xxx |
| SEG ARRAY ERR around 924100 | \*SMA/ALGOLPROCS/xxx |

All of these have the same resolution: remove the files listed below and start the agent again. Refer to [MCP Known Issues](../reference-information/mcp-known-issues.md) and [LSAM Initialization and Stopping Troubleshooting](../reference-information/troubleshooting/lsam-initialization-stopping.md) for the individual entries.

## Remove Checkpoint and Tracking Files

To update the maximum concurrent jobs setting, complete the following steps:

1. Determine whether jobs were active the last time the MCP Agent was stopped. If jobs were active, start the agent to allow recovery to take place and the active jobs to complete.
2. Stop the MCP Agent. For instructions on stopping the agent, refer to [Stop the LSAM](../operations-and-components/sma-manager/initiate-the-lsam.md#stop-the-agent-stoplsam).
3. Modify the configuration file to reflect the desired "Max number of concurrent jobs." For more information on configuration, refer to [Max number concurrent jobs](../configuration/processing-variables.md#max-number-concurrent-jobs).
4. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/CP/MCS/xxx/=. Transmit the line.
5. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/CP/LIB/=. Transmit the line.
6. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/TRACKING/FILE/xxx. Transmit the line.
7. Repeat steps 4 through 6 for every family on the system, not only the family on which the agent runs.
8. Start the MCP Agent. For instructions on starting the agent, refer to [MCP LSAM Operation](../operations-and-components/mcp-lsam-operation.md).

:::caution

Check all families on the system. A checkpoint or tracking file left on another family causes the same startup errors after the agent is restarted.

:::

:::info Note

Steps 4 and 5 remove the checkpoint files. REMOVE*SMA/CP/= removes both sets in one command. The \*SMA/CP/LIB/= files are the ones \*SMA/ALGOLPROCS/xxx reads, so leaving them behind produces SEG ARRAY ERR around 924100 even when the \*SMA/CP/MCS/xxx/= files were removed.

:::
