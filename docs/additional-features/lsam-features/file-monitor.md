# File Monitor

File Monitor takes user-defined actions upon the attainment of various file conditions which occur against a user defined set of files. When the file meets the criterion, File Monitor sends external events to the SAM and supporting services (SAM-SS), and/or sends selected MCP commands to the MCP operating system. File Monitoring criteria include:

* Achievement of a user-defined percentage of maximum allowable size
* Absence or removal
* Existence
* Modification

:::info Note

The actions associated with file existence occur only when the file is **entirely** created.

:::

File Monitor runs as a privileged process under Resource Monitor if: 

1) enabled within the configuration file 

and 

2) a valid \*SMA/FILEMON/DEFS file is present. The \*SMA/INSTALL program automatically applies the necessary privileges during an installation or upgrade.
 
Upon initiation, the File Monitor interrogates the status of all files defined within the definitions file, \*SMA/FILEMON/DEFS. If the monitored condition exists and the file has been altered since the last time File Monitor was active, the actions associated with the file will be performed. This behavior will also occur of the user delivers an AX RESTART to the \*SMA/FILE/MONITOR program.

## Update the Configuration Files

Modify the following fields under [Optional Modules (OPT)](../../operations-and-components/sma-manager/optional-modules) and General [LSAM Configuration (GEN)](../../configuration/general-lsam-configuration):

a. **File Monitor**: Set to a value of ```Y```.

b. **OpCon user and OpCon Event Token**: If a default user name and external token have not been entered for external events (for File Monitor, Automated Response, and EventGen), enter the *OpCon User ID* and the OpCon External Token.

## Start the File Monitor

The File Monitor is started by the Resource Monitor. Refer to the discussion of the [Resource Monitor](../../additional-features/lsam-features/resource-monitor) (*SMA/RESOURCE/MONITOR) for further details.

## File Monitor Data File

The File Monitor Definitions File (\*SMA/FILEMON/DEFS/xxx) contains the file names and conditions to be monitored, optionally the time of day during which to monitor for the file condition, and the OpCon event(s) and/or MCP command for each file. The \*SMA/FILEMON/DEFS/xxx file is examined at the beginning of each processing cycle and upon being notified of a new \*SMA/FILEMON/DEFS file by the Resource Monitor. An error report is produced as a printer backup file. For a list of possible File Monitor errors and their descriptions, refer to [File Monitor Messages](../../reference-information/file-monitor-messages).

## Files Rules

1. Edit the \*SMA/FILEMON/DEFS/xxx file using the *SMA/MANAGER program (?ON SMAMGRxxx). Select the FILEMENU choice, and edit/insert/delete records as desired.
2. Save your changes.
3. The File Monitor Data File is dynamic. After updating the file, From the Main Menu, select the LOADFILE choice.
4. Any number of events are allowed for each file record.
5. Blank lines are allowed. A percent sign (%) in position one of any record also causes that record to be treated as a comment record.
6. The first position in each record must indicate the record type:
    * F: Indicates a file record.
    * M: Indicates an MCP command to be delivered to the MCP operating system. The command should not be followed by a period (.) or any other punctuation.
    * S: Indicates an OpCon event to be sent to the SAM-SS. The event should not be followed by a period (.) or any other punctuation.
    * %: Indicates a comment record.
7. At least one M or S record must follow each F record.

