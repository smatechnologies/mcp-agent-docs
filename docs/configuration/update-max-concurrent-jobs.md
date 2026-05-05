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

If the "Max number concurrent jobs" configuration variable is changed, remove the agent's checkpoint files and tracking file before restarting the MCP Agent. Refer to [MCP Known Issues](../reference-information/mcp-known-issues) concerning a Known Issue about the "Max number concurrent jobs" field and startup errors.

## Remove Checkpoint and Tracking Files

To update the maximum concurrent jobs setting, complete the following steps:

1. Determine whether jobs were active the last time the MCP Agent was stopped. If jobs were active, start the agent to allow recovery to take place and the active jobs to complete.
2. Stop the MCP Agent. For instructions on stopping the agent, refer to [Stop the LSAM](../operations-and-components/sma-manager/initiate-the-lsam#stop-the-agent-stoplsam).
3. Modify the configuration file to reflect the desired "Max number of concurrent jobs." For more information on configuration, refer to [Max number concurrent jobs](../configuration/processing-variables#max-number-concurrent-jobs).
4. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/CP/MCS/xxx/=. Transmit the line.
5. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/TRACKING/FILE/xxx. Transmit the line.
6. Start the MCP Agent. For instructions on starting the agent, refer to [MCP LSAM Operation](../operations-and-components/mcp-lsam-operation).
