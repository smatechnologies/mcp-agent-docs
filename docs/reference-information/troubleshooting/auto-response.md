# AutoResponse Troubleshooting

## Display Monitor Rules not Applied

#### Full Description

AutoResponse is configured, but does not appear to be responding to displays.
 
#### First Possible Explanation:
 
The global displays file is missing. Effective with MCP LSAM 04.14.02, this file is no longer required.

###### First Operator Response:

Create a \*SMA/DISPLAYS/xxx file. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/file-monitor#files-rules).

#### Second Possible Explanation:
 
The global displays file is under a different usercode than the LSAM.

###### Second Operator Response:

Change the usercode of the \*SMA/DISPLAYS/xxx file to the correct usercode, or copy it under the correct usercode. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/file-monitor#files-rules).

#### Third Possible Explanation:
 
The display is not correctly defined in the displays file.

###### Third Operator Response:

Run the \*SMA/DISPLAY/HANDLER/xxx in debug mode to troubleshoot the entry. For more information on this response, refer to \*[SMA/DISPLAY/HANDLER](../../operations-and-components/optional-programs-and-files#smadisplayhandler-associated-files).

#### Fourth Possible Explanation:
 
The display message has not yet been processed by the \*SMA/DISPLAY/HANDLER.

###### Fourth Operator Response:

Query the \*SMA/DISPLAY/HANDLER/xxx to determine the display message backlog. This is accomplished by delivering an AX COUNT to the \*SMA/DISPLAY/HANDLER and observing the response on the system console.
 
## External Events not Sent to SAM

#### Full Description

External Events do not appear to have been sent to the SAM.
 
#### First Possible Explanation:
 
Communication between the SAM and the LSAM is not active.

##### First Operator Response:

Verify the LSAM is up and is communicating with the SAM. For information on verifying LSAM communication, refer to [Machines](https://help.smatechnologies.com/opcon/core/objects/machines) in the Concepts online help.

#### Second Possible Explanation:
 
External event is sent to SAM, but an error is reported in the critical log.

##### Second Operator Response:
Verify the external token is the correct external events token and is not the Enterprise Manager password. For more information on this response, refer to [Update the Configuration File](../../additional-features/lsam-features/user-defined-restart-checkpoints#update-the-configuration-file).

## Changes to Display Monitor Rules not Applied

#### Full Description

Displays file changes were not applied.
 
#### Possible Explanation:
 
The \*SMA/DISPLAYS/xxx file was modified, but the *SMA/DISPLAY/HANDLER/xxx program was not notified of the changes.

##### Operator Response:

After making modifications to the \*SMA/DISPLAYS/xxx file, copy it under the LSAM's usercode and deliver an "AX REFRESH" to the \*SMA/DISPLAY/HANDLER/xxx program. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/file-monitor#files-rules).
 
## Title Missing "." @41800

#### Full Description

ATTRIBUTE ERROR:JOB-DISPLAYS TITLE MISSING "." @41800 is displayed by \*SMA/DISPLAY/HANDLER/xxx.
 
#### Possible Explanation:
 
The job's File Title field on the Enterprise Manager's Job Details screen contains WFL parameters.

##### Operator Response:

After making modifications to the \*SMA/DISPLAYS/xxx file, copy it under the LSAM's usercode and deliver an "AX REFRESH" to the \*SMA/DISPLAY/HANDLER/xxx program. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/file-monitor#files-rules).
 
## Jobs Stuck in "Waiting" State

#### Full Description

Jobs stay in a waiting state too long.
 
#### Possible Explanation:
 
The Idle Timer is configured for a long interval.

##### Operator Response:

Reduce the Idle Timer. For more information on this response, refer to [Idle Timer](../../additional-features/lsam-features/resource-monitor#smafilemonitor-behavior).

:::info Note 

MCP LSAM version 04.09.00 or higher is required in order to configure the Idle Timer.

::: 

## High Message Count

#### Full Description

Actions associated with defined messages are not occurring and the MSGCOUNT inquiry indicates a very high number of messages awaiting processing.
 
#### Possible Explanation:
 
The message tokens defined are not adequately unique for the site.

##### Operator Response:

* There are two perspectives involved – the cause of this issue and the short-term resolution. To determine the cause of this issue, you must analyze the \*SMA/DISPLAYS and \*SMA/DISPLAYS/SYSMSG files to determine if you are using common terms as message tokens, i.e., FILE, ENTER, DATE, COPIED, PACK, or a term that may be often-used in displays at your site.

There are two possible reactions to the present situation:

* Allow processing to continue and see if the message count decreases on its own,
\- or -
* Stop the LSAM and remove the \*SMA/DISPMSG/FILE – be advised that any actions associated with messages in the backlog will NOT occur and you will need to manually attend to any downstream processes that would have been impacted by these actions.