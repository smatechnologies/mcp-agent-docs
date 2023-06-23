# Automated Response

The Automated Response (AutoResponse) feature allows the MCP LSAM to respond to messages displayed on the MCP console. The predefined MCP LSAM responses can be sent to the MCP or to the Schedule Activity Monitor (SAM).
 
The following types of messages are forwarded to the display handler for Automated Response processing:

* WFL or program displays that appear on the MCP console and appear in the system log, preceded by DISPLAY (the process does not go into the waiting mix).
* WFL or program displays that appear on the MCP console and appear in the system log, proceeded by ACCEPT (the process goes into the waiting mix).
* System messages that appear on the MCP console or appear in the system log. The *SMA/RESOURCE/MONITOR, not the LSAM, captures system messages. The Resource Monitor must be enabled in order to utilize Automated Response for system messages.
* Task/Job completion messages for the OpCon job when this job-level feature is enabled by checking the EOT Notice Message check box on the Job Details. For more information on utilizing this feature, refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help. Possible completion status values are "EOT", "EOJ", and "DS". Explicit reasons for job/task discontinuance are not included in the display to simplify creation of the automated response entries in the displays files. All forms of DS (e.g., I-DS, F-DS, O-DS, P-DS, etc.) are denoted as "DS".

## Update the Configuration File

If Automated Response was not activated during the installation, the configuration file must be updated.
 
Modify the following fields under [Optional Modules (OPT)](../../configuration/optional-modules):

a. **Autoresponse**: Set to a value of **Y**.

b. **Resource Monitor Freq**: To capture and analyze messages emitted by processes started outside the LSAM, enter the *frequency*, in seconds, that the Resource Monitor should sample for system metrics. While this frequency value has no bearing on the processing of system messages, a value must be defined in order for the Resource Monitor to run.

## Automated Response Data File

### Create the Necessary Displays File(s)

A Displays File contains the definition of the MCP tokens to compare to a console message and also contains the action to take when a match is found. An token is defined as a word (a contiguous group of one or more letters, numbers, and/or special characters) preceded and followed by a single blank space. If more than one space separates the text of a message, each additional space is counted as one token when calculating the ordinal position of the target text.
 
The following four kinds of Displays Files are allowed:

* **Global**: Entries in the Global Displays File apply to all jobs initiated by the LSAM. Careful consideration should be given to the number of entries in the Global Displays File, particularly if the volume of display messages emitted in the site's environment is high. When Automated Response is activated, each message displayed by an OpCon job is processed by the LSAM and compared to the entries within the Global Displays File. In a display-intensive environment, this can lead to delays in processing if the Global Displays File is in use.
 
More efficient processing can be achieved by using Template or Job-specific Displays Files in lieu of a Global Displays File when possible. Please note that this approach does result in a greater number of individual Displays Files.
 
