---
title: Set Up Failure and Status Message Logic
description: "Understand and configure how the MCP LSAM determines job success or failure using the JOB TO BE FAILED flag, Fail Codes, Fail Resets, and task-level checking."
tags:
  - Conceptual
  - Automation Engineer
  - System Configuration
  - Agents
---

# Set Up Failure and Status Message Logic

## What is it?

This page explains the interaction between the JOB TO BE FAILED flag, Fail Code and Fail Reset matching, task-level checking settings, and task-completion messaging to determine how MCP job outcomes are reported in Enterprise Manager Operation. It provides reference tables for all combinations of these conditions and their resulting status messages.

- Use this page when configuring Fail Codes and Fail Resets on MCP job definitions to understand exactly when the MCP Agent reports a job as failed versus finished OK, and which status message will appear in the Enterprise Manager.
- Use this page to evaluate the effect of enabling task-level checking so that subordinate task failures are surfaced in job history without requiring WFL-level ABORT coding.

An MCP job's status in Enterprise Manager Operation relies on several configuration settings: Fail Immediately on Fail Code, Send Fail/Reset Message, Task-Failure Checking, and Task-Completion Message. (Refer to the configuration file tables starting in [Processing Variables (VAR)](../configuration/processing-variables.md).) If a job is not failed immediately, the internal JOB TO BE FAILED flag also plays an important role.

## Job to be Failed Flag

The JOB TO BE FAILED flag, set per job, ultimately determines the final status of MCP jobs run through the MCP Agent. The agent checks this flag when the job terminates. If the flag is set to the default "N", the agent reports the job as successful. If the flag is set to "Y", the agent reports a job's failure, even if the operating system reports a job's success.

During the processing of a job or a task, a match between the console display and the words entered in the Fail Code or Fail Reset fields determines the JOB TO BE FAILED flag's setting. A Fail Code match sets the flag to "Y" and a Fail Reset match sets the flag back to "N". Refer to [Failure Criteria](https://help.smatechnologies.com/opcon/core/job-types/mcp#failure-criteria) in the Concepts online help. Regardless of the actual outcome of the job or tasks, the final value of the JOB TO BE FAILED flag decides the success or failure in Enterprise Manager Operation.

## Fail Code and Fail Reset Logic

Use of Fail Codes is an alternative solution to programming a WFL to ABORT if a program IS NOT COMPLETED OK. Use of Fail Resets provides greater flexibility in assigning job statuses. For example, a critical application's success can reset the JOB TO BE FAILED flag despite the failure of other non-critical tasks. Refer to [Failure Criteria](https://help.smatechnologies.com/opcon/core/job-types/mcp#failure-criteria) in the Concepts online help.

### How the Agent Matches Fail Code and Fail Reset Text

The MCP Agent compares the text in the Fail Code and Fail Reset fields against the console display using the following rules. All four fields, two Fail Codes and two Fail Resets, are compared the same way.

* **Each entry must end with an asterisk (`*`).** The asterisk marks the end of the text to compare. An entry without an asterisk is never compared against any display.
* **The comparison starts at the character immediately after the first colon (`:`) in the display.** If the display contains no colon, the comparison starts at the beginning of the display text.
* **The comparison is case-sensitive.** `out of*` does not match the display text `OUT OF BALANCE`.
* **Only the text before the asterisk is compared**, up to a maximum of 40 characters, so the entry matches a display that begins with that text.

Because the comparison begins immediately after the colon, any space that follows the colon in the display is part of the text being compared. For the console display `POST: OUT OF BALANCE`, the compared text begins with a space:

| Fail Code entry | Matches | Reason |
| --------------- | ------- | ------ |
| `OUT OF*` | No | The compared text starts with the space that follows the colon |
| ` OUT OF*` (the entry begins with a space) | Yes | The leading space matches the space that follows the colon |
| `out of*` | No | The comparison is case-sensitive |
| `OUT OF BALANCE` | No | The entry does not end with an asterisk |

:::tip

Enter the Fail Code exactly as the console shows it, including capitalization, starting from the character after the first colon, and end it with an asterisk.

:::

The next table shows all the factors involved in using the Fail Code/Fail Reset feature. Use the table to configure the MCP Agent's behavior upon a Fail Code or Fail Reset match.

### Fail Code/Fail Reset Conditions

