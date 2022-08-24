# Resource Monitor

The \*SMA/RESOURCE/MONITOR runs continuously, gathering data as configured. Possible objects of the monitoring process are the following categories: system messages to include EOJ/EOT messages, files (creation, deletion, recent alterations, attainment of a percentage of maximum allowable size), and selected system resources. 

The Resource Monitor uses definition files maintained by the user to identify the resources, file conditions, and system messages for which to monitor. Once an event in any of the configured categories occurs, the data will be forwarded to the appropriate recipient; messages will be forwarded to the Display Handler \*SMA/DISPLAY/HANDLER, file events will be forwarded to the file monitor \*SMA/FILE/MONITOR, and system resource data will be retained by the Resource Monitor, \*SMA/RESOURCE/MONITOR. 

The recipient will then traverse the associated user data file to determine whether the event is one for which the user wishes to monitor and, if so, will take the predefined action(s).

## Update the Configuration File

Modify the following fields under [Optional Modules](/operations-and-components/sma-manager/optional-modules) (OPT) and [General LSAM Configuration (GEN)](/configuration/general-lsam-configuration):

1. For file monitoring:

    a. **File Monitor**: Set to a value of Y.

    b. **OpCon user and OpCon External Token**: If a user name and external token have not already been entered for external events, enter the *OpCon User ID* and the OpCon External Token.

2. For system message monitoring:

    a. **Autoresponse-Displays**: Set to a value of ```Y```.

    b. **OpCon user and OpCon External Token**: If a user name and external token have not already been entered for external events, enter the *OpCon User ID* and the OpCon External Token.

3. For resource monitoring:

    a. **Resource Mon Freq**: Set to a numeric value representing the number of minutes between sampling for system resource utilization.

    b. **OpCon user and OpCon External Token**: If a user name and external token have not already been entered for external events, enter the *OpCon User ID* and the OpCon External Token.

## Start the Resource Monitor

In order to provide continuous monitoring apart from the MCP LSAM, the Resource Monitor is initiated independently of the LSAM. If you have configured the Resource Monitor to be initiated concurrently with the LSAM, use the STATUS choice of SMA/MANAGER to confirm that the Resource Monitor is running. If you did not have the Resource Monitor set up to be initiated with the LSAM, use the INITRM choice on the SMA/MANAGER Main Menu to start it.
 
