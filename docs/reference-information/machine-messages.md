# Machine Messages

The list presents LSAM status messages forwarded to the SAM and supporting services. The message descriptions are displayed in the graphical interfaces following the job status.
 
The 20-character status description field contains a five-character area reserved for the ClearPath MCP mix number followed by a 15-character description.
 
All TX messages referenced below indicate a message sent from SMANetCom to the LSAM.

## ADOPTED

This message indicates that a tracking request has been received by the LSAM.

## ALREADY RUNNING

An OpCon job initiation request (TX1) was received for this job and the job is running on the ClearPath MCP.

## ATTRIBUTE ERR

* Assignment of task attributes was attempted on a job initiated with a RUN.
* One of the task attributes is erroneous.
* Refer to the system log for a display of the error message from the HANDLEATTRIBUTES procedure.
* Verify the job definition details.

## COMPLETED

The job completed successfully.

## COMPLETED–ADOPT

A tracked job has completed successfully.

## DATA TOO LONG

* In the process of property resolution within OpCon, the data sent to the LSAM is longer than the allowed maximum length.
* Check that data values associated with properties do not exceed the length specified for the MCP Job Details.
* The job was not run on the MCP platform.
* The Job Details field that contains the long data can be identified by viewing Enterprise Manager path: Job Information > Configuration > Operations Related Information > Detailed Job Messages.

## DS

The job terminated abnormally.

## DSED - ADOPT

The external tracked job terminated abnormally.

## DS OUT OF QUEUE

The job was DS'ed while still queued.

## F DS

The job experienced a fault and was terminated abnormally.

## F DS - ADOPT

The externally tracked job experienced a fault and was terminated abnormally.

## FAIL MSG

The WFL displayed a message that matched one of the Fail Codes, causing the job to be reported as failed in Enterprise Manager Operation.

## FAILED - ADOPT

A tracked job has failed. (The HISTORY task attribute indicates job finished in error and a specified reason has not been determined.)

## INV PARM LOC

This error is caused by placing the WFL or program parameter on the File Title instead of the Arguments field of the Job Details. To resolve, modify the Job Details such that the parameter is located in the Arguments field.

## JJJJJ/TTTTTCOMP OK

* The task completed successfully.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTDS

* The task terminated abnormally.
    * JJJJJ is the job number.
    *  TTTTT is the task number.

## JJJJJ/TTTTTFAILCODE

* The task displayed a message that matched one of the Fail Codes, causing the task to be reported as failed in Enterprise Manager Operation.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTF DS

* The task experienced a fault and was terminated abnormally.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTO DS

* The system operator terminated the task abnormally.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTP DS

* The task was terminated abnormally because of a program fault.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTQ DS

* The task was terminated abnormally because of an improper job queue definition or a job queue error.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTRESETCODE

* The task displayed a message that matched one of the Fail Reset codes, causing the task to be reported as Finished OK in Enterprise Manager Operation.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JJJJJ/TTTTTSNTX/SCRY

* An OpCon task initiation request (TX1) was received by the LSAM, but the initiation attempt failed because of an invalid syntax used in the construction of the file title.
    * JJJJJ is the job number.
    * TTTTT is the task number.

## JOB ARRAY FULL

* This message is sent in response to an OpCon job initiation request (TX1).
* The message occurs when the number of active jobs, according to the OS handler (SMA/MCP/INTERFACE), has reached the maximum defined in the LSAM configuration file.
* OpCon attempts job initiation again.

## JOB MISMATCH

* This message may be received in response to a TX1 or TX2 request.
* It indicated that the external job was located in the tracking file, but the stack number and/or process name belonging to the mix number assigned to this job cannot be verified with certainty.
* The most probable cause is a delay in the TX1 reaching *SMA/SURROGATE – perhaps because the LSAM was not up at the time the job was adopted, or the MCP machine was marked down on the Enterprise Manager when the job was adopted, resulting in a delayed TX1 which reached *SMA/SURROGATE some time after the job completed.

## JOB NOT ACTIVE

* This message is sent in response to an OpCon job status request (TX2) or to an OpCon job completion acknowledgment (TX3).
* Although the job was found in the tracking file, the record is not available because the job is no longer active.

## JOB NOT FOUND

