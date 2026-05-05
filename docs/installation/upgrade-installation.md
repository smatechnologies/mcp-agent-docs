---
title: Upgrade Installation
description: "Safely stop the running MCP LSAM, back up files, and run the *SMA/INSTALL upgrade to move to a new LSAM version."
tags:
  - Procedural
  - System Administrator
  - Installation
  - Agents
---

# Upgrade Installation

## What is it?

This page describes the ordered steps for upgrading an existing MCP Agent installation, covering how to quiesce active jobs, stop agent components, remove checkpoint files, and run the installer in upgrade mode. It also addresses the additional configuration migration steps required when upgrading from a version earlier than 18.00.00.

- Use this page when upgrading from any prior MCP Agent version to ensure active jobs complete, external events are not lost, and checkpoint files are cleanly removed before the new version is installed.
- Use this page to understand the configuration file migration steps required when crossing the 18.00.00 version boundary.

To perform an upgrade installation of the MCP Agent, follow the procedures in this section.

## Complete Job and Event Processing

To allow all active jobs to complete and outstanding external events to be processed, complete the following steps:

1. Under the Operation topic, select **Machine Status** below the Navigation tab on the Enterprise Manager screen.

2. Confirm the number of Running Jobs is 0 for the MCP machine.

3. Wait approximately two minutes to allow any outstanding external events to be forwarded to the SAM and supporting services.

:::caution

Any external events generated after the machine is marked down and before the new version of the agent is running may be lost. This depends on the current agent version and the changes in structure of the file in which these events are stored before being forwarded to the SAM and supporting services.

:::

4. Right-select the Machine name, then select **Stop Communication**.

5. Check the current agent version:

    a. From the Home position of the LSAM window, type VERSION. Transmit the line -or-
    
    b. For agent version 18.00.00 and up, perform the STATUS inquiry from the Main Menu of the SMA/MANAGER program. The RELEASEID is displayed on the STATUS screen.
    
    c. Note the version for reference during the upgrade installation.

## Stop the Agent and Resource Monitor

:::info Note 

Please allow up to five minutes for the components to shut themselves down.

:::

1. Access *SMA/MANAGER via ?ON SMAMGRxxx.

2. From the Main Menu, select STOPLSAM.

3. From the Main Menu, select STOPRM, if the Resource Monitor is active.

For the previous procedure, refer to [Stop the LSAM and Resource Monitor](../reference-information/legacy#stop-the-mcp-agent-and-resource-monitor) in the Legacy Information topic.

## Remove Checkpoint Files and Perform Upgrade

1. Remove ```*SMA/CP/MCS/= ON <diskpack>```.

2. Use the ```*SMA/INSTALL``` program to perform the upgrade.

## Configure the Agent

If upgrading from a version earlier than 18.00.00 to version 18.00.00 or higher, complete the following steps:

1. Run ```*SMA/CONFIG/xxx``` and capture a screenshot or print the configuration values.

2. Next, remove the ```*SMA/CONFIG/FILE/xxx```.

:::info Note

 This is necessary due to the various configuration file formats that have existed over multiple releases.

:::

3. Run the SMA/MANAGER program to populate the agent configuration file with the values you captured, as well as any additional fields, before starting the agent. Access all four agent configuration screens. For new fields, refer to [SMAGEN (GEN option)](../configuration/general-lsam-configuration) in the MCP LSAM Configuration.

:::info Note 

For versions prior to MCP LSAM 19.01.00, it is also necessary to exit the Manager program after updating the configuration fields to save the new values. Then, you may run the Manager program to perform all other functions.

:::
