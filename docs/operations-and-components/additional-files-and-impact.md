---
title: Additional Files and Impact
description: "Reference the supplemental MCP LSAM files, sample programs, and the COMS and IDC entities that are created or modified during installation."
tags:
  - Reference
  - System Administrator
  - Agents
  - Installation
---

# Additional Files and Impact

## What is it?

This page lists the additional files installed with the MCP Agent—including sample source programs, WFL templates, and utility definitions files—as well as the COMS and IDC entities that are created or modified as a side effect of the installation. It provides the file title, permanence, and a description of each item's purpose.

- Use this page to understand which sample and utility files are available after installation, such as the ALGOL and COBOL source programs for external event forwarding and the sample definitions files for file and performance monitoring.
- Use this page when verifying post-installation results to confirm that COMS entities (agent window, SMAMGR window, program, and agenda) and the IDC MCS declaration for *SMA/MCP/INTERFACE/xxx were created correctly.

The programs listed in this section are installed with the MCP Agent, or are affected by agent configuration. During initial installation, COMS and IDC are modified to accommodate the MCP Agent.

### Additional MCP Agent Files

| Program | External File Title | Permanent? | Description |
| ------- | ------------------- | ---------- | ----------- |
| ```<None>``` | *SMA/ANNOUNCE/ALGOL | Y | This is the sample ALGOL source program for requesting the agent to track a job initiated outside the scope of OpCon. |
| | *SMA/GENERICP | Y | This program validates the installation and base functionality of the agent. |
| | SMA/SAMPLE/DISPLAYS/SYSMSG | Y | This is the sample definitions file for system message monitoring. |
| | SMA/SAMPLE/FILEMON/DEFS | Y | This is the sample definitions file for file monitoring. |
| |  SMA/SAMPLE/PERFMON/DEFS | Y | This is the sample definitions file for CPU and disk space usage monitoring. |
| |  SMA/SRC/MULTI/EVENT/ALGOL | Y | This is the sample ALGOL source program for forwarding multiple external events to SAM and supporting services. |
| | SMA/SRC/MULTI/EVENT/C85 | Y | This is the sample COBOL 85 source program for forwarding multiple external events to SAM and supporting services. |
| ```<None>``` | *SMA/WFL/COMMAND/xxx | Y | - This is the sample WFL for forwarding commands to specified processes on the MCP system. <br></br> - The file demonstrates the use of the *SMA/COMMAND program. <br></br> - For more information, refer to Command-line Interface Utility.
| ```<None>``` | *SMA/WFL/EVENTGEN/xxx | Y | - This is the sample WFL for forwarding external events to the SAM and supporting services. <br></br> - The file demonstrates the use of the *SMA/EVENTGEN program. <br></br> - For more information, refer to Using *SMA/EVENTGEN.
| ```<None>``` | *SMA/WFL/FILECHECK/xxx | Y | - This is the sample WFL for interrogating the existence of a file (or group of files). <br></br> - The file demonstrates the use of the *SMA/RESOURCE/CHECK program. <br></br> - For more information, refer to Using *SMA/WFL/FILECHECK.
| ```<None>``` | *SMA/WFL/PROCESSCHECK/xxx | Y | - This is the sample WFL for interrogating the existence of a process (or group of processes) in the mix. <br></br> - The file demonstrates the use of the *SMA/RESOURCE/CHECK program. <br></br> - For more information, refer to Using *SMA/WFL/PROCESSCHECK. |
| ```<None>``` | *SMA/WFL/SMASUP | Y | - Sample WFL for running the debug data collection utility, SMASUP. <br></br> - The file demonstrates the use of the *SMASUP program. <br></br> - For more information, refer to Problem Resolution and Debugging. |
| ```<None>``` | *SMA/RESOURCE/CHECK/xxx | Y | - This utility program is used to interrogate the existence of files or processes. <br></br> - The use of this file is demonstrated in the *SMA/WFL/FILECHECK and *SMA/WFL/PROCESSCHECK WFLs. |
| ```<None>``` | *SMA/WFL/OPS/MONITOR/xxx | Y | - This WFL is used for interrogating the value of a performance metric. This WFL accepts various parameters used to determine success/failure and optional parameters for the OpCon event to be generated upon success/failure. <br></br> - The file demonstrates the use of the *SMA/RESOURCE/CHECK program. |
| ```<None>``` | *SMA/OBJ/OPS/MONITOR/xxx | Y | - This utility program is used to interrogate the value of specified performance metrics. <br></br> - The use of this file is demonstrated in the *SMA/WFL/OPS/MONITOR WFL. |
| COMS | | Y | The following entities are defined to COMS: agent window, SMAMGR window, SMAMGR program, and SMAMGR agenda. |
| IDC | | Y | *SMA/MCP/INTERFACE/xxx is declared as an MCS. |