If you suspect that you are experiencing a delay due to high display message volume, you may determine the number of display messages waiting to be processed by selecting the MSGCOUNT choice of the SMAMGR Main Menu. The display message backlog will be returned. To view the previous information, refer to [Create the Necessary Displays File(s)](../../reference-information/legacy#create-the-necessary-displays-files) in the Legacy Information topic.

* The Global Displays File is optional and, if used, must be named \*SMA/DISPLAYS/xxx.
* The Global Displays File is not dynamic. After updating \*SMA/DISPLAYS/xxx, issue the AX REFRESH command to the \*SMA/DISPLAY/HANDLER/xxx to reload the Displays File.

The Global Message Definitions File is not dynamic. After updating the *SMA/DISPLAYS/xxx, instruct the LSAM to reload the Definitions File using the LOADDISP option of SMA/MANAGER and selecting the Global Displays file.

* **Template**: Entries in Template Displays File are only applied to the associated jobs. The use of a Template Displays File precludes the use of a job-specific Displays File for that job. Template Displays Files are associated with specific OpCon jobs by denoting the template file name on the MCP Job Details. Template Displays Files must be named \*SMA/DISPLAYS/```<unique template file name>```. Template Displays Files are dynamic. There is no need to reload the file after updating a Job-specific or Template Displays File. For further information on the SMA/DISPLAYS template file, refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help.

* **Job-specific**: Entries in Job-specific Displays File are only applied to the associated job. Job-specific Displays Files must be named *SMA/DISPLAYS/```<WFL source file name>``` (without the usercode or familyname). Job-specific Displays Files are dynamic. There is no need to reload the file after updating a Job-specific or Template Displays File.

* **System Message**: Entries in the System Message Definitions File are applied to ALL processes. The System Message Definitions File is not dynamic. After updating the \*SMA/DISPLAYS/SYSMSG/xxx, instruct the LSAM to reload the Definitions File using the LOADDISP option of SMA/MANAGER and selecting the System Message Displays file. The format of the System Message file differs slightly than the format of the other three types of Displays Files.

### Define an Automated Response

1. Decide whether to use the Global Displays File or a Job-specific Displays File. The console displays are matched first against any scenarios defined in the Job-specific Displays File and then matched to any scenarios defined in the Global Displays File.

a. If the Global Displays File is required, use the existing \*SMA/DISPLAYS/xxx file.

b. If a Job-specific Displays File is required, create a SEQDATA file named \*SMA/DISPLAYS/```<WFL source file name>``` (without the usercode or familyname). Use SMA/MANAGER DISPMENU choice and process through the screens.

2. Create the D record to define the UNIQUE combination of MCP tokens to match within a display. For syntax, refer to File Rules.

3. Create the A and/or S record(s) to define the action to take if a match is found for the specified MCP token(s). For syntax, refer to File Rules.

4. Access the \*SMA/MANAGER program using ?ON SMAMGRxxx.

5. Select the DISPMENU choice.

6. On the SMADISPMENU screen, select the displays file you wish to edit.

7. Edit/insert/delete the desired entries. When finished, enter PARENT in the Action line. You will be asked if you want to save the changes.

8. Return to the Main Menu using the RETURN Action.

9. If the Global Displays File was modified, notify the \*SMA/DISPLAY/HANDLER to refresh its internal tables with the new definitions using the LOADDISP option of the Main Menu of SMAMGRxxx, and selecting the Global Displays file.

10. If the System Messages File was modified, notify the \*SMA/DISPLAY/HANDLER and \*SMA/RESOURCE/MONITOR to refresh its internal tables with the new definitions using the LOADDISP option of the Main Menu of SMAMGRxxx and selecting the System Messages file.

11. If a Job-specific or Template Displays File was modified, no notification is necessary.

To view the previous procedure, refer to [Define an Automated Response](../../reference-information/legacy#define-an-automated-response) in the Legacy Information topic.

### Displays File Rules that Apply ONLY to System Messages

When identifying the tokens in a system message, keep in mind the following:

* The first token of a system message is the identifier of the process that emitted the message.
* The first token of the display will often be preceded by DISPLAY: or ACCEPT:.
* The last token in the message will often be followed by a period (.). Omit trailing punctuation from the message definition.

To illustrate how to comply with these rules, use the system message display: "12345 DISPLAY:This UnIqUe message is from PROG/A." Assume you wish to take action if PROG/A displays this message.
 
The message definition entry might look like this:

```

D#M2=DISPLAY:This #M3=UnIqUe #M7=PROG/A
 
```

:::info Note 

There is no trailing period in this message.

:::

### File Rules

The file rules must be followed exactly for the Automated Response feature to function properly:

* All definitions must start in the first position of the record.
* The first position in each record must indicate the record type:
    * **A**: Indicates an action to be sent to the ClearPath MCP.
    * **D**: Indicates the tokens within the console display message to match.
    * **S**: Indicates an OpCon event to be sent to the SAM-SS. The event should not be followed by a period (.) or any other punctuation.
* Any number of Automated Response scenarios may be defined in each Displays File.
* The maximum line length is 72 characters. Lines cannot be continued to the following line.

#### A Rules

MCP tokens and mix numbers may be used in the A record using the following variables:

* **#A**```<token number>``` is placed in the definition of the action for the MCP token name.

* **<MX#>** is placed in the definition of the action as a variable to indicate where the mix number is to be placed.

* **<JB#>** is placed in the definition of the action as a variable to indicate where the parent WFL mix number is to be placed.

#### D Rules

The syntax for listing MCP token combinations in the D record must use the following format: #M```<token number>=<token value><space>```

* **#M**```<token number>``` defines the ordinal position of the MCP token within the display.
* **=**```<token value>``` defines the value of the MCP token. A space is required between each MCP token listed.

:::info Note 

Do not place a space on either side of the equals sign (=). This results in an invalid definition.

:::

#### S Rules

* In some instances, the user may require more than 71 characters to define an OpCon event. A maximum of 2 records may be used to define the external event:
    * A max of 350 characters may comprise the external event (after any token substitution).
    * External events (S records) that will fit on one line (71 chars) are not to be changed.
    * External events (S records) that require two lines must follow the syntax: S1$```<event>``` and S2```<event>``` where S1 is the first part and S2 is the second part.
        * The syntax must be strictly followed or unexpected results may occur.
* MCP tokens may be used in the S record using the following variable: **#A**```<token number>```.

## Activate the Debug Option

If problems arise while implementing the Automated Response feature, the *SMA/DISPLAY/HANDLER/xxx can run in stand-alone, debug mode using the following steps:

1. Stop the MCP LSAM. Refer to MCP LSAM Operations and Components.
2. Start the Displays Handler: RUN \*SMA/DISPLAY/HANDLER/xxx.
3. Set Switch Four (SW4) to true: ```<mix number of *SMA/DISPLAY/HANDLER/xxx> SW4=TRUE```.

:::info Note 

To turn off the debug switch, use the following syntax:
```<mix number of *SMA/DISPLAY/HANDLER/xxx> SW4=FALSE```

:::

4. Start the WFL that should be waiting for a console display.
5. In debug mode, the operator is prompted for:

a. The mix number of the job/task that produces the display.

b. The name of the WFL that contains the code or program that produces the display.

c. The console display.

## Examples

:::tip Example 

A WFL (JOB1) executes multiple actions and another job (JOB2) is waiting for output from one of the actions in JOB1. Instead of JOB2 waiting until JOB1 finishes completely, the key action in JOB1 can display a unique message after it is completed. As a result, a message is sent to the SAM-SS to start JOB2.

:::


:::tip Example 

A WFL has multiple messages defined. For each message, an operator response is required. The *SMA/DISPLAYS file may be set up to respond automatically to these messages.

:::


:::info Note

The second Example above lends itself more practically to passing the appropriate parameter to the job during scheduling, but the Automated Response tool may prove a useful interim method of addressing the scenario.

:::

### Working with an Example Automated Response

#### Scenario

The OpCon job SampleRun is scheduled to run the MCP job WFL/TEST/JOB. During the course of processing, this job creates a file called EOM/BUDGET/DATA. The WFL also displays the message: ```FILE <file name> WAS CREATED - COPY IT, START BUDGET```.

#### Requirement

The Displays File must be configured to copy the file automatically, send a message to the SAM-SS, and instruct the program to continue.

#### Solution

Complete the following steps to meet the requirements:

1. Determine the number for each token in the display. The tokens in the example display message are:

```

#1 FILE
#2 EOM/BUDGET/DATA or EOY/BUDGET/DATA (depending on run)
#3 WAS
#4 CREATED
#5 -
#6 COPY
#7 IT,
#8 START
#9 BUDGET

```

2. Verify that the Global Displays File exists. The file must be called \*SMA/DISPLAYS/xxx.
3. If the Global Displays File does not exist, you may create one and follow the above directions for modifying a definitions file.
4. Create a file called \*SMA/DISPLAYS/WFL/TEST/JOB.
5. Define the search string and automated response. The displays file contains the following information:

```

000100D#M9=BUDGET #M6=COPY #M4=CREATED
000200S$CONSOLE:DISPLAY,THE #A2 #A1 WAS #A4
000300ACOPY #A2 AS #A2/SAVE
000400A<MX#> AX OK
 
```

Line 000100 defines the combination of tokens that must be matched in a console display. Line 000200 defines an event to be sent to the SAM-SS. Line 000300 defines the action for the file to be copied. Line 000400 instructs the job to continue.

6. The job is submitted, and the mix number is 12345. When a match is found in a console display, the automatic response is:

a. An external event is sent to the SAM-SS with the following information:

```

$CONSOLE:DISPLAY,THE EOM/BUDGET/DATA FILE WAS CREATED,userid,password

```

b. The file on the ClearPath MCP is copied:

```

COPY EOM/BUDGET/DATA AS SAVE/EOM/BUDGET/DATA

```

c. The program is prompted to continue: ```12345 OK```