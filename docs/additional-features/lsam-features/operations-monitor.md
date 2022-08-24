# Operations Monitor

The WFL /*SMA/WFL/OPS/MONITOR/xxx performs a limited number of system resource interrogations, such as processor utilization and available disk space. This utility is intended to be used to monitor for adverse conditions.

## Usage 

There are multiple ways to use this utility:

1. Define within the WFL parameters the resource to be monitored, the target value of the resource, the type of comparison to be performed between the target value and the actual value, and whether attainment of the target value indicates an acceptable condition or an alarm condition. The WFL will then complete OK or fail depending on this criteria.

2. Define all the parameters discussed in item 1. Additionally, define up to two OpCon events; one to be sent in the case of an acceptable condition, the other to be sent in case of an alarm condition. The WFL will always complete OK when any events are defined.

## Syntax

On the MCP Job Details screen, use the syntax specified in these next two subsections.

#### File Title

\*SMA/WFL/OPS/MONITOR/xxx

#### Arguments

```

"<Cmd>","<Comparison>","<Criterion>","<Good Event>","<Bad Event>"

```

* ```<Cmd>``` is the command to be performed. The following commands are supported: DU and U.
* ```<Comparison>``` is used to specify the value, and optionally a qualifier, against which to compare the inquiry result.
    * The first piece of data is applicable only to the "U" command and is omitted for the "DU" command. The qualifier "USER" will target the CPU usage consumed by all user processes; the qualifier "IDLE" will target the true CPU idle percentage.
    * The next piece of data is the comparison to use. Applicable values are:
        * EQ (equal to)
        * NE (not equal to)
        * LT (less than)
        * GT (greater than)
        * LE (less than or equal to)
        * GE (greater than or equal to)
    * The third piece of data is the numeric value against which to compare. All values are in terms of percentage.
* ```<Criterion>``` is the criterion used to determine if the result of the inquiry should be deemed successful.
    * The value TRUE indicates success if the condition is met.
    * The value FALSE indicates success if the condition is not met.
* ```<Good Event>``` is the optional OpCon external event to be forwarded to SAM-SS in the event of success. This parameter is optional. If unnecessary, insert a pair of double quotes to indicate a null value.
* ```<Bad Event>``` is the optional OpCon external event to be forwarded to SAM-SS in the event of success is not achieved. This parameter is optional. If unnecessary, omit the parameter or insert a pair of double quotes to indicate a null value.

## Keywords Available

To support the collection and reporting of meaningful data, the following MCP-specific tokens may be used within the external events supplied in the fourth and fifth parameters. Each of these tokens will be replaced with the corresponding value by the SMA/WFL/OPS/MONITOR/xxx:

|     |     |
| --- | --- | 
| @TASKVALUE | An integer value representing the TASKVALUE task attribute returned by SMA/OBJ/OPS/MONITOR |
| @TIME | MCP system time in the format HH:MM:SS |
| @DATE | MCP system date in the format MM/DD/YY |
 
For sites that opt not to use external events, the OpCon job should be defined to trigger a JOB:RESCHEDULE event if the job fails. The frequency of the sampling can be dictated within the JOB:RESCHEDULE event. If the job completes successfully (it got a hit on the target conditions), an appropriate event should be triggered. This event might be some form of notification, adding a cleanup job to a schedule, placing a schedule on hold, etc. 

The Operations Monitor utility may also be used as a prerun if the desire is to execute a job on the MCP platform when the utility completes successfully rather than to trigger an event. When used as a prerun, the frequency of sampling is controlled by the OpCon timer associated with prerun re-submission (the default is three minutes).

## Reporting

An optional, cumulative user report file showing the command, qualifier, and results can also be produced. This file contains a header record with comma-delimited data records.

```

Date, Time, Command Entered, Result
4/22/16, 15:09:40, U Option:IDLE, Result:93

```

When \*SMA/OBJ/OPS/MONITOR is run with the cumulative reporting enabled:
* The current execution will update the existing file if a user report file of the same title exists.
* The current execution will create a new file if a user report file of the same title does NOT exist.

To enable reporting:
* Copy SMA/WFL/OPS/MONITOR/xxx as a unique user job. This step is strongly recommended by SMA Technologies to prevent overwriting the changes with the next MCP LSAM upgrade.
* Modify the copied WFL such that the SMA/OBJ/OPS/MONITOR/xxx program is executed with SW8 set (un-comment sequence number 15000).
* Use the copied WFL in the File Title field of the Job Details.

The default title of the report file is (uc)SMA/OPSMON/REPORT ON ```<pack name>```. If the site wishes to create a separate report for each unique entity monitored:
* Copy SMA/WFL/OPS/MONITOR/xxx as a unique user job. This step is strongly recommended by SMA Technologies to prevent overwriting the changes with the next MCP LSAM upgrade.
* Modify the copied WFL such that the SMA/OBJ/OPS/MONITOR/xxx program is executed with SW8 set (un-comment sequence number 15000) AND modify line 15300 to define the desired file title for the report file.
* Use the copied WFL in the File Title field of the Job Details.

Because the user report file is cumulative, SMA Technologies strongly recommends that sites perform periodic maintenance to remove user report files so the \*SMA/OBJ/OPS/MONITOR/xxx will create fresh files. This can be performed by passing SMA/WFL/COMMAND/xxx the following parameters:
 
"MCP","REMOVE ```<user report file title>```"

:::tip Example

If the user specifies the DU ON PRODPK command and wishes to update a property (called a token prior to OpCon release 4.0) named DU-PRODPK if the usage is greater than 80%, the event might look like this:

```$TOKEN:SET,DU-PRODPK,@TASKVALUE``` 

\- or -

```$CONSOLE:DISPLAY, Disk usage on PRODPK is @TASKVALUE at @TIME on @DATE```

:::

:::tip Example

The following combinations of Cmd and Comparison are supported. The literal "LT 45" is used for illustrative purposes only.

```"U","IDLE LT 45",…```

```"U","USER LT 45",…```

```"DU ON DISK","LT 45",…```

:::