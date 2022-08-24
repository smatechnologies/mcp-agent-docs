# Communication Troubleshooting

## Jobs Stuck in "Running" State

#### Full Description

Although a task and its subtasks were completed, the job's status in Enterprise Manager's Operations remained "Job Running".
 
#### Possible Explanation:
 
Multiple SMANetCom components are communicating with a single instance of the MCP LSAM. This situation can result in one SMANetCom "stealing" messages intended for the other SMANetCom; as a result, the correct database is not updated with the current job status or external event.

##### Operator Response:

Contact SMA Technologies Support to configure OpCon correctly.
 
## LSAM not Communicating

#### Full Description

The LSAM is not communicating with SMANetCom, and/or jobs fail to start (i.e., the Enterprise Manager displays "Wait Machine"), and/or job status information is not up-to-date in the Enterprise Manager.
 
#### First Possible Explanation:
 
The machine name matches neither the BNA host name nor the alias defined in the LSAM's configuration file.

##### First Operator Response:

The machine name is case-sensitive and must be followed by a period (.) in the Machines table. If an alias is defined in the *SMA/CONFIG/FILE/xxx, it should not be followed by a period in the \*SMA/CONFIG/FILE/xxx, but should be followed by a period in the Machines table. For more information on this response, refer to [Machine Name Resolution](https://help.smatechnologies.com/opcon/core/objects/machines/#machine-name-resolution) in the Concepts online help.
OpenSecond Possible Explanation:
 
The TCP/IP address of the MCP machine has not been defined on the SAM machine.

##### Second Operator Response:

The TCP/IP address of the MCP machine may be defined either in the hosts file on the SAM machine, or in the Advanced Properties of the Machines table. For more information on this response, refer to Machine Name Resolution in the Concepts online help.

#### Third Possible Explanation:
 
\*SMA/MCP/INTERFACE has left the active mix with the following error: "F-DS INVALID INDEX @ 02412000". The cause of this situation is failure to remove the \*SMA/CP/MCS/= and *SMA/TRACKING/FILE files after changing the "max number of concurrent jobs" configuration variable.

##### Third Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the LSAM:

1. \*SMA/TRACKING/FILE/xxx ON ```<packname>```

2. \*SMA/CP/MCS/xxx/= ON ```<packname>```

3. Be sure to check ALL families on the system - not just the family on which the LSAM runs.

#### Fourth Possible Explanation:
 
The LSAM is not configured to accept messages from the SAM machine's IP address. The message "```$CONSOLE:DISPLAY, Bad IP:<Invalid IP Address>```" in the SMANetComTrace log confirms this cause.

##### Fourth Operator Response:

Update the LSAM configuration to permit communication with desired IP address. For more information on this response, refer to Communication Parameters (COMM).

#### Fifth Possible Response:
 
The LSAM detected that the message CRC does not match the calculated CRC value. The message "```$CONSOLE:DISPLAY, Bad CRC:<Partial SMANetCom Message>```" in the SMANetComTrace log confirms this cause.

##### Fifth Operator Response:

The occurrence of an invalid CRC indicates either a problem in the underlying TCP/IP protocol, or indicates a bug in the CRC calculation routine by the LSAM or by SMANetCom. Gather debug information (e.g., the debug print file produced by the \*SMA/TCPIP module, and the SMASUP information from the SAM machine) and contact SMA Technologies Support.
 
## Arithmetic Overflow Error

#### Full Description

The message, "Arithmetic overflow error for data type smallint, value = 32768," is observed in the OpCon log.
 
#### Possible Cause:
 
In excess of 32,767 job status messages were generated for a single OpCon job.

##### Operator Response:

1. Examine the program logic to determine the cause for the excessive number of messages, and take steps to reduce the number if possible.

2. Set the MCP LSAM config variable, Task Completion Messages" to "N" to suppress task completion messages from being generated for subordinate tasks. This will not affect reporting of the completion status of the OpCon job.

3. Set the MCP LSAM config variable Enable Statistics to "N". This will disable all statistics reporting for all jobs.