# Command-line Interface Utility

The Command-line Interface Utility forwards commands to specified processes on the MCP system. The process may be the MCP itself or may be any other process in an active or waiting state.

## Using SMA/COMMAND

The SMA/COMMAND program parameters are the name of the target process and the command to be passed to the process.
 
Because processes initiated via a RUN command are limited to a single parameter when initiated using OpCon or CANDE, it is necessary to initiate the \*SMA/COMMAND program using a WFL. The program may be contained in a user-written WFL or initiated using the SMA/WFL/COMMAND WFL. Refer to [Using *SMA/WFL/COMMAND](/additional-features/utilities/sma-wfl-command).
 
*SMA/COMMAND will fail if any of the following conditions are true:

1. There is no active or waiting process with a name matching the target string - or -
2. The command is supported by SETSTATUS and is not syntactically correct - or -
3. The command is not applicable given the current state of the target process (i.e., attempting to deliver an OK to a job that is not expecting an OK). The program does not determine the success or failure of the command once submitted. If the \*SMA/COMMAND program is successful in submitting the command, the \*SMA/COMMAND program completes successfully regardless of whether the command was accepted and acted upon by the target process. For this reason, it is important that both target process names and commands be syntactically correct, and exercised in a test environment prior to implementation in the production environment. If the \*SMA/COMMAND program is not successful in submitting the command to the target process (or MCP), the \*SMA/WFL/COMMAND job will be reported as failed.

SMA/COMMAND must be run as a privileged process. The SMA/INSTALL program grants the necessary privileges during installation or upgrade.

### Syntax

:::info Note

The wrapping of the syntax in this document does not indicate the location of a carriage return; the ↵ indicates the location of a carriage return.

:::

The syntax for running the SMA/COMMAND program is:

```RUN *SMA/COMMAND("<Target Process>","<Command>") ↵```

* ```<Target Process>``` is the process receiving the command.
    * The process may be:
        * A user-written or system program.
        * The MCP.
    * The usercode is omitted when specifying the target process.
* The command must be syntactically correct as though it were being entered from the ODT. Some suggestions for use are:
    * Enable/disable COMS programs in conjunction with batch processing.
    * Pass commands to the IPS program in a check processing environment.
    * Manipulate network entities using the MCP as the target process and an "NW…" command.
    * Issue an MCP PRIMITIVE RUN command.

## Using SMA/WFL/COMMAND

Via the Enterprise Manager, the SMA/WFL/COMMAND WFL forwards commands to specified processes on the MCP system. The process may be the MCP itself, or any other process in an active or waiting state. The \*SMA/WFL/COMMAND string parameters are the name of the target process and the command to be passed to the \*SMA/COMMAND program.
 
### Initiate a Command

Use the Command-line Interface through the Enterprise Manager to initiate a command.

1. Enter the SMA/WFL/COMMAND in the **File Title** field on the Job Details screen.

2. Enter the target process and command in the **Arguments** field.

## Examples

:::tip Example

The following example illustrates disabling the online COMS program ACCTSPROG in advance of batch processing:
 
On the MCP Job Details screen, enter:

1. File Title field: ```*SMA/WFL/COMMAND```

2. Arguments field: ```"*SYSTEM/COMS","SM DISABLE PROGRAM ACCTSPROG"```

Upon completion of batch processing, a separate job could then enable the ACCTSPROG program.

:::

:::tip Example

The following example illustrates the initiation of SYSTEM/COMS using an PRIMITIVE RUN command:
 
On the MCP Job Details screen, enter:

1. File Title field: ```*SMA/WFL/COMMAND```

2. Arguments field: ```"MCP","PRIMITIVE RUN *SYSTEM/COMS"```

:::

:::tip Example

The following example is a list of the SMA/WFL/COMMAND file:

```

00000100?BEGIN JOB RUN/COMMAND (STRING PARM1, STRING PARM2);
00000200 TASK T;
00000300 RUN *SMA/COMMAND (PARM1, PARM2) [T];
00000400 IF T ISNT COMPLETEDOK THEN
00000420 BEGIN
00000440 DISPLAY (PARM1);
00000460 DISPLAY (PARM2);
00000500 ABORT "SMA/COMMAND failed";
00000550 END;
00000600END JOB

```

:::