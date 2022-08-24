# External Jobs Tracking

The SMA/ANNOUNCE/xxx program allows user-submitted jobs to be tracked by OpCon. When SMA/ANNOUNCE/xxx executes, a message is sent to the LSAM. The LSAM forwards a request to the SAM-SS to track the defined job. If the request is accepted, the SAM-SS returns a job initiation message (TX1) to the LSAM. From this point forward, the job can be viewed in Operations in the Enterprise Manager. The job's completion status will be sent to the SAM-SS when the job completes. For LSAM messages regarding external job tracking, refer to [Machine Messages](/reference-information/machine-messages).
 
Two items must be configured before the job tracking feature can function:

* The \*SMA/CONFIG/FILE/xxx under the [Optional Modules (OPT)](/operations-and-components/sma-manager/optional-modules) section must be updated. Set MixWatcher to a value of Y.
* The SMA/ANNOUNCE/xxx program defaults must be verified.

## Update the Configuration File

Modify the following field under [Optional Modules (OPT)](/operations-and-components/sma-manager/optional-modules):
 
MixWatcher: Set to a value of ```Y```.

:::info Note

The Mixwatcher configuration field is not automatically dynamic. Access the LOADCFG choice of SMAMGR if Mixwatcher was previously set to N and you have now set it to Y. This will cause the LSAM to initiate the \*SMA/SURROGATE program.

:::

## Using SMA/Announce

SMA/ANNOUNCE may be used as a stand-alone command or used as a step in a WFL. SMA Technologies recommends automating the tracking process by placing the command in each WFL to be tracked.

### SMA/Announce Defaults

* The installed program assumes the following:
* The SMA library function name is SMALIBRARY.
* The Schedule Date for tracking the job is the current date.
* The Schedule Name for the tracked job is AdHoc.
* The Frequency Name for the tracked job is the first defined frequency for the job in OpCon.

:::info Note

To override the default values, the parameters to SMA/ANNOUNCE should be populated with the desired values.

:::

#### Syntax

:::info Note

The wrapping of the syntax in this document does not indicate the location of a carriage return; the ↵ indicates the location of a carriage return.

:::

The syntax for running the SMA/ANNOUNCE program is:

```RUN *SMA/ANNOUNCE ("<SchedDate>","<SchedName>","<JobName>", "<FreqName>",<mix#>, "<UserLoginID>","<EventExternalToken>") ↵```

:::info Note

The following definitions assume that the original compiled SMA/ANNOUNCE program distributed by SMA Technologies is in use.

:::

* ```<SchedDate>``` is the Schedule Date on which the job should be tracked.
    * If not defined, the SAM-SS assumes the current date.
    * If the AdHoc schedule is used for ```<SchedName>``` and does not already exist on the current date, it is automatically added to the * Daily tables on the current date.
    * If an alternate schedule is specified for ```<SchedName>``` and the schedule does not already exist for the current date, the tracking request is denied.
* ```<SchedName>``` is the name of the schedule on which the job to be tracked is defined.
    * If not defined, the SAM-SS assumes the job is located on the AdHoc schedule.
    * If the job is not found on the schedule, the tracking request is denied.
    * If a schedule other than the AdHoc schedule is specified, the schedule must already be built in the Daily tables. If the schedule does not exist in the daily tables, the tracking request is denied.
* ```<JobName>``` is the name of the job as known to OpCon. This is the name entered on the Job Master screen in the Enterprise Manager.
    * If the job does not exist in Job Master, the tracking request is denied.
    * If a duplicate job already exists in the Daily tables (and the job name is 124 characters or less in length), a $nnn suffix is added to the job name (e.g., TestJob is displayed as TestJob$001, TestJob$002, TestJob$003, and so forth).
    * If a duplicate job already exists in the Daily tables and the job name is longer than 128 characters, the tracking request is denied. The maximum name length in the Job Master must not exceed 64 characters.
