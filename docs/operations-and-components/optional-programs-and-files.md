# Optional Programs and Files

The programs listed in this section are installed with the MCP LSAM. The files listed below each program are created as a result of executing the feature, or are used by the feature.

### MCP LSAM Optional Programs

| Optional Program | Short Description |
| ---------------- | ----------------- |
| *SMA/ANNOUNCE/xxx | - This program is used to notify the LSAM to monitor the process which initiated the *SMA/ANNOUNCE program, and to report the completion status of the process. <br></br> - This program is only used for processes started outside of OpCon. <br></br> - For more information, refer to [External Jobs Tracking](/additional-features/lsam-features/external-jobs-tracking). |
| *SMA/COMMAND | - This program is used to forward commands to specified processes on the MCP system. <br></br> - The process may be the MCP itself or any other process in an active or waiting state. <br></br> - For more information, refer to [Command-line Interface Utility](/additional-features/lsam-features/command-line-interface-utility). |
| *SMA/DISPLAY/HANDLER/xxx | This program handles the Automated Response feature. Automated Response allows the MCP LSAM to respond to messages displayed on the MCP console. For more information, refer to [Automated Response](/additional-features/lsam-features/automated-response). |
|*SMA/OBJ/CONVERT/PRINT <br></br> *SMA/WFL/CONVERT/PRINT | A utility used to convert an MCP BACKUPPRINTER file to an ASCII text file prior to transferring the ASCII file to a non-MCP machine. For more information, refer to Using [*SMA/WFL/CONVERT/PRINT (MCP Print File Conversion)](/additional-features/utilities/sma-wfl-convert-print). |
| *SMA/EVENTGEN/xxx | - This utility program is inserted into a WFL and is used to forward external events to the SAM-SS. <br></br> - The program accepts three parameters: the SAM ID, the SAM external token, and the external event to be forwarded. <br></br> - For more information, refer to [External Event Interface Library](/additional-features/lsam-features/external-event-interface-library). |
| *SMA/FILE/MONITOR/xxx | File Monitor receives notification that user-specified files have been altered and sends external events to the SAM and supporting services, or forwards selected MCP commands to the MCP when these files meet a defined criterion. For more information, refer to [File Monitor](/additional-features/lsam-features/file-monitor). |
| *SMA/FTAGENT/xxx | This program is one of the components of SMA File Transfer. |
| *SMA/FTHANDLER/xxx | This program is one of the components of SMA File Transfer. Up to 9 SMA File Transfer handlers may be configured. | 
| *SMA/FTHANDTLS/xxx | The SMA File Transfer handler sends the MCP source file to the destination platform via the FTSERVERTLS (the FTSERVER program that is using TLS). Up to 9 SMA File Transfer handlers may be configured to permit multiple concurrent outgoing transfers. |
| *SMA/FTSERVER/xxx | The SMA File Transfer server handles communication between SMA File Transfer agents and the MCP handlers. The unique port number configured for the SMA File Transfer server must match the FT server port number defined on the Enterprise Manager. |
| *SMA/FTSERVERTLS | The SMA File Transfer server which handles communication using TLS between SMA File Transfer agents and the MCP handlers. The unique port number configured for use by the SMA File Transfer TLS server must match the FT TLS server port number defined on the Enterprise Manager. |
| *SMA/JORS/xxx | The JORS program retrieves and forwards the printed output from the selected job to the Enterprise Manager. For more information on JORS, refer to Job Output Retrieval System. |
| *SMA/MSGIN/DETECTOR/xxx | This program detects and processes MSGIN data. For more information on MSGIN, refer to [MSGIN](/additional-features/lsam-features/msgin). |
| *SMA/OBJ/CHECK/MIX | This program queries the Waiting or Scheduled mix and returns a task value indicating whether processes were found. If processes were found, a report is generated. Refer to [Using *SMA/WFL/CHECK/MIX](/additional-features/utilities/sma-wfl-check-mix). |
| *SMA/OBJ/OPS/MONITOR/xxx | This program is an interface between the *SMA/WFL/OPS/MONITOR and the MCP. For more information on utilities, refer to [Operations Monitor](/additional-features/lsam-features/operations-monitor). |
| *SMA/RESOURCE/MONITOR/xxx | This program monitors system messages, CPU and disk utilization, and file status notifications if configured by the user. For more information on utilities, refer to [Resource Monitor](/additional-features/lsam-features/resource-monitor). |
| SMASUP | This program gathers detailed debug information into one file for analysis by SMA Technologies. For more information on the Data Collector for MCP, refer to [Data Collector for MCP (SMASUP)](/additional-features/lsam-features/data-collector-for-mcp). |
| *SMA/SURROGATE/xxx | This program monitors and reports on external (tracked or adopted) jobs. For more information on Tracking External Jobs, refer to [External Jobs Tracking](/additional-features/lsam-features/external-jobs-tracking). |
| *SMA/SYNTAX/CHECK | This utility program is used to validate the syntax of various definitions files created by the user and utilized by the LSAM and utilities. |
| *SMA/WFL/CHECK/MIX | This utility WFL is used to interrogate the presence of entries in the Waiting or Scheduled mix. For more information, refer to Using *SMA/WFL/CHECK/MIX. |
| *SMA/WFL/FILECHECK/xxx | This WFL reports the presence/absence of a file. For more information on utilities, refer to Utilities. |
| *SMA/WFL/OPS/MONITOR/xxx | This WFL enables the user to take action based upon the value of selected CPU usage metrics or available disk space. For more information on utilities, refer to [Utilities](/additional-features/utilities/mcp-lsam-utilities). |
| *SMA/WFL/PROCESSCHECK/xxx | This WFL reports the presence/absence of a process in the active or waiting mix. For more information on utilities, refer to [Utilities](/additional-features/utilities/mcp-lsam-utilities). | 
| *SMA/RESOURCE/CHECK/xxx | This program is an interface between the *SMA/WFL/FILECHECK and *SMA/WFL/PROCESSCHECK WFLs. For more information on utilities, refer to [Utilities](/additional-features/utilities/mcp-lsam-utilities). |

