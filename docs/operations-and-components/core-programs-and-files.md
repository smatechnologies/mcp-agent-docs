---
title: Core Programs and Files
description: "Reference the core MCP LSAM programs installed by *SMA/INSTALL and the permanent and temporary files each program uses or creates."
tags:
  - Reference
  - System Administrator
  - Agents
  - System Configuration
---

# Core Programs and Files

## What is it?

This page lists each core MCP Agent program—including *SMA/ALGOLPROCS, *SMA/COMM, *SMA/MANAGER, *SMA/MCP/INTERFACE, and *SMA/TCPIP—along with the permanent and temporary files associated with each program. It describes the purpose of each file and whether it persists between agent cycles.

- Use this page to identify which files are created or used by each agent core component, which is essential when diagnosing issues or cleaning up files before an upgrade.
- Use this page as a reference for understanding the agent's data flow, such as how inbound and outbound message files relate to the *SMA/ALGOLPROCS and *SMA/COMM programs.

The programs listed in this section are installed with the MCP Agent. The files listed below each program are either installed with the agent or created as a result of agent execution. Each file or entity listed for a program is in use or is affected by the agent. Select the link for more information on the program.

### MCP Agent Core Programs

| Core Program | Short Description |
| ------------ | ----------------- |
| \*SMA/ALGOLPROCS/xxx | - The library interface for submitting external events to the agent by COBOL/ALGOL programs including *SMA/EVENTGEN/xxx. <br></br> - This library also contains common procedures used by the agent processes and utilities. |
| \*SMA/COMM/xxx | - This program starts and stops the agent components. <br></br> - This program also maintains records in the *SMA/TRACKING/FILE/xxx. |
| \*SMA/CONFIG/xxx | To view information about this program, refer to *SMA/CONFIG in the Legacy Information topic. |
| \*SMA/MANAGER | - The SMA/MANAGER program provides a single interface for performing configuration and operations tasks related to the MCP Agent. <br></br> - It replaces the *SMA/CONFIG program, and reduces the MCP-specific knowledge required to perform routine operational tasks. |
| \*SMA/MCP/INTERFACE/xxx | - A module responsible for starting and monitoring a job. <br></br> - A new *SMA/MCP/INTERFACE/xxx is created for each job's WFL compile under the job's specified Usercode. |
| \*SMA/TCPIP/xxx | The TCPIP program handles communication between the agent and SMANetCom. |

### *SMA/ALGOLPROCS Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- | 
| SMA/CONFIG/FILE/xxx | Y | This file contains the agent's configuration values. |
| SMAMIXLISTxxx | N | This port file is used to communicate between \*SMA/ALGOLPROCS/xxx and \*SMA/SURROGATE/xxx. |
| \*SMA/INBOUND/ADOPT/FILE/xxx | Y | This file contains SMANetCom and LSAM adoption messages waiting to be processed by \*SMA/SURROGATE/xxx. |
| \*SMA/INBOUND/FILE/xxx | Y | This file contains SMANetCom messages waiting to be processed by the agent. |
| \*SMA/INBOUND/ADOPT/FILE/TEMP/xxx | N | This file is used to reorganize \*SMA/INBOUND/ADOPT/FILE/xxx. |
| \*SMA/INBOUND/FILE/TEMP/xxx | N | This file is used to reorganize \*SMA/INBOUND/FILE/xxx. |
| \*SMA/OUTBOUND/FILE/xxx | Y | This file contains external events and status messages waiting to be forwarded to SMANetCom. |
| \*SMA/OUTBOUND/FILE/TEMP/xxx | N | This file is used to reorganize \*SMA/OUTBOUND/FILE/xxx. |
| \*SMA/DISPMSG/FILE/xxx | Y | This file contains display messages waiting to be processed by the \*SMA/DISPLAY/HANDLER/xxx. |
| \*SMA/DISPMSG/FILE/TEMP/xxx | N | This file is used to reorganize \*SMA/DISPMSG/FILE/xxx. |
| \*SMA/FILE/LIST/xxx | Y | This file contains a list of files waiting to be processed by the \*SMA/FILE/MONITOR/xxx. |
| \*SMA/FILE/LIST/TEMP/xxx | N | This file is used to reorganize \*SMA/FILE/LIST/xxx. |
| \*BD/…../DEBUGPRT | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/COMM Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| \*SMACOMPORTxxx | N | This port file is used to communicate between \*SMA/MCP/INTERFACE/xxx and \*SMA/COMM/xxx. |
| \*SMA/TRACKING/FILE/xxx | Y | This file contains job status information for OpCon jobs. |
| \*SMA/RESTART/FILE/xxx | Y | This file is used to determine whether \*SMA/COMM/xxx went to an orderly EOJ during the previous cycle. |
| \*SMA/COMM/xxx | N | This file is used at agent initiation to determine whether \*SMA/COMM/xxx is already running. |
| \*BD/…../COMM-PRINT-FILE | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### SMA/CONFIG

To view information about this program, refer to [*SMA/CONFIG](../reference-information/legacy#smaconfig) in the Legacy Information topic.

### *SMA/MANAGER Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| \*SMA/CONFIG/FILE/xxx | Y | This file contains the agent configuration information. |
| \*SMA/CONFIG/AUDIT/xxx | Y | This file contains an audit history of changes to the agent configuration file |
| \*SMA/DISPLAYS/… <br></br> \*SMA/DISPLAYS/SYSMSG/xxx <br></br> \*SMA/FILEMON/DEFS/xxx <br></br> \*SMA/PERFMON/DEFS/xxx | N | These are the definitions files used to configure the entities to be monitored and the actions to take when the condition occurs. |
| \*BD/…../LINE | Y | This print file contains debug entries. |

### *SMA/MCP/INTERFACE Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| SMACOMPORT/xxx | N | This port file is used to communicate between *SMA/MCP/INTERFACE/xxx and *SMA/COMM/xxx. |
| *SMA/CP/MCS/xxx/1 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/2 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/3 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/4 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/5 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/6 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/7 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *SMA/CP/MCS/xxx/8 | Y | This is one of eight checkpoint files used to save internal arrays. |
| *TEMP/SMA/```<SAM job id>``` | N | This file is used to gather names of print files generated by an OpCon job. |
| *TEMP/SMAFTPARMS/```<SAM job id>``` | N | This file is used to pass SMA File Transfer data to the SMA File Transfer Agent program. |
| *BD/…../PRINTFILE | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |
| ```<WFL job filename>``` | N | This file is used to validate the residence and type of WFL files before submitting the WFL for compilation. |

### *SMA/TCPIP Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| SAMPORT/xxx | N | This port file is used to communicate with SMANetCom. |
| *BD/…../PRT_TCPIP | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |







