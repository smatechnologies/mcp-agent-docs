---
title: Configuration Settings
description: "Access the SMA/MANAGER program and navigate its configuration screens to modify MCP LSAM settings."
tags:
  - Procedural
  - System Administrator
  - System Configuration
  - Agents
---

# Configuration Settings

## What is it?

This page explains how to open the SMA/MANAGER program and use its GEN, COMM, VAR, and OPT screens to review and modify agent configuration values. It notes that most configuration fields are dynamic, with the exception of the maximum concurrent jobs setting, which requires a full MCP Agent restart to take effect.

- Use this page when you need to change any agent configuration value and want to know the correct entry point and menu options within SMA/MANAGER.
- Use this page to understand the distinction between dynamic configuration changes and the restart-required "Max number concurrent jobs" field before making modifications in a production environment.

## Run the Manager Program

1. From the home position of any MCP window, type ?ON SMAMGRxxx and transmit.

2. You will be presented the Main Menu. To modify the agent configuration, use choices GEN, COMM, VAR, and OPT.

:::info Note

Most of the configuration fields are dynamic; however, each agent component must be notified that the configuration file has changed in order to effect the changes. The "Max number concurrent jobs" variable is never changed dynamically. To implement a new max jobs count, stop and restart the MCP Agent to apply the new max job count settings. For more information on applying changes to all other configuration values, refer to [Dynamic LSAM Configuration](../additional-features/lsam-features/dynamic-lsam-configuration).

:::

To view the previous procedure, refer to [Run the Configuration Program](../reference-information/legacy#run-the-configuration-program) in the Legacy Information topic.

## Configuration Settings

The next several topics describe the fields found on the GEN, COMM, VAR, and OPT screens of the SMA/MANAGER Main Menu screen.

To view the previous settings, refer to [Configuration Settings](../reference-information/legacy#configuration-settings) in the Legacy Information topic.