### *SMA/FILE/MONITOR Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| *SMA/FILEMON/DEFS/xxx | Y | - This user-created file contains the files to monitor and the conditions for which each file should be monitored. <br></br> - The file also includes the actions to perform when a condition is satisfied. |
| ```<Monitored file>``` | N | Interrogation of certain file attributes requires that the file be logically assigned first. ```<Monitored File>``` is a dummy file used for this logical assignment. |
| *SMA/FILEMON/CONTROL/FILE/xxx | Y | This file contains the timestamp from the most recent file close notification. The timestamp is used at BOJ to determine whether any of the monitored files have been altered since the previous iteration of File Monitor. |
| *SMA/FILEMON/HISTORY/xxx | Y | This file contains a list of files for which the PRESENT condition has been processed. If a file is deleted, its corresponding entry within this file is deleted. | 
| *BD/…../DEBUG_FILE> | Y | - This print file contains errors detected in the *SMA/FILEMON/DEFS file during the editing process. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. | 

### *SMA/DISPLAY/HANDLER Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
*SMA/DISPLAYS/xxx | Y | - This user-modified file contains the displays for which to monitor and the associated action to be taken by the SAM and supporting services or by the MCP. <br></br> - This is referred to as the "global displays file." <br></br> - The release container includes a template for this file. |
| *SMA/DISPLAYS/xxx/```<WFL file name>``` | Y | - This user-created file contains the displays for which to monitor the specified job and the associated action to be taken by the SAM and supporting services or by the MCP. <br></br> - This is referred to as the "job-specific displays file". |
| *SMA/DISPLAYS/SYSMSG | Y | This user-created file contains the messages, displayed by non-OpCon jobs, for which to monitor. This file also contains action(s) to be taken by the SAM and supporting services or by the MCP when the message is displayed. |
| TEMP/SMA/DISPTOKENS | N | This temporary file is used to alphabetize display tokens in the global displays file. |
| *BD/…../PRINT-FILE> | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/EVENTGEN Associated Files

