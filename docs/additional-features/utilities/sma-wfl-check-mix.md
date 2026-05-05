---
title: "*SMA/WFL/CHECK/MIX"
description: "A utility WFL that checks for processes in the MCP Waiting or Scheduled mix and reports the results to OpCon."
tags:
  - Procedural
  - Operations Staff
  - Agents
---

# *SMA/WFL/CHECK/MIX

## What is it?

\*SMA/WFL/CHECK/MIX provides a batch interface for checking whether any processes are present in the MCP Waiting mix or Scheduled mix, eliminating the need for an operator to log on to the MCP system to perform the interrogation. When processes are found, the WFL creates a print file listing them and aborts, causing the OpCon job to be reported as Failed.

- Detect stalled or waiting MCP processes as part of a scheduled OpCon workflow
- Trigger downstream remediation jobs when entries are found in the Waiting or Scheduled mix


## Usage

To use this utility, complete the following steps:

* **Job Command**: START
* **Usercode**: Desired usercode under which to run the utility
* **File Title**: \*SMA/WFL/CHECK/MIX ON ```<diskpack>```
* **Arguments**: Enter "WAITING" if you want to determine if there are processes in the waiting mix. Enter "SCHEDULED" if you want to determine if there are any processes in the Scheduled entries.

If there are no processes found, the WFL completes OK. If there are processes found, a print file listing these processes is created and the WFL is aborted, resulting in the OpCon job being reported as Failed. You may view the report using "View Job Output".
 
Here is a sample report indicating there is one entry in the Waiting mix:

```

000001 2014/02/18 09:41:49
000002 MIX ENTRIES FOUND IN WAITING LIST
000003 Job:4814 Mix:4814 Time Waiting:10.7998464 Name:WFL/WAIT
000004 DISPLAY:PLEASE ENTER RESPONSE.
000005 PROGRAMMATICALLY SUSPENDED
000006 Responses: OK, DS

```

At this point, you can log onto the MCP platform to address the condition, create an OpCon job that starts \*SMA/WFL/COMMAND to respond to the condition, or start some other OpCon job to address the condition.

