# LSAM Feature Overview

The MCP LSAM has a variety of unique features and utilities. In this section, these tools have been thoroughly defined so that you may determine which best suit(s) your needs.

:::info Note

If you are already familiar with the MCP LSAM features, you may bypass this section and go directly to the section for the feature that you wish to use.

:::

## Monitor for Files Utilization

There are multiple tools available for monitoring files and directories on the MCP platform. The table identifies these tools.

| Tool | Description |
| ---- | ----------- |
| File Monitor | - This tool allows you to monitor continuously, and independently of any OpCon schedule. <br></br> - With File Monitor, you can send events to OpCon or take action directly on the MCP platform. <br></br> - File Monitor runs independently of the LSAM-based software and is not scheduled via OpCon, an advantage for those sites which utilize task-based OpCon licensing. <br></br> - For more information, refer to [File Monitor](../additional-features/lsam-features/file-monitor). |
| FILECHECK | - This tool allows you to check for the presence or absence of a particular file or set of wildcarded file names in order to satisfy a requirement for an OpCon job or schedule. <br></br> - FILECHECK's completion status depends on whether the requirements are satisfied. It may be used as a prerun, or as a job upon which other jobs are dependent. This allows you to control the processing path and to be assured that file dependencies are met before downstream processing occurs. <br></br> - FILECHECK runs as an OpCon job and does not require additional configuration or definition files to implement. <br></br> - For more information, refer to [Using *SMA/WFL/FILECHECK](../additional-features/utilities/sma-wfl-filecheck). |
| FILECOUNT	| - This tool allows you to check for the presence or absence of a minimum or maximum number of particular files or set of wildcarded file names in order to satisfy a requirement for an OpCon job or schedule. <br></br> - FILECOUNT's completion status depends on whether the requirements are satisfied. It may be used as a prerun, or as a job upon which other jobs are dependent. This allows you to control the processing path and to be assured that file dependencies are met before downstream processing occurs. <br></br> - FILECOUNT runs as an OpCon job and does not require additional configuration or definition files to implement. <br></br> - For more information, refer to [Using *SMA/WFL/FILECOUNT](../additional-features/utilities/sma-wfl-filecount). |

## Monitor Resource Utilization

| Tool | Description |
| ---- | ----------- |
| Resource Monitor | - This tool allows you to monitor continuously, and independently of any OpCon schedule. <br></br> - With Resource Monitor, you can send events to OpCon or take action directly on the MCP platform. <br></br> - Resource Monitor runs independently of the LSAM-based software and is not scheduled via OpCon, an advantage for those sites which utilize task-based OpCon licensing. <br></br> - For more information, refer to [Resource Monitor](../additional-features/lsam-features/resource-monitor). |
| PROCESSCHECK | - This tool allows you to check for the presence or absence of a particular process or set of wildcarded process names in order to satisfy a requirement for an OpCon job or schedule. <br></br> - PROCESSCHECK's completion status depends on whether the requirements are satisfied. It may be used as a prerun, or as a job upon which other jobs are dependent. This allows you to control the processing path and to be assured that file dependencies are met before downstream processing occurs.<br></br> - PROCESSCHECK runs as an OpCon job and does not require additional configuration or definition files to implement. <br></br> - For more information, refer to Using *SMA/WFL/PROCESSCHECK. |
| Operations Monitor | - This tool allows you to sample a limited subset of disk usage and usage values. Operations Monitor supports the following inquiries: DU, CPU usage for all user processes, CPU TRUE IDLE. <br></br> - The Operations Monitor utility allows you to supply a target value as well as OpCon events to be generated for wither success or failure, or both. <br></br> - You can also instruct this utility to create a cumulative report (i.e., you can accumulate samples throughout the month to assess critical metrics). <br></br> - Operations Monitor supports the following inquiries: DU, CPU usage for all user processes, CPU TRUE IDLE. <br></br> - Operations Monitor runs as an OpCon job and does not require additional configuration or definition files to implement. <br></br> - For more information, refer to [Operations Monitor](../additional-features/lsam-features/operations-monitor). |
| Job-level Resource Utilization | - This feature enables statistics to be returned for every job initiated by the MCP LSAM. <br></br> - The returned values are also stored with the job's history. <br></br> - For more information, refer to Resource Utilization Statistics. |
| *SMA/WFL/CHECK/MIX | - This tool allows you to interrogate for the presence or absence of any entries in the MCP Waiting mix or Scheduled entries. <br></br> - CHECK/MIX prepares a report listing all Waiting or Scheduled entries detected. Access this report via the View Job Output option. <br></br> - For more information, refer to [Using *SMA/WFL/CHECK/MIX](../additional-features/utilities/sma-wfl-check-mix). |

## Capture ODT Messages

There are times when processing paths may change depending upon the contents of a message displayed by a program. You might also want to capture a portion of a message to pass along to a subsequent job. With [Automated Response](../additional-features/lsam-features/automated-response), you can monitor for messages, send events to OpCon to change the processing path, update a variable used by a subsequent job or schedule, and take action directly on the MCP platform, such as automatically responding to a waiting entry.
 
From an OpCon perspective, there are two types of messages:
* OpCon job messages: messages displayed by processes started by OpCon.
* System messages: messages displayed by the system or by processes not initiated by OpCon.

For more information, refer to [Automated Response](../additional-features/lsam-features/automated-response) to learn how to implement this feature.

## Schedule via Command-line Interface

If you want to schedule, as an OpCon job, a command you would normally run from the MCP console, consider *SMA/WFL/COMMAND for this purpose. Commands may be delivered to:
* The MCP system, such as a SQUASH DISK command.
* System software, such as instructing Transaction Server (COMS) to disable an online program.
* A user process.

For more information, refer to [Using *SMA/WFL/COMMAND](../additional-features/utilities/sma-wfl-command).

## File Manipulation

If you want to schedule a CHANGE, COPY, or REMOVE command as an OpCon job you would normally run from the MCP ODT, be aware that these functions exist as OpCon job templates. From the Job Details screen, simply select an MCP Job Type of CHANGE, COPY, or REMOVE and fill in the form. 

The job will be submitted and the success or failure of the CHANGE, COPY, or REMOVE will be reported as the status of the OpCon job. This allows you to be assured that these actions have completed successfully before proceeding with processing. For more information, refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help.
 
If you need to convert a traditional MCP print file to a format that can be read on a user's desktop, consider using the CONVERT/PRINT utility. This utility will convert a traditional MCP print file into a flat ASCII text file suitable for transferring to and viewing on a user's workstation. 

While the same effect can be achieved with manual user intervention via the View Job Output facility on the SMA user interface, the MCP Print File Conversion utility allows you to automate the conversion of the file. You can then automate the transfer of the ASCII text file using whatever method you prefer. For more information, refer to [Using *SMA/WFL/CONVERT/PRINT (MCP Print File Conversion)](../additional-features/utilities/sma-wfl-convert-print).