| External File Title | Permanent? | Description | 
| ------------------- | ---------- | ----------- |
| BD/…../DEBUGPRT | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/FTAGENT

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| FTPORT | N | This port is used to communicate between *SMA/FTAGENT and the File Transfer server. |
| TEMP/SMAFT/```<SAM job id>``` | N | This temporary file is used to store the transferred data prior formatting. |
| *TEMP/SMAFTPARMS/```<SAM job id>``` | N | This file is used to pass transfer data from the LSAM to the SMA File Transfer Agent. |
| User-defined | Y | This is the formatted file received via SMA File Transfer. The name of this file is specified on the File Transfer Job Details as the Destination File Name. |
| User-defined/```<backup suffix>``` | Y | This is the backed up copy of the received file. The name is derived by appending the backup suffix specified in the configuration file to the file name specified for the Destination File Name on the File Transfer Job Details. |
| *BD/…/…/PRT_FTAGENT | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/JORS Associated Files

| External File Title | Permanent | Description |
| ------------------- | --------- | ----------- |
| ```<Requested print file>``` | N | This file is used to format the requested print file. |
| TEMP/SMA/```<10-digit SAM job id>``` | N | This file is used to accumulate print file names. |
| *BD/…../SMA_JORS_DEBUG | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/MSGIN/DETECTOR Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| *MSGIN/= | N | User-created files containing an external event, OpCon User Login ID, and events external token to be forwarded to the SAM and supporting services. |
| *BD/…../DEBUG_PRT | Y | - This print file contains errors and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/OBJ/OPS/MONITOR Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| (uc)SMA/OPSMON/REPORT/xxx | Y	| This optional file is created by setting SW8 = TRUE when running *SMA/OBJ/OPS/MONITOR in the *SMA/WFL/OPS/MONITOR. It contains a cumulative listing of the inquiries and results processed by the Operations Monitor. By default, this file is not created. |
| *BD/…../DEBUGPRT | Y | - This print file contains error and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/RESOURCE/MONITOR Associated Files

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| *SMA/DISPLAYS/SYSMSG | Y | This file is maintained by the user and contains definitions of messages for which to monitor and actions to be performed when the defined messages are displayed by processes initiated outside OpCon. |
| SMA/FILEMON/DEFS/xxx | Y | This file is maintained by the user and contains definitions of files and conditions for which to monitor as well as actions to be performed when the target condition has been achieved. |
| SMA/PERFMON/DEFS/xxx | Y | This file is maintained by the user and contains definitions of performance metrics for which to monitor and actions to be performed when the target value has been achieved. |
| *BD/…../DEBUG_FILE | Y | - This print file contains error and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### *SMA/SURROGATE Associated Files

| Exernal File Title | Permanent? | Description |
| ------------------ | ---------- | ----------- |
| *SMA/TRACKING/ADOPT/FILE/xxx | Y | This file contains job status information for active, external tracked/adopted jobs. |
| SMAMIXLISTxxx	| N | This port file is used to communicate between *SMA/ALGOLPROCS/xxx and *SMA/SURROGATE/xxx. |
| *BD/…../SURROGATEDBG | Y | - This print file contains error and debug information. <br></br> - The name of this file may differ depending on the site print defaults and/or the use of the BDNAME task attribute. |

### SMASUP

| External File Title | Permanent? | Description |
| ------------------- | ---------- | ----------- |
| SMASUPTXT | Y | This ASCII text file contains the SMA file and process information. |
| SMASUPFILCON | Y | This container file contains several critical MCP LSAM files. |
| SMASUPPRTCON | Y | This container file contains the MCP LSAM debug print files. |












