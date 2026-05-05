---
title: New Installation
description: "Run the *SMA/INSTALL program, define the LSAM to IDC, and complete initial configuration for a first-time MCP LSAM installation."
tags:
  - Procedural
  - System Administrator
  - Installation
  - Agents
---

# New Installation

## What is it?

This page walks through the complete process for installing the MCP Agent for the first time, including running `*SMA/INSTALL`, defining the agent as an MCS in IDC, and opening the SMA/MANAGER program for initial configuration. It covers both CANDE and MARC menu methods for each step.

- Use this page when the MCP Agent has never been installed on the target machine and a clean first installation is required.
- Use this page to ensure the agent is correctly registered with IDC so that the MCP Agent interface can function as a properly declared MCS within the environment.

If the MCP Agent has not been installed on the machine, follow the procedures in this section for the first installation.

:::warning 

Before proceeding, check the FAMILY statement. If it does not say ```FAMILY DISK = <lsam pack> ONLY```, you will be given the opportunity to correct it during the installation, and must do so before continuing.

:::

## Run *SMA/INSTALL

1. Choose one of the following two options to run the ```*SMA/INSTALL/nnnnnn/LEVELn``` program:

    a. From CANDE, type ```RUN *SMA/INSTALL/nnnnnn/LEVELn```. Transmit.

    b. On the MARC main menu screen, go to the Choice line. Type ```RUN *SMA/INSTALL/nnnnnn/LEVELn```. Transmit.

2. Select INSTALL as the type of installation.

3. Follow the remaining prompts.

If the ```*SMA/INSTALL/nnnnnn``` program is not correctly named, the install/upgrade will not be performed, and this error message will be displayed:

"Invalid version number. Aborting install/upgrade." To recover from this, name the ```*SMA/INSTALL/nnnnnn``` program correctly and rerun it.

For a list of files installed with the MCP Agent, refer to [MCP LSAM Components](../operations-and-components/core-programs-and-files).

## Define the Agent to IDC

### Obtain the DCPREFIX

You will need to know the DCPREFIX for the NIF file. To obtain the DCPREFIX, use the following information:

By default, the NIF file is called ```*SYSTEM/DATACOMINFO ON DISK``` (*SYSTEM ON DISK as the full DCPREFIX). In some cases, however, customers change this to another prefix.

For example, ```(USERCODE)CUSTOMER/DATACOMINFO ON PROD```. To obtain this information, use the ID command from the Action line of the MARC Main Menu to get the NIF prefix.

The following example shows the response of the ID command. This response indicates that `*SYSTEM ON DISK` is the "full DCPREFIX" when running IDC.

```

Response returned at 08:20:05

NIF: SYSTEM

NIF TO BE: SYSTEM

DC AUDIT OPTIONS: NONE.

MAXPSEUDO: 0

NEXT MAXPSEUDO: 0

NUMBER OF PSEUDOS IN-USE: 100

```

### Define the Agent to IDC

To define the agent to IDC, complete the following steps:

1. Choose a or b:

    a. On the MARC main menu screen, go to the Choice line. Type UTIL IDC. Transmit the line - or -

    b. Enter the command RUN SYSTEM/IDC. Transmit the line.

2. On the Welcome to IDC screen, type the DCPREFIX.


:::info Note 

The DCPREFIX is the leading node name(s) for the DATACOMINFO file for IDC without the last node (i.e., *SYSTEM). If the machine has a configuration description in the form of a Network Information File (NIFII), a DATACOMINFO file with the same prefix (as the NIFII file) is automatically built from the NIFII. Building occurs the first time the DATACOMINFO prefix is referenced by the operating system, IDC, or DCSTATUS. Remove and rebuild the corresponding DATACOMINFO file to update the configuration with any subsequent changes to the NIFII.

:::

3. On the Choice line, type CREATE. Transmit the line.

4. On the Choice line, type MCS. Transmit the line.

5. In the Name of MCS to be created field, type *SMA/MCP/INTERFACE/xxx.

6. Transmit the screen.

7. In the Familyname field, type ```<PACK NAME>```.

:::info Note 

```<PACK NAME>``` is the name of the family on which the agent is installed (e.g., DISK).

:::

8. On the Action line, type DONE. Transmit the screen.

9. To return to the main IDC screen, go to the Action line. Type HO. Transmit the line.

10. To exit the IDC Utility, go to the Choice line. Type BYE. Transmit the line.

11. Type YES and transmit to make your changes permanent.

12. To return to the MARC main menu, go to the Action line. Type HO. Transmit the line.

## Configure the Agent

Use the SMA/MANAGER program to configure the agent. To begin using the MCP Agent, refer to [MCP LSAM Configuration](../configuration/mcp-lsam-configuration).