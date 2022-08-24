# External Event Interface Library

The External Event Interface Library allows OpCon events to be passed directly to the LSAM from a user program. Several methods of accessing the library are available: the \*SMA/EVENTGEN utility, an ALGOL program, and a COBOL85 program.

## Using *SMA/EVENTGEN

In a WFL, the \*SMA/EVENTGEN/xxx utility forwards external events to the SAM-SS. The program accepts three parameters: the SAM ID, the SAM external token, and the external event to be forwarded. The SAM ID and SAM external token can default to the values defined in the LSAM's configuration file. For information on these configuration settings, refer to the [General LSAM Configuration (GEN)](/configuration/general-lsam-configuration) topic. In order to use the default(s), substitute a null string (i.e., "") for the SAM ID and SAM external token value when running the \*SMA/EVENTGEN/xxx utility. The \*SMA/EVENTGEN program requires no modification.
 
The utility is often applied in the event a WFL contains numerous tasks and the failure (or completion) of a given task should trigger an OpCon action. This WFL may or may not have been initiated using OpCon. This application of the utility is valuable when the WFL cannot be scheduled using OpCon (i.e., it is initiated by a user of an online program).

### Syntax

:::info Note

The wrapping of the syntax in this document does not indicate the location of a carriage return; the ↵ indicates the location of a carriage return.

:::

The syntax for running the \*SMA/EVENTGEN/xxx program is:

```

RUN *SMA/EVENTGEN/xxx ("<SAM ID>","<SAM External Token>","<OpCon Event>")

```

* ```<SAM ID>``` is the OpCon User ID specified in the MCP configuration file. The SAM ID parameter defaults to the configuration file's SAM ID value. To use the default, substitute a null string (i.e., "") for the parameter value. Refer to General LSAM Configuration (GEN).

* ```<SAM External Token>``` is the external token for the relevant SAM ID. The SAM External Token parameter defaults to the configuration file's OpCon External Token value. To use the default, substitute a null string (i.e., "") for the parameter value. Refer to General LSAM Configuration (GEN).

* ```<OpCon Event>``` is a valid OpCon event. For a list of valid OpCon events, refer to Introduction in the OpCon Events online help.

:::tip Example

The following example shows syntax for a valid OpCon event:

```

NOTIFY:LOG,<Severity>,<EventID>,<Msg>

```

:::

## Customizing External Event Generation

A sample ALGOL program and a sample COBOL85 program are provided with the LSAM. The file names are \*NEW/SMA/SRC/MULTI/EVENT/C85 and \*NEW/SMA/SRC/MULTI/EVENT/ALGOL, respectively.

### Modify the ALGOL Program

For the ALGOL program, the following three items should be modified:

1. SAM_ID: Enter an OpCon User Login ID with the required privileges.
2. SAM_PW: Enter the event external token for the OpCon User Login ID.
3. SAM_EVENT: Enter any valid OpCon event.

For a list of valid OpCon events, refer to [Introduction](https://help.smatechnologies.com/opcon/core/events/introduction) in the OpCon Events online help.

### Modify the COBOL85 Program

For the COBOL85 program, the following three items should be modified:

1. **WS-SAM-ID**: Enter an OpCon User Login ID with the required privileges.
2. **WS-SAM-PW**: Enter the event external token for the OpCon User Login ID.
3. **WS-SAM-EVENT**: Enter any valid OpCon event.

For a list of valid OpCon events, refer to [Introduction](https://help.smatechnologies.com/opcon/core/events/introduction) in the OpCon Events online help.

## SMA/EVENTGEN Library Interface Results

The *SMA/EVENTGEN program sets its TASKVALUE attribute with the result from the SEND_EXTERNAL_EVENT library interface. The possible library interface results are provided in the table.

| Library Interface Results | Description |
| ------------------------- | ----------- |
| 0 | Event placed in *SMA/OUTBOUND/FILE for retrieval by the TCPIP handler. <- Success! |
| 1 | SAM userid starts with a blank. |
| 2 | SAM external event starts with a blank. |
| 3 | SAM event array starts with a blank. |
| 4 | SAM event does not start with $. | 
| 8 | File was available, but could not read from file. |

## Examples

:::tip Example

In this use case, we have the need to dynamically supply different values as parameters to a job through an OpCon Event. One of these values contains a character that would cause a problem with the event. The solution for this problem is to define multiple properties instead, and place the problem character in the job definition. For this example, the problem character in question is a comma (,).
 
On the Job Definition, the first Parameter to the job must be a string of alpha characters (e.g., DAILY), and the second parameter must be a string of alpha characters with a comma in the middle (e.g., TEST,JOB).
 
The *incorrect* approach is:

1. In the Job Details for the platform, we use the following Tokens separated by commas:

```[[JI.PARAM1]],[[JI.PARAM2]]```

2. In the OpCon Event to add the job, we use this syntax:
```$JOB:ADD,$DATE,SCHEDULE,JOB,FREQCODE,PARAM1=DAILY;PARAM2=TEST,JOB```

**Result**

The job will fail because a comma is used by OpCon as a delimiter for events, and when the Tokens resolve, the value becomes ```DAILY,TEST``` instead of ```DAILY,TEST,JOB```.
 
The **correct** approach is:

1. In the Job Details for the platform, we use the following tokens separated by commas:

```[[JI.PARAM1]],[[JI.PARAM2]],[[JI.PARAM3]]```

2. In the OpCon Event to add the job, we use this syntax:

```$JOB:ADD,$DATE,SCHEDULE,JOB,FREQCODE,PARAM1=DAILY;PARAM2=TEST;PARAM3=JOB```

**Result**

When those tokens are resolved at job run time, they will become: ```DAILY,TEST,JOB```.

:::

### Example WFL

:::tip Example 

The following example is a sample WFL:

```

?BEGIN JOB SMA/EVENT/ILLUSTRATION;
TASK T1, T2;

% Specifying the SAM ID and SAM password
RUN PROG1 [T1];
IF T1 ISNT COMPLETEDOK THEN
RUN *SMA/EVENTGEN
("SAMuser","SAMpassword"SAMpassword","$NOTIFY:LOG,<Severity>,<EventID>,<Msg>")
ELSE
RUN *SMA/EVENTGEN
("SAMuser","SAMpassword","$SCHEDULE:RELEASE,<schedule date>,<schedule name>");
% Using the default SAM ID and SAM password from the LSAM configuration file
RUN PROG2 [T2];
IF T2 ISNT COMPLETEDOK THEN
RUN *SMA/EVENTGEN
("","","$CONSOLE:DISPLAY,PROG2 FAILED");
?END JOB

```

:::