* ```<FreqName>``` is the name of the frequency to be used for the tracked job. The frequency name is the name entered in the Job Master (Frequency tab) screen for the job to be tracked.
    * If the frequency is not provided, the SAM-SS uses the first defined frequency for the job.
    * If the frequency is not found for the job, the tracking request is denied.
* ```<mix #>``` is the mix number of the job to be tracked.
* <```UserLoginID>``` is an OpCon User Login ID with the correct privileges to add a job to the schedule. The UserLoginID and EventPassword can default to the values defined in the LSAM's configuration file. For information on these configuration settings, refer to MCP LSAM Configuration. In order to use the default(s), substitute a null string (i.e., "") for the UserLoginID and EventPassword values.
* ```<EventPassword>``` is the password associated with the User Login ID for External Events.

:::info Note

This password is **not** the same password used to log in to the Enterprise Manager.

:::

* The UserLoginID and EventPassword can default to the values defined in the LSAM's configuration file. For information on these configuration settings, refer to [MCP LSAM Configuration](/configuration/mcp-lsam-configuration). In order to use the default(s), substitute a null string (i.e., "") for the UserLoginID and EventPassword values.


### Example WFL

:::tip Example

The SMA/ANNOUNCE program should be run as one of the first steps of each WFL to be tracked. The example below uses the default values for Schedule Date, Schedule Name, and Frequency Name. The example also defines a variable used to populate the parameter for the mix number of the job.

The following example shows a variable used to populate the parameter:

```

00000100?BEGIN JOB WFL/ADOPT;
00000200 INTEGER MYMIX;
00000250 MYMIX := MYSELF(MIXNUMBER);
00000300 RUN *SMA/ANNOUNCE ("","",
00000320 "JOBTrack","",
00000350 MYMIX,
"TrackUser","TrackExternal Token");
00000400 WAIT("Just ran Announce",OK);
00000500?END JOB.

```

:::

## Using SMA/SURROGATE

The SMA/SURROGATE program monitors each tracked job and queues the status for forwarding to SAM-SS. This program may be executed independently of the MCP LSAM to permit tracking of external jobs when the MCP LSAM is not active. In order to accomplish this, simply RUN \*SMA/SURROGATE/xxx from a WFL or by using the RUN command. If this option is chosen, be aware that if sufficient time elapses such that the external job is cleared from the MCP completion table, the job will be marked failed with a status description of "JOB MISMATCH" when communication between the MCP LSAM and SAM-SS is restored and manual investigation into the true disposition of the job will be required.
 
To stop the \*SMA/SURROGATE/xxx, issue a HI 2 command using the mix number of \*SMA/SURROGATE/xxx (i.e., ```<mix #>``` HI 2). The \*SMA/SURROGATE/xxx program will issue a display indicating that it is monitoring jobs if any tracked jobs are active. Once the number of monitored jobs is zero, the *SMA/SURROGATE/xxx will terminate gracefully without further intervention.
 
To see a list of the mix numbers being monitored, issue a HI 3 command. If there is a desire to remove a mix number from the list of tracked jobs, issue a HI command passing as the numeric value the mix number to be removed. Usage of the HI ```<mix#>``` command should be required only in rare instances, but is available if needed.

## Identify the External Job(s) in the Enterprise Manager

### The AdHoc Schedule

SMA Technologies recommends adding jobs to be tracked to the AdHoc schedule for two reasons:

* The schedule is dynamically added to the Daily Tables when the SAM-SS is informed of a job on the schedule that is to be tracked.
* Once active, the schedule remains open until midnight when it is allowed to go into a completed state. All jobs on the schedule must finish before the schedule closes.

If jobs to be tracked are on user-defined schedules, those schedules must be built and must be active in the Daily Tables for the SAM-SS to adopt the job(s). The corresponding schedule name must also be specified correctly in each WFL. On the other hand, if jobs to be tracked are defined on the AdHoc schedule, there is no need to define a schedule in the WFL or worry about the status of a schedule.

