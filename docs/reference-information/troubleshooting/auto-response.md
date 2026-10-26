---
title: AutoResponse Troubleshooting
description: "Troubleshooting guidance for common AutoResponse issues including display monitor rules not applied, external events not sent, and high message count conditions."
tags:
  - Reference
  - System Administrator
  - Operations Staff
  - Agents
---

# AutoResponse Troubleshooting

## Display Monitor Rules not Applied

#### Full Description

AutoResponse is configured, but does not appear to be responding to displays.
 
#### First Possible Explanation:
 
The response is defined at the global level, but the global displays file is missing. Effective with MCP Agent 04.14.02, the global displays file is optional, so the MCP Agent starts normally and reports no error when the file is absent — it simply has no global entries to match against.

*First Operator Response:*

Create a \*SMA/DISPLAYS/xxx file under the agent's usercode, then select the LOADDISP choice on the SMA/MANAGER Main Menu and select the Global Displays file. Alternatively, define the response in a job-specific or template displays file, which takes effect without a reload. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/automated-response.md#file-rules).

#### Second Possible Explanation:
 
The global displays file is under a different usercode than the agent.

*Second Operator Response:*

Change the usercode of the \*SMA/DISPLAYS/xxx file to the correct usercode, or copy it under the correct usercode. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/automated-response.md#file-rules).

#### Third Possible Explanation:
 
The display is not correctly defined in the displays file.

*Third Operator Response:*

Run the \*SMA/DISPLAY/HANDLER/xxx in debug mode to troubleshoot the entry. For more information on this response, refer to \*[SMA/DISPLAY/HANDLER](../../operations-and-components/optional-programs-and-files.md#smadisplayhandler-associated-files).

#### Fourth Possible Explanation:
 
The display message has not yet been processed by the \*SMA/DISPLAY/HANDLER.

*Fourth Operator Response:*

Query the \*SMA/DISPLAY/HANDLER/xxx to determine the display message backlog. This is accomplished by delivering an AX COUNT to the \*SMA/DISPLAY/HANDLER and observing the response on the system console.
 
## External Events not Sent to SAM

#### Full Description

External Events do not appear to have been sent to the SAM.
 
#### First Possible Explanation:
 
Communication between the SAM and the agent is not active.

##### First Operator Response:

Verify the agent is up and is communicating with the SAM. For information on verifying agent communication, refer to [Machines](https://help.smatechnologies.com/opcon/core/objects/machines) in the Concepts online help.

#### Second Possible Explanation:
 
External event is sent to SAM, but an error is reported in the critical log.

##### Second Operator Response:
Verify the external token is the correct external events token and is not the Enterprise Manager password. For more information on this response, refer to [General LSAM Configuration (GEN)](../../configuration/general-lsam-configuration.md).

## Changes to Display Monitor Rules not Applied

#### Full Description

Displays file changes were not applied.
 
#### Possible Explanation:
 
The \*SMA/DISPLAYS/xxx file was modified, but the *SMA/DISPLAY/HANDLER/xxx program was not notified of the changes.

##### Operator Response:

After making modifications to the \*SMA/DISPLAYS/xxx file, copy it under the agent's usercode and deliver an "AX REFRESH" to the \*SMA/DISPLAY/HANDLER/xxx program. For more information on this response, refer to [File Rules](../../additional-features/lsam-features/automated-response.md#file-rules).
 
## Title Missing "." @41800

#### Full Description

ATTRIBUTE ERROR:JOB-DISPLAYS TITLE MISSING "." @41800 is displayed by \*SMA/DISPLAY/HANDLER/xxx.
 
#### Possible Explanation:
 
The job's File Title field on the Enterprise Manager's Job Details screen contains WFL parameters. The \*SMA/DISPLAY/HANDLER/xxx builds the job-specific displays file title from this field, and the parameters make the resulting title invalid.

##### Operator Response:

Remove the WFL parameters from the **File Title** field on the Job Details and supply them through the job's parameter fields instead. If the job requires parameters in the File Title field, enter a template file name on the Job Details so the \*SMA/DISPLAY/HANDLER/xxx builds the title from the template name. For more information on template displays files, refer to [Create the Necessary Displays File(s)](../../additional-features/lsam-features/automated-response.md#create-the-necessary-displays-files).
 
## Jobs Stuck in "Waiting" State

#### Full Description

Jobs stay in a waiting state too long.
 
#### Possible Explanation:
 
The Idle Timer is configured for a long interval.

##### Operator Response:

Reduce the Idle Timer. For more information on this response, refer to [Communication Parameters (COMM)](../../configuration/communication-parameters.md).

:::info Note 

MCP Agent version 04.09.00 or higher is required in order to configure the Idle Timer.

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
* Stop the agent and remove the \*SMA/DISPMSG/FILE — be advised that any actions associated with messages in the backlog will NOT occur and you will need to manually attend to any downstream processes that would have been impacted by these actions.