| Console Match | Fail Immediately on Fail Code | Job to be Failed | Send Fail/Reset Message | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ------------- | ----------------------------- | ---------------- | ----------------------- | -------------------------------------- |
| Fail Code | Y | N/A | A, F | JJJJJ/TTTTTFAILCODE, then JJJJJ/TTTTTFAIL MSG |
| Fail Code | Y | N/A | R, N | JJJJJ/TTTTTFAIL MSG |
| Fail Code | N | Set to Y | A, F | JJJJJ/TTTTTFAILCODE |
| Fail Code | N | Set to Y | R, N | ```<NONE>``` |
| Fail Reset | N | Set to N | A, R | JJJJJ/TTTTTRESETCODE |
| Fail Reset | N | Set to N | F, N | ```<NONE>``` |

## Task-Level Checking

Task-level checking enables the MCP Agent to report a job as failed to Enterprise Manager Operation when a job's subordinate task fails. Display messages issued by the job do not determine the job completion status; job completion status is determined solely by the completion status of the subordinate task(s). With task-level checking enabled, the failure of any single task in a WFL marks the job as failed or sets the JOB TO BE FAILED flag to Y. 

If defined, Fail Codes and/or Fail Resets are applied to tasks regardless of the task-level checking setting. For more information on configuration settings, refer to [Processing Variables (VAR)](../configuration/processing-variables.md). When the MCP Agent is configured to report at the task level (A or F), the Enterprise Manager's job history includes the completion status of each task. 

The next table shows all the factors involved in task-level checking. Use the table to configure the MCP Agent's behavior upon a task's failure or success.

### Task-Level Checking Conditions

| Task | Task-Level Checking | Job to be Failed	| Task-Completion Message | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ---- | ------------------- | ---------------- | ----------------------- | -------------- |
| FAIL | I | N/A | A, F | The task's own ending status, then JJJJJ/TTTTTTASK FAIL |
| FAIL | I | N/A | N | JJJJJ/TTTTTTASK FAIL |
| FAIL | T | Set to Y | A, F | The task's own ending status, then JJJJJ/TTTTTTASK FAIL at end of job |
| FAIL | T | Set to Y | N | JJJJJ/TTTTTTASK FAIL at end of job |
| FAIL | T | Reset to N by a Fail Reset | A, F | The task's own ending status, then JJJJJTASK(S) FAILED at end of job |
| FAIL | T | Reset to N by a Fail Reset | N | JJJJJTASK(S) FAILED at end of job |
| OK | I,T | N/A | A | JJJJJ/TTTTTCOMP OK |
| OK | I,T | N/A | F, N | ```<NONE>``` |

A failing task's own ending status is the status the ClearPath MCP reported for that task, such as JJJJJ/TTTTTDS, JJJJJ/TTTTTF DS, or JJJJJ/TTTTTP DS. The MCP Agent sends it whenever Task-Completion Message is any value other than N.

With task-level checking set to I, the agent fails the job as soon as the task fails. With T, it records the failure and sends TASK FAIL when the job ends, so the job keeps running in the meantime.

## Final Status

If a job is not failed immediately, the JOB TO BE FAILED flag determines the success or failure of a job in Enterprise Manager Operation. If the flag is set to Y for multiple reasons, Enterprise Manager Operation takes the last job or task status.

If the flag is N, the job finishes OK, but the status message depends on whether any subordinate task failed. If no task failed, the final status is JJJJJCOMPLETED. If one or more tasks failed and the flag was never left at Y, the agent sends JJJJJTASK(S) FAILED with the same Finished OK job status.

:::info Note

JJJJJTASK(S) FAILED is a Finished OK status, not a failure. It means the WFL itself completed and at least one task inside it did not. To have the job reported as failed instead, set task-level checking to I or T, or code the WFL to ABORT.

:::

### Job To Be Failed Flag Effects


| Job to be Failed | Final Status | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ---------------- | ------------ | --------------------------------------------------------------------------------- |
| Set to Y by a Fail Code match | FAILED | JJJJJ/TTTTTFAIL MSG |
| Set to Y by a task failure | FAILED | JJJJJ/TTTTTTASK FAIL |
| Set to N, no task failed | FINISHED OK | JJJJJCOMPLETED |
| Set to N, one or more tasks failed | FINISHED OK | JJJJJTASK(S) FAILED |

