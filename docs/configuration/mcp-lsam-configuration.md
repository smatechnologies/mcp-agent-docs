---
title: MCP LSAM Configuration
description: "Review and update the MCP LSAM configuration file to set communication options and activate optional features before starting the agent."
tags:
  - Conceptual
  - System Administrator
  - System Configuration
  - Agents
---

# MCP LSAM Configuration

## What is it?

This page introduces the MCP Agent configuration file and identifies the critical settings that must be correct before the agent can communicate with OpCon, including the OpCon port number, hostname alias, and maximum concurrent jobs value. It also notes the upgrade requirement to access the SMAMGR window when migrating to version 18.00.00 or higher.

- Use this page as the starting point before starting the MCP Agent for the first time to confirm that all required communication settings are in place.
- Use this page to understand which configuration values directly affect agent-to-SMANetCom connectivity and require matching entries in the Enterprise Manager.

The agent configuration file contains information needed to set the correct options for communication with SMANetCom and to activate optional features. After installation, review the configuration file before starting the MCP Agent.

:::info Note 

If upgrading to MCP LSAM 18.00.00 or higher from a version earlier than 18.00.00, you MUST access the SMAMGR window to update the new configuration fields on the GEN screen.
 
:::


:::info Note 

The configuration file must reside on the same family and under the same usercode as the MCP Agent.

:::

The following settings are critical to the operation of the MCP Agent with OpCon:

* OpCon port: This value controls communication between the agent and SMANetCom. The value for this setting and the value for the Socket Number on the Machines screen in the Enterprise Manager must match.
* Hostname alias: The default value of ```<None>``` for the hostname causes the agent to automatically look up and use the BNA hostname. The BNA hostname (or a configured hostname alias) is required when setting up the Machine in the Enterprise Manager. The BNA hostname is displayed when the SYSTEM user is logged on to the MARC Main Menu screen. At the bottom of the window, there is a string with the following syntax: Window MARC/```<window number>``` at ```<hostname>```. Make note of the hostname for use in the Enterprise Manager if you are not supplying a hostname alias.
* Max number concurrent jobs: This value determines the maximum number of jobs the agent is allowed to process concurrently. The maximum allowed value is 500.