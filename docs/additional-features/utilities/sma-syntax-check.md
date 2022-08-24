# *SMA/SYNTAX/CHECK

This utility is used to validate the syntax of the contents of the definitions files used by various LSAM modules. These definitions files include \*SMA/DISPLAYS, \*SMA/DISPLAYS/SYSMSG, \*SMA/FILEMON/DEFS and \*SMA/PERFMON/DEFS. SMA Technologies strongly encourages the use of this utility prior to implementing a definitions file within the production environment in order to minimize the potential for disruption to production processing. The SMA/RESOURCE/MONITOR also automatically executes SMA/SYNTAX/CHECK at BOJ and upon being notified of a new definitions file.
 
After manually initiating the program, you will be asked to identify the type of file to be analyzed. There are four possible responses:

* D = Displays definition (Automated Response)
* F = File Monitor definitions file
* P = Performance Monitor definition file
* Q = Quit

After specifying the type of file, you will be asked to provide the file title of the file to be analyzed. Enter the full file title, followed by a period (.).
 
There are several processing options that are controlled by switches. To select the processing option that best suits your environment, set/reset the appropriate switches, as described below:

* SW1 = TRUE
    * When set, SW1 enables the user to analyze multiple files during one execution of the \*SMA/SYNTAX/CHECK utility. After each file has been analyzed, you will again be prompted to enter the type of file. When you have finished analyzing all the files, quit the program by supplying a file type of "Q".
* SW2 = TRUE
    * When set, SW2 will cause all records analyzed to be recorded in the debug print file even if they contain no errors.
* SW3 = TRUE
    * When set, SW3 will cause the utility to P-DS if any errors are located in the definitions file.

If both SW1 and SW3 are used, the utility will analyze multiple files UNTIL a file containing an error is found, at which point the utility will self-destruct with a P-DS condition.
 
You could also configure this utility to run within a WFL if the system option QUEUEDAX is set:

```

?BEGIN JOB VERIFY/SMA/FILES;
RUN *SMA/SYNTAX/CHECK; SW1;
AX = D; AX = (MYUSER)TEST/DISPLAYS ON TESTPK.;
AX = D; AX = (MYUSER)TEST/DISPLAYS/FOR/MYJOB ON TESTPK.;
AX = D; AX = (MYUSER)TEST/DISPLAYS/SYSMSG ON TESTPK.;
AX = F; AX = (MYUSER)TEST/FILEMON ON TESTPK.;
AX = P; AX = (MYUSER)TEST/PERFMON ON TESTPK.;
AX = Q;
?END JOB

```

After each file is analyzed, one of the following messages will be displayed:

```

"Errors found - See edit report."
"Congratulations! All records passed."

```

If analyzing multiple files, all results will appear within a single edit report, along with the following attributes of each file: FILENAME, FAMILYNAME, ALTERDATE, ALTERTIME, number of records in file.

## Application

SMA Technologies recommends using the capabilities of SMA/FILE/MONITOR to monitor for changes to any of the definitions files. Upon the file being altered, add an OpCon job which runs \*SMA/SYNTAX/CHECK to the daily schedule, setting SW3 = TRUE. 

If the Syntax Check job completes OK, start OpCon job(s) that run \*SMA/COMMAND to deliver the appropriate AX (FILEMON, PERFMON, SYSMSG) to the appropriate programs (\*SMA/RESOURCE/MONITOR, \*SMA/FILE/MONITOR, \*SMA/DISPLAY/HANDLER). 

In this way, you can minimize the possibility that critical actions fail to occur due to syntax errors within a definitions file or due to failure to notify the appropriate programs that a new definitions file is to be implemented.