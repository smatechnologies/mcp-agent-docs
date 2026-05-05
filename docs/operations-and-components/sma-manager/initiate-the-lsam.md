---
title: LSAM Start and Stop (INITLSAM / STOPLSAM)
description: "Start or stop the MCP Agent and optionally the Resource Monitor using the INITLSAM and STOPLSAM screens."
tags:
  - Procedural
  - System Administrator
  - Operations Staff
  - Agents
  - System Configuration
---

# LSAM

## What is it?

The INITLSAM and STOPLSAM screens control starting and stopping the MCP Agent, with the option to include or exclude the Resource Monitor in the same operation. Debug mode can also be enabled at startup to capture diagnostic information for support purposes.

- Start the MCP Agent alone or together with the Resource Monitor, optionally with debug mode active.
- Stop the MCP Agent gracefully, with the option to stop the Resource Monitor at the same time.

## Initiate the Agent (INITLSAM)

Use this screen to start the agent, and optionally the Resource Monitor if you have configured the agent to include the Resource Monitor within the agent WFL. You may also initiate the agent with debug enabled if you are attempting to capture debug information for SMA Technologies Support regarding an issue.

*SMA Configuration and Operations Manager: SMAINITLSAM*

![SMAINITLSAM](../../../static/img/smainitlsam.png)

## Stop the Agent (STOPLSAM)

Use this screen to stop the agent, and optionally the Resource Monitor as well. You may also stop the Resource Monitor using the STOPRM main menu option.

*SMA Configuration and Operations Manager: SMASTOPLSAM*

![SMASTOPLSAM](../../../static/img/smastoplsam.png)
