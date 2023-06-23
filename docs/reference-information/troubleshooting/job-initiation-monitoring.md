# Job Initiation/Monitoring Troubleshooting

## Job Stuck in "QUEUED" State

#### Full Description

Job stays in "QUEUED" state.
 
#### Possible Cause:
 
The MIXLIMIT or TASKLIMIT attribute of the queue through which the job starts is preventing the job from being run.

##### Operator Response:

1. Check the MIXLIMIT and TASKLIMIT values for the job queue to confirm the values.

2. Verify the job is in the queue.

3. Increasing the MIXLIMIT or TASKLIMIT value, or changing the queue through which the job is run may be appropriate. For more information on this response, refer to [MCP LSAM Operation](../../operations-and-components/mcp-lsam-operation).
 
## Job Stuck in "Start Attempted" State

#### Full Description

Job stays in a "Start Attempted" state.
 
#### First Possible Explanation:
 
Communication with the LSAM has been lost.

##### First Operator Response:

Verify the LSAM modules \*SMA/COMM/xxx, \*SMA/TCPIP/xxx, and \*SMA/MCP/INTERFACE/xxx are up and running. For more information on this response, refer to \*[SMA/TCPIP](../../operations-and-components/core-programs-and-files#smatcpip-associated-files).

#### Second Possible Explanation:
 
\*SMA/MCP/INTERFACE has left the active mix with the following error: "F-DS INVALID INDEX @ 02412000". The cause of this situation is failure to remove the \*SMA/CP/MCS/= and \*SMA/TRACKING/FILE file after changing the "max number of concurrent jobs" configuration variable.

##### Second Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the LSAM:

1. ```*SMA/TRACKING/FILE/xxx ON <packname>```

2. ```*SMA/CP/MCS/xxx/= ON <packname>```

Be sure to check ALL families on the system - not just the family on which the LSAM runs.
 
## Job Stuck in "Wait Machine" State

#### Full Description

Job stays in "Wait Machine" state.
 
#### Possible Explanation:
 
The maximum number of jobs is being run.

##### Operator Response:

No action required. When the number of active jobs falls below the maximum for which the LSAM is configured, additional jobs are initiated by SAM. The LSAM may be configured for a maximum of 500 jobs. For more information on this response, refer to [Update the "Max Number Concurrent Jobs" Field](../../configuration/update-max-concurrent-jobs).
 
## Job Status "0SNTX/SECRTY" Error

#### Full Description

Receiving a 0SNTX/SECRTY ERR status.
 
#### First Possible Explanation:
 
The LSAM is running under a usercode without the correct privileges to run the job.

##### First Operator Response:

Stop the LSAM and then start the LSAM under a usercode with correct privileges. For more information on this response, refer to Stop the LSAM.

#### Second Possible Explanation:
 
The usercode being used to start the job does not have the privileges needed.

##### Second Operator Response:

Verify the job's usercode on the Enterprise Manager's Job Details screen. For more information on this response, refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help.

#### Third Possible Explanation:
 
The queue through which the LSAM WFL runs has a TASKLIMIT.

##### Third Operator Response:

Change the WFL CLASS attribute to a queue that does not have a TASKLIMIT value set. For more information on this response, refer to [Using *SMA/WFL/COMMAND](../../additional-features/utilities/sma-wfl-command).
 
## Job Status "NOT JOB FILE" Error

#### Full Description

Receiving a NOT JOB FILE error.
 
#### Possible Explanation:
 
The WFL file's FILEKIND is neither JOBSYMBOL nor SEQDATA.

##### Operator Response:

Using CANDE or DUMPALL, change the FILEKIND attribute of the WFL file to JOBSYMBOL or SEQDATA. Contact the MCP-platform system administrator to request this action.
 
## Job Status "PARAM/ATTR" Error

#### Full Description

Receiving a PARAM/ATTR ERR status.
 
#### Possible Explanation:
 
On Enterprise Manager's Job Details screen, the job's "File Title" field contains a parameter following the file title.

##### Operator Response:

On the Enterprise Manager's Job Details screen, place the parameter in the job's "Arguments" field. For more information on this response, refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help.
 
## PROCESSCHECK not Working

#### Full Description

\*SMA/WFL/PROCESSCHECK/xxx does not find WFL jobs that are active.
 
#### Possible Explanation:
 
The target process is incorrectly identified using the name of the WFL file. When searching for a WFL job in the mix using \*SMA/WFL/PROCESSCHECK, one must use the job name (from the ?BEGIN JOB line within the WFL file) and not the name of the WFL file. If the presence of the WFL file is in question, then the appropriate tool is \*SMA/WFL/FILECHECK.

##### Operator Response:

In the \*SMA/WFL/PROCESSCHECK ```<Process Name>```, replace the name of the WFL with the job name in the search criteria.