To view the previous procedure, refer to [File Rules](../../reference-information/legacy#file-rules) in the Legacy Information topic.

### F Rules

Wildcarded file names are supported in the following fashion:

* An equals sign (=) may be used as a wildcard character in the following instances:

    * at the end of a filename:

        (UC)DATA= will match (UC)DATA, (UC)DATA123, (UC)DATA/XYZ/ABC

    * to replace an entire ending filename node:

        (UC)DATA/= will match (UC)DATA/123, (UC)DATA/XYZ/ABC

    * to replace an entire embedded filename node:

        (UC)DATA/=/FILE will match (UC)DATA/123/FILE, (UC)DATA/VWXYZ/FILE
        
* A question mark (?) may be used as a wildcard character to mask specific characters. Each question mark represents a single character (or /) in the filename:
    * (UC)DA?A/123 will match (UC)DATA/123, (UC)DANA/123, and (UC)DA/A/123, but will NOT match (UC)DATA123.
    * (UC)DA??D will match (UC)DATAD, (UC)DA12D, (UC)DARED, and (UC)DAY/D, but will NOT match (UC)DAY/D123.

* Wildcard characters may NOT be combined within a single file definition. Multiple question marks can be used in a file definition or multiple equals signs (=) in a file definition, but both question marks and equals signs can NOT be used within the same file definition.
    * These are valid definitions: (UC)MY/D???Y/FILE/2008????, (UC)MY/=/FILE=
    * This is NOT a valid definition: (UC)/MY/D???Y/FILE/= because both ? and = are present.

* Also effective with MCP LSAM 04.13.00, file monitoring is not performed at a configured interval; changes to monitored files will be recognized by the insertion of a "File Status" entry in the system log. This eliminates the timing issues previously observed on occasion for volatile files which were monitored for presence or absence.

* The syntax for listing files in the F record must use the following format:
```<FILE TITLE>```.,```<CONDITION>```

* If there is insufficient space in the "F" record to fully contain the file title and condition, a continuation "F-" record may be used.

* The file title must include the usercode, filename, and family name; wildcard characters may be used. Wildcarding rules for File Monitor are identical to those used with the MCP procedure ASERIES_INFO.

* The file title must be followed by a period (.) and a comma (,).

* The file condition may be any of the following:
    * PRESENT - The file is present on the ClearPath MCP or was created during the processing cycle.
    * ALTERED - The file was altered or created during the processing cycle.
    * DELETED - The file is not present or was removed during the processing cycle.
    * WARN=## - The file has reached a specified percentage of maximum allowable size. Replace the pound signs (##) with the desired percentage (e.g., 10, 50, 90).

:::info Note

The actions associated with file creation occur only when the file is **entirely** created.

:::

### F- Record

* This definition record is used to continue the (F)ile definition started in the "F" record. The "F-" record is ONLY used when there is insufficient space in the "F" record to define the file title and condition in the preceding "F" record.

* If it is necessary to use the "F-" continuation record, the comma and file condition must be placed in the "F-" record.

* The continuation of the file title must start immediately after the "-" in the "F-", otherwise the file name or family will contain a space (and this will result in an invalid file title).

### F2 Record

* This definition record is used to specify an optional time frame during which to monitor for the file condition defined in the preceding "F" record.

* The format is:
    * F2 ```<time to start monitoring>```,```<time to stop monitoring>```

* The time to start monitoring must be earlier than the time to stop monitoring.

* Both times use a 24-hour clock format.

* If you want to monitor from before midnight until after midnight, create two separate file monitor definitions with one monitoring from the start time until 2400 and the other monitoring from 0000 until the stop time.

### M Record

* The syntax for MCP commands in the M record must use the following format:
    * M```<MCP command>```

* The first position defines the record type.

* The MCP command must immediately follow the M.

* Valid MCP commands are:

    * CHANGE TO ```<new file title, including usercode and family name>```

    * COPY AS ```<new file title, including usercode and family name>```

    * DISPLAY ```<message to be displayed on the system console>```

    * REMOVE ```<file title, including usercode and family name>```; or the token ```<FILE>```
        * The token ```<FILE>``` may be used with the DISPLAY and REMOVE commands as an abbreviated method of passing the file title to the MCP command. This is done to overcome the length restrictions of the SEQDATA record.

:::tip Example

The following example is an abbreviation that can be used to overcome the length restrictions:

```

MDISPLAY "<FILE> HAS ARRIVED" or MREMOVE <FILE>

```

:::

### S Record

* The syntax for OpCon events in the S record(s) must use the following format:
    * S$```<OpCon EVENT>```

* The first position defines the record type.

* The dollar sign ($) must follow the S.

* A valid OpCon event must follow the dollar sign ($). For a list of valid OpCon events, refer to Introduction in the OpCon Events online help.

* If there is insufficient space in the "S" record to fully contain the file title and condition, a continuation "S-" record may be used. The ```<FILE>``` token may be used within the OpCon external events. All references to the token ```<FILE>``` are replaced with the full file title of the monitored file.

### S- Record

This definition record is used to continue the event definition started in the "S" record. The "S-" record is ONLY used when there is insufficient space in the "S" record to define the entire external event.

:::tip Example

The following example is a \*SMA/FILEMON/DEFS/xxx file:

```

00000100F(ADMIN)SOME/VOLATILE/FILE ON MYPACK.,WARN=80
00000200S$CONSOLE:DISPLAY, <FILE> IS GETTING BIG
00000300S$JOB:ADD,[[$DATE]],DAILYSCH,FILEREFRESH,DAILY
00000400MDISPLAY "<FILE> IS BIG – FILEREFRESH WILL BE RUN"
00000500MCHANGE TO (PROD)SAVE/VOLATILE/FILE ON MYPACK
00000510% The budget files arrive only in August
00000600F(ACCTG)INCOMING/BUDGET ON ACCTPK.,PRESENT
00000700S$SCHEDULE:RELEASE,[[$DATE]],BUDGETREPT
00000800S$CONSOLE:DISPLAY,RUNNING BUDGET REPORTS
00000900MCOPY AS (PROD)PERMANENT/FILE ON MYPACK
00001000MREMOVE <FILE>

```

:::