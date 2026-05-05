---
title: Automated Installation/Upgrade
description: "Understand what the *SMA/INSTALL program does automatically during a new installation or upgrade of the MCP LSAM."
tags:
  - Conceptual
  - System Administrator
  - Installation
  - Agents
---

# Automated Installation/Upgrade

## What is it?

This page describes the actions performed automatically by the `*SMA/INSTALL` program during a new installation or an upgrade, including backing up existing files, configuring COMS entities, setting program privileges, and establishing the agent as a system library.

- Use this page to understand what `*SMA/INSTALL` does on your behalf so you can verify the environment is correctly set up after the automated steps complete.
- Use this page as a reference when troubleshooting installation results, since it details which files are backed up, which are removed, and which COMS entities are created or updated.

The `*SMA/INSTALL` program automates most of the steps required for an installation or upgrade. To run `*SMA/INSTALL`, use a privileged MCP usercode obtained from the site administrator. This usercode must have as its ONLY family the same family on which the agent will reside. `*SMA/INSTALL` performs the following actions:

* Prompts the user for the following required environmental information:

:::info Note

With each prompt, the user is given the opportunity to abort the process. The installation/upgrade process does not start until all required information has been gathered.

:::

* The type of installation: INSTALL or UPGRADE.
* The family on which the agent will reside. The user's FAMILY statement is retrieved and analyzed to determine if it is ```<LSAM family>``` ONLY. If it is not, the user is asked to allow the SMA/INSTALL program to modify the FAMILY statement for the duration of the installation/upgrade. If permission is not granted, the SMA/INSTALL program exits without performing the install/upgrade.
* The three-character agent instance identifier (or "NONE").

* If "UPGRADE" is specified, performs the following procedures:
    * Backs up the current agent programs, agent utility WFLs, and agent files.
    * The names of the backed up files are preceded with a node of SAVE (e.g., the backup saves ```*SMA/CONFIG/FILE``` as ```*SAVE/SMA/CONFIG/FILE```).
    * Removes the checkpoint, tracking, and message persistence files.
    * Removes the SMA library as a system library.
    * Restores the previously backed-up ```*SMA/CONFIG/FILE```, ```*SMA/FILEMON/DEFS```, ```*SMA/DISPLAYS```, ```*SMA/DISPLAYS/SYSMSG```, and ```*SMA/PERFMON/DEFS``` files.

* Unwraps the release container and names the files using the specified family and agent instance identifier.
* Makes the ```*SMA/ALGOLPROCS/xxx```, ```*SMA/COMMAND/xxx```, ```*SMA/RESOURCE/MONITOR/xxx```, ```*SMA/SURROGATE/xxx```, and ```*SMA/ANNOUNCE/xxx``` programs privileged.
* Makes the ```*SMA/ALGOLPROCS/xxx``` library security PUBLIC IO.
* Establishes ```*SMA/ALGOLPROCS/xxx``` as a system library.
* Sets up the SMAMGR program, window, and agenda in Transaction Server (COMS). The entities are named ```SMAMGRxxx```, where ```xxx``` is the 1-to-3-character agent instance identifier.

* If "INSTALL" is specified, performs the following procedures:
    * Sets up the LSAM window in Transaction Server (COMS). The window is named ```LSAMxxx```, where ```xxx``` is the 1-to-3-character agent instance identifier.
    * Sets up the SMAMGR program, window, and agenda in Transaction Server (COMS). The entities are named ```SMAMGRxxx```, where ```xxx``` is the 1-to-3-character agent instance identifier.
    * Prompts the installer to declare the ```*SMA/MCP/INTERFACE/xxx``` as an MCS using IDC.