To view the previous information, refer to [Start the Resource Monitor](/reference-information/legacy#start-the-resource-monitor) in the Legacy Information topic.

## Maintenance of Definitions Files

The instructions provided in this section should be used to maintain these definitions files. Failure to follow these instructions may result in unexpected results.
 
#### Maintain Definitions Files

1. Edit the file using the PERFMENU option of the SMA/MANAGER Main Menu.

2. When you have completed the changes, enter PARENT in the Action area and save your changes.

3. If the file monitor definitions file, performance monitor definitions file, or system message definitions file was modified, notify the \*SMA/RESOURCE/MONITOR to refresh its internal tables with the new definitions. From the SMA/MANAGER Main Menu, select LOADDISP, LOADFILE, or LOADPERF.

To view the previous procedure, refer to [Maintain Definitions Files](/reference-information/legacy#maintenance-of-definitions-files) in the Legacy Information topic.

## Monitor for Performance and Disk Space Utilization Metrics

To instruct the Resource Monitor to monitor for performance and disk space utilization metrics, the MCP LSAM must be configured to define the sampling interval used by the Resource Monitor. The Resource Monitor will first determine, by checking the LSAM configuration file, if the Resource Monitor feature is in use. If it is, then the program will check for the presence of the Performance Monitor Definitions file, \*SMA/PERFMON/DEFS/xxx. If the file exists, the program will load into an internal table a list of performance metrics defined within the \*SMA/PERFMON/DEFS/xxx file, storing the location of the definition in the file within the internal table, and will then initiate monitoring at the frequency defined in the LSAM configuration file. Otherwise, the program will make an entry in the debug log.
 
At the configured frequency, the defined metrics will be interrogated and the results analyzed to determine whether a target condition has been reached. Upon attainment of a target condition, the associated action(s) contained in the Definitions file will be executed.
 
Each time a defined performance metric is achieved, the associated actions will be executed. There exists no facility for one-time processing of performance metrics.
 
If you update the performance definitions file and wish for the changes to take effect immediately as opposed to upon the next initiation of the Resource Monitor, you should utilize the LOADPERF choice on the Main Menu of SMAMGR after completing the steps provided in the [Maintenance of Definitions Files](/reference-information/legacy#maintenance-of-definitions-files) section. This will cause the internal table to be updated without the need to terminate the Resource Monitor. However, all cumulative data gathered prior to the update will be lost; the only values impacted will be those metrics accumulated using SUM or AVG. Should the AVG and SUM accumulation methods prove to be widely used in an environment in which the \*SMA/PERFMON/DEFS file is volatile and the loss of accumulated data is demonstrated to be an issue, an enhancement request to retain the accumulated values should be submitted.

## Performance Monitor Data File

This file is used to define the performance statistics to be gathered, the number of samples to be used in calculating an average, the target value, and the action(s) to be taken upon attainment of the target value.
 
There are three types of records: (D)efinition, (S)am action, and (M)CP action. The record type is located in the first position of the record. Definition records and their associated action records may be made inactive by inserting a percent sign (%) in the first position of each record.

:::info Note

 Commas are required for omitted parameters if subsequent parameters are used. However, if subsequent parameters are not being used, the trailing commas should be omitted (refer to the Example - "The user wishes to take some action if the CPU Utilization by user processes exceeded 90% at any time between 6:00 p.m. and 4:00 a.m.").

:::

Definition records are indicated by the presence of a "D" in the first position of the record. Data within the definitions record following the Metric Type are comma-delimited and must be in the following order:
 
**D**

**Metric Type**

**Metric**

**Comparison EQ, GE, GT, LE, LT, NE**

**Target value**: A numeric target value against which to compare the actual value. This number must be a whole number (no decimals or fractions) and must not contain any non-numeric characters such as commas (,) or percent (%) signs.

**Accumulation Type (optional)**: The values are AVG, SUM. Averages are computed using only the most recent number of specified samples. When a new sample is taken, the oldest one is dropped.

**Number of samples (optional)**: This is used only if Type of Accumulation is used. Default is 1; minimum is 1, maximum is 100.

**Start time (optional)**: The time at which to begin sampling, based on a 24-hour clock.

**End time**: The time at which to stop sampling, based on a 24-hour clock. End time is required only if Start Time is used.

:::info Note

End time must be later than Start time; the time during which to monitor cannot span midnight. To monitor both before and after midnight, create two separate entries in the definitions file.

:::

#### Metric Types

The possible Metric Types are:
 
**U**: CPU utilization.

**DU**: Disk usage. If the target diskpack is other than DISK, the user must supply the phrase ON ```<diskpack>```, where ```<diskpack>``` is replaced by the name of the diskpack.
 
The CPU Utilization Metrics table identified the possible metrics for CPU Utilization (Metric Type = U) and their descriptions.

## CPU Utilization Metrics

| Resource | Description |
| -------- | ----------- |
| USER PROC | This resource is the percentage of processor time spent in the user stacks. |
| I/O FINISH | This resource is the percentage of processor time spent handling I/O completion. |
| INIT PBIT | This resource is the percentage of processor time spent making arrays and code present initially. |
| OTHER PBIT | This resource is the percentage of processor time spent making arrays and code available again after they were overlaid. |
| MCP PROC | This resource is the percentage of processor time spent in MCP stacks and time spent by an active stack that has incurred an interrupt by another processor. |
| SEARCH PROC | This resource is the percentage of processor time charged to SEARCHLEAD and SEARCHFOLLOW accounts. |
| FALSE IDLE | This resource is the percentage of processor time spent idle when overlaid data is being transferred by the I/O subsystem. |
| TRUE IDLE | This resource is the percentage of processor time spent idle that is not considered to be false idle time. |
| PROC SW | This resource is the number of process switches that occur per second. |
| MEM DISK | This resource can have the value: <br></br> 1 = Memory disk units are present. <br></br> 0 = No memory disks are present. |
| USER IO | This resource represents the average number of user I/O operations per second during the time interval specified by the SBP command. |
| USER KBPS | This resource represents the average number of kilobytes of data transferred per second by user I/O operations during the time interval specified by the SBP command. |
| MCP IO | This resource represents the average number of MCP I/O operations per second during the time interval specified by the SBP command. |
| MCP KBPS | This resource represents the average number of kilobytes of data transferred per second by MCP I/O operations during the time interval specified by the SBP command. |
| DC IO | This resource represents the average number of data comm I/O operations per second during the time interval specified by the SBP command. |
| DC KBPS | This resource represents the average number of kilobytes of data transferred per second by data comm I/O operations during the time interval specified by the SBP command. |
| MD USER IO | This resource represents the average number of user I/O operations per second to memory disks during the time interval specified by the SBP command. |
| MD USER KBPS | This resource represents the average number of kilobytes of data transferred per second by user processes to memory disks during the time interval specified by the SBP command. |
| MD MCP IO | This resource represents the average number of MCP I/O operations per second to memory disks during the time interval specified by the SBP command. |
| MD MCP KBPS | This resource represents the average number of kilobytes of data transferred per second by MCP I/O operations to memory disks during the time interval specified by the SBP command. |
| SUM IO | This resource represents the sum of USER IO, MCP IO, and DC IO. | 
| SUM MD IO | This resource represents the sum of MD USER IO and MD MCP IO. |
| SUM MD KBPS | This resource represents the sum of MD USER KBPS and MD MCP KBPS. |
| IO INTERRUPT | This resource represents the average number of I/O completion interrupts per second during the time interval specified by the SBP command. |

The Diskspace Utilization Metrics table identifies the possible metrics for Diskspace Utilization (Metric Type = DU) and their descriptions.

## Diskspace Utilization Metrics

| Resource | Description |
| -------- | ----------- |
| TOT AVAIL | This resource represents the total number of available sectors on the entire family. |
| LARGEST | This resource represents the size, in sectors, of the largest available area. |
| SMALL AREAS | This resource represents the number of areas smaller than the specified size. |
| SMALL SECTORS | This resource represents the number of sectors in areas smaller than the designated size (this Name token will resolve to "SMALL SECTOR"). |
| LARGE AREAS | This resource represents the number of areas at least as large as the specified size. |
| LARGE SECTORS | This resource represents the total number of sectors in areas at least as large as the specified size (this Name token will resolve to "LARGE SECTOR"). |
| DISK ROWS | This resource represents the number of disk rows (areas) of the designated size that can be allocated. |
| AREA SIZE | This resource represents the number of sectors used to base comparisons on. |
| CAPACITY | This resource represents the total capacity, in sectors, of the entire family. |
| SECTOR SIZE | This resource represents the sector size in bytes. |
| AVAIL PCT | This resource represents the number of available sectors (TOT AVAIL) divided by the CAPACITY of the entire family. |

## SAM Action Records

SAM action records are indicated by the presence of an "S" in the first position of the record, followed immediately by a "$". Any valid OpCon external event may be used. One suggestion would be to set a machine instance property upon which jobs are dependent, thereby allowing users to control the number of jobs submitted when resource availability is limited. If omitted from the definition, the OpCon userid and password will be obtained from the LSAM configuration file.

#### S

**$**
**OpCon external event**
**Optional OpCon userid and password, each preceded by a comma**

#### MCP Action Records

MCP action records are indicated by the presence of an "M" in the first position of the record. Any valid MCP command may be entered. It is anticipated that a common usage of this definition will be to start a WFL job. If starting a WFL, the command START, followed by the full title of any valid WFL file must be entered. The user should take care to ensure that the WFL is syntactically correct and present in the location specified as the WFL job will not be monitored.
 
#### M

**MCP command**

## System Message Monitoring

To instruct the Resource Monitor to monitor system messages, the MCP LSAM must be configured to use the Automated Response feature. To specify the message to be monitored and the actions to take when the message is displayed, insert, within the definitions file (\*SMA/DISPLAYS/SYSMSG/xxx), the system message tokens and actions to take when the system message is displayed. If the LSAM is not configured for Automated Response or the \*SMA/DISPLAYS/SYSMSG/xxx file does not exist, the Resource Monitor program will make an entry in the debug log and will NOT monitor system messages.
 
As system messages are received, the Resource Monitor will scan the list of message definitions in search of a possible match. This scan will be cursory and is intended to identify messages that do not match any of the token definitions, so those messages will not be forwarded to the Display Handler for further matching and processing. The approach will be that of an OR comparison. If any token of the incoming message matches any token in the definitions file, the message will be forwarded.
 
The Display Handler performs AND comparisons wherein all tokens for a given definition must be present and in the specified location in order for a match to occur. The goal of this approach is to reduce the volume of messages passed to the Display Handler and minimize negative impact to performance on the Display Handler while avoiding excessive additional overhead in the Resource Monitor. With this understanding in mind, you should take care to select message tokens that are as unique as possible.
 
:::caution 

At a site in which system message volume is high, a delay in performing the defined actions may be observed. This delay can be significant.

:::

Each time a defined system message is received, it will be processed. There exists no facility for one-time processing of system messages.
 
If you update the system message definitions file and wish for the changes to take effect immediately, as opposed to upon the next initiation of the Resource Monitor, you should utilize the LOADDISP choice of SMAMGR to cause the internal list of message tokens to be refreshed without the need to terminate the Resource Monitor.

### SMA/DISPLAYS/SYSMSG Definitions File

The syntax rules for entries in the \*SMA/DISPLAYS/SYSMSG/xxx file are the same as those defined for the Automated Response feature, documented in [Automated Response](automated-response).

### SMA/DISPLAY/HANDLER

The Display Handler will make no distinction between messages from the LSAM and messages from the Resource Monitor. System message definitions and actions are defined within the \*SMA/DISPLAYS/SYSMSG/xxx file only. Because system messages are quite plentiful and diverse in content, it is strongly recommended that definitions for the system messages be specific enough to avoid the possibility of inadvertently getting a match. For more information on the Automated Response, refer to [Automated Response](automated-response).

## File Monitoring

Each time a file close notification is received, it will be processed by the Resource Monitor and forwarded to the File Monitor. If you update the \*SMA/FILEMON/DEFS /xxx file and wish for the changes to take effect immediately as opposed to upon the next initiation of the Resource Monitor, use the LOADFILE option on the Main Menu of SMA/MANAGER. This will cause the Resource Monitor to the list of files to be refreshed without the need to terminate the Resource Monitor. The Resource Monitor will inform \*SMA/FILE/MONITOR/xxx of the changes to \*SMA/FILEMON/DEFS/xxx so that the pointers to the associated actions within the file will be accurate.

To view the previous information, refer to [File Monitoring](/reference-information/legacy#file-monitoring) in the Legacy Information topic.

### SMA/FILEMON/DEFS Definitions File

The syntax rules for entries in the \*SMA/FILEMON/DEFS/xxx file are documented under F- Record in File Monitor. MCP action records are indicated by the presence of an "M" in the first position of the record. Any valid MCP command may be entered. It is anticipated that a common usage of this definition will be to start a WFL job or running a program. If starting a WFL, the command START, followed by the full title of any valid WFL file, must be entered. 

You should take care to ensure that the WFL is syntactically correct and present in the location specified, as the WFL job will not be monitored by the LSAM. If starting a program, the command RUN, followed by the full title of any valid executable file, must be entered. You should take care to ensure that the executable file is present in the location specified and appropriate permissions exist, as the process will not be monitored by the LSAM.
 
**M**
**MCP command**

### SMA/FILE/MONITOR Behavior

Upon initiation the File Monitor will load into its internal arrays a list of file entries along with a pointer representing the ordinal position of the file (F) entry within the \*SMA/FILEMON/DEFS/xxx file. The control file, \*SMA/FILEMON/CONTROL/FILE/xxx, will be opened. The list of files will be traversed and an inquiry performed for each file (F) entry to determine of any of the monitored conditions occurred while \*SMA/FILE/MONITOR/xxx was not active. 

The ALTERDATE and ALTERTIME of the monitored file will be compared to the date/time entry in the control file to ascertain whether the condition MIGHT have occurred again since the last time the \*SMA/FILE/MONITOR/xxx received a file close notice. This is not fool-proof, as there exists no facility for determining the activity that caused the ALTERDATE and ALTERTIME to be updated. The following table lists the behavior for each monitored condition.

| Condition | Condition Exists | Altered after control date | Actions Performed? |
| --------- | ---------------- | -------------------------- | ------------------ |
| Present | Yes	| Yes | Yes |
| Present | Yes	| No | No | 
| Present | No | N/A | No | 
| Deleted | Yes	| Alter date/time are not available for nonexistent files | Yes |
| Deleted | No | N/A | No |
| Altered | Yes	| Yes | Yes |
| Altered | Yes	| No | No |
| Altered | No | N/A | No | 
| MAX PCT | Yes | Yes | Yes |
| MAX PCT | Yes | No | No | 
| MAX PCT | No | N/A | No |

If the file monitor definitions file has been modified and you desire to implement the changes immediately as opposed to with the next initiation of the Resource Monitor and File Monitor, you should use the LOADFILE option on the Main Menu of SMA/MANAGER. This will cause only the File Monitor to close and reopen the definitions file so the pointers received from the Resource Monitor will coincide with the record locations within the file.

To view the previous information, refer to [SMA/FILE/MONITOR Behavior](/reference-information/legacy#smafilemonitor-behavior) in the Legacy Information topic.
 
If, at any time, you wish to force the File Monitor to re-evaluate the conditions of all files defined within \*SMA/FILEMON/DEFS/xxx, you should deliver an AX RESTART to \*SMA/FILE/MONITOR/xxx. The RESTART option will cause the File Monitor to close and reopen the definitions file (\*SMA/FILEMON/DEFS/xxx) as well as check the defined conditions and perform the associated actions if the conditions occur.
 
The \*SMA/FILE/MONITOR/xxx program will, based upon the value of the LSAM Idle Timer, check for new records in the \*SMA/SMA/FILE/LIST/xxx file. If a new record is present, the File Monitor will process and remove it from the \*SMA/FILE/LIST/xxx file.
 
Upon retrieving a file from the list, associated actions will be retrieved from the \*SMA/FILEMON/DEFS/xxx file and performed. The date and time stamp in the File Monitor control file will be updated with the time stamp from the "File Close" log entry.

## Timing of Definitions File Changes

Implementation of a modified File Monitor Definitions file (\*SMA/FILEMON/DEFS/xxx) should be performed at a time when it is anticipated there will be minimal file activity. Judiciously selecting the time to implement this file will minimize the potential for a file condition to be overlooked or for the pointers in the Resource Monitor to fail to match those in the File Monitor.
 
If a site is monitoring a relatively static file system, it might be advisable to insert the following in the \*SMA/FILEMON/DEFS/xxx file so that implementation of the changes can occur automatically and almost simultaneously (The "M" records are to be contained on a single line within the \*SMA/FILEMON/DEFS/xxx file and not on multiple lines as they appear below.):

``` 

% File Monitoring
F*SMA/FILEMON/DEFS ON <diskpack>., ALTERED
MSTART *SMA/WFL/COMMAND ON PRODPK("*SMA/RESOURCE/MONITOR","AX FILEMON")

```

You can also use the File Monitoring capabilities to monitor for an altered \*SMA/DISPLAYS/SYSMSG/xxx file and/or \*SMA/PERFMON/DEFS/xxx file and automate delivery of the appropriate AX commands to \*SMA/RESOURCE/MONITOR/xxx. To do this, define appropriate "F" and "M" records within the \*SMA/FILEMON/DEFS/xxx file, as shown in the following examples:
 
```

% Performance Monitoring
F*SMA/PERFMON/DEFS ON DISK.,ALTERED
MSTART *SMA/WFL/COMMAND("*SMA/RESOURCE/MONITOR","AX PERFMON")
% System Message Monitoring
F *SMA/DISPLAYS/SYSMSG ON DISK.,ALTERED
MSTART *SMA/WFL/COMMAND("*SMA/RESOURCE/MONITOR","AX SYSMSG")

```