* This message is sent in response to an OpCon job status request (TX2) or to an OpCon job completion acknowledgement (TX3).
* The job was not found in the tracking file.
* This can be the result of any number of situations (multiple SAM's connected to a single LSAM, delayed delivery of a TX1 for a job on which a JOB:TRACK event was sent to SAM, etc.).

## JOB Q FULL

* This message is sent in response to any OpCon job initiation request (TX1) that is received when the number of active jobs, determined by the COMM Handler (SMA/COMM), has reached the maximum.
* The maximum number is defined in the LSAM configuration file.
* OpCon attempts job initiation again.

## LSAMRESTARTING

* This message is sent following a restart/recovery of the LSAM modules.
* The job was present in the LSAM arrays before the LSAM terminated.
* This is the initial status following an LSAM recovery.
* It is followed by a current status of the job.

## MISSING OBJECT

* The Details screen in the Enterprise Manager contains the RUN command, but the file named in the File Title is not present.
*  Verify the USERCODE, FAMILY, and spelling.
* The usercode does not have a family assignment and the Job Details File Title does not include the family name of the program.

## NO JOB TITLE

No file title was defined on the Details screen in the Enterprise Manager.
 
:::info Note 

The PARAM/ATTR ERR message replaces NO JOB TITLE when the "Contemporary, XML" protocol is in use.

:::

## NO MATCH -ADOPT

* During restart/recovery of the *SMA/SURROGATE program, an attempt was made to query the current status of the external adopted job. Either the query itself was unsuccessful, or the stack number and/or process name of the active mix number does not stack the number/process name earlier retrieved for this job.
* Manually determine the completion status of the job and mark it accordingly on the Enterprise Manager.

## NO WFL FILE

* The Details screen in the Enterprise Manager contains the START command, but the file named in the File Title is not present. Verify the usercode, family, and spelling.
* The mix number of this status description belongs to the LSAM task that initiates the WFL compile. It is not the mix number for the WFL compile itself.
* The usercode does not have a family assignment and the Job Details File Title does not include the family name of the WFL.
 
:::info Note 

The PARAM/ATTR ERR message replaces NO WFL FILE when the "Contemporary, XML" protocol is in use.

:::

## NOT CODE FILE

The Details screen in the Enterprise Manager contains the RUN command, but the File Title is not the name of an existing executable file.

## NOT DSED

* A "Kill" was requested for this job, but the job was not O-DS'ed.
* This message often occurs when the kill was attempted after the job's completion.

## NOT FOUND-ARRAY

This message is sent in response to an OpCon job status request (TX2) or to an OpCon job completion acknowledgment (TX3) when an OpCon Job ID is not in the OS Handler (SMA/MCP/INTERFACE) tables.

## NOT JOB FILE

*  The Details screen in the Enterprise Manager contains the START command, but the File Title is not the name of an existing WFL file.
* The File Title indicates the name of a file whose file type is other than JOBSYMBOL, DATA, or SEQDATA. Change the file type to JOBSYMBOL, DATA, or SEQDATA.

## NOT VALID

* The job could not be located and the status is unknown.
* This message may be received following a restart/recovery of the LSAM modules.
* This message usually indicates the job has completed (normally or abnormally).

## O DS

The system operator terminated the job abnormally.

## O DS - ADOPT

The system operator terminated the tracked job abnormally.

## P DS

The job was terminated abnormally because of a program fault.

## P DS - ADOPT

The external job was terminated abnormally because of a program fault.

## PARAM/ATTR ERR

* An OpCon job initiation request (TX1) was received by the LSAM, but the initiation attempt failed because of a parameter mismatch or invalid attribute (job name does not conform to the rules for entity names).
* If the START command was used, the mix number of this status description belongs to the LSAM task initiating the WFL compile and not to the mix number for the WFL compile itself. A possible cause for this error is that the Details screen in the Enterprise Manager contains the START or RUN command, but the file named in the File Title is not present. Verify the USERCODE, FAMILY, and spelling.

## PARAMETER ERR

* The Details screen in the Enterprise Manager contains the RUN command, but a parameter is erroneous.
* Verify the parameter length and type.

# PRERUN ACTIVE

The Prerun job is active.

# PRERUN FAILED

* The Prerun job failed.
* OpCon attempts job initiation again.

# PRERUN WAITING

The Prerun job is in the waiting mix.

## QUEUED

* The job has been placed in a system queue.
* This is the first status for a WFL job that compiled successfully.
* When the job is released from the queue, the status will change to RUNNING.

## RESTART H_ER nnn

* Following a restart of the LSAM, the job's status could not be determined due to a GETSTATUS hard error "nnn".
* A description of the specific hard error may be found in the appropriate appendix of the MCP GETSTATUS/SETSTATUS Manual.

## RESTART S_ER nnn

* Following a restart of the LSAM, the job's status could not be determined due to a GETSTATUS soft error "nnn".
* A description of the specific soft error may be found in the appropriate appendix of the MCP GETSTATUS/SETSTATUS Manual.

## RUNNING

* This job is active.
* This message will also be seen if a WFL has been DS'ed and is waiting for tasks to complete.
* This message is also generated when a process resumes execution following a wait, such as that caused by a suspension awaiting an operator response.

## RUNNING –ADOPT

OpCon has received the tracking request and responded with a TX1 message. SMA/SURROGATE has received the TX1 message and the job is running.

## SCHEDULED

* This job has been scheduled by the system.
* This message can be expected during periods of high processor usage.

## SNTX/SECRTY ERR

An OpCon job initiation request (TX1) was received by the LSAM, but the initiation attempt failed because of an invalid syntax used in the construction of the file title.

## TASK(S) FAILED

The job completed successfully, but one or more of the subordinate tasks within the WFL failed.

## TASK FAILED JOB

* The configuration option Fail Job if Task Fails has been set to Y.
* A subordinate task of the WFL has failed and consequently the Enterprise Manager has reported the job as failed.

## UNKNOWN ERROR

* This message occurs when a specific reason for the job's failure could not be identified.
* In most cases, the WFL job will have failed queue insertion. The mix number is the one most recently identified with the OpCon job. If the job has failed queue insertion, this will be the mix number of the WFL compile.

## USERCODE ERROR

* The LSAM was unable to completely assume the identity (i.e., security privileges, family assignments, and so forth) of the usercode specified on the Details screen in the Enterprise Manager.
* Verify the spelling.

## WAITING

* The job is in the waiting mix.
* The mix number shown is the mix number of the waiting process, not necessarily the number of the parent WFL.
* This message will be displayed momentarily even if Automated Response has been set up for the situation.
* When the task becomes active again, a status of RUNNING will be displayed.

## WFL SYNTAX ERR

* The WFL source file contains syntax errors.
* Correct the WFL source.
* The File Title field on the Details screen in the Enterprise Manager may contain extraneous characters, such as CR/LF, START, or RUN.
* The File Title field should contain only the file title of the process to be initiated; furthermore, if the job is being initiated using a RUN command, the appropriate task attributes should also be included.
* The WFL source file contains an "INCLUDE" statement that references a file that cannot be found. The WFL compile was DS'ed.
