---
title: "*SMA/WFL/PROCESSCHECK"
description: "A utility WFL that makes an OpCon job dependent on the existence or absence of a specified process in the MCP active mix."
tags:
  - Procedural
  - Automation Engineer
  - Agents
---

# *SMA/WFL/PROCESSCHECK

## What is it?

\*SMA/WFL/PROCESSCHECK/xxx allows a job to proceed only when a specified process is either running or not running in the MCP active mix, supporting both exact process names and wildcard patterns. The utility accepts the process name and a criterion value (REQUIRES or EXCLUDES) as parameters.

- Gate a dependent job so it runs only while a required companion process is active in the MCP mix
- Gate a dependent job so it runs only after a blocking process has finished and left the active mix


## Syntax

On the MCP Job Details screen, use the syntax specified in these next two subsections.

### File Title

\*SMA/WFL/PROCESSCHECK/xxx

### Arguments

"```<Process Name>```","```<Criterion Value>```"
```<Process Name>``` is the name of the process to be interrogated.
Wildcarding is accomplished using the rules defined for the ASERIES_INFO MCP procedure.

:::tip Example 

The following example shows a wildcard search string:

```

=CANDE=

```

:::

* ```<Criterion Value>``` is the criterion used to determine if the prerun was successful.
    * The value "REQUIRES" indicates the dependent job may proceed if the process is currently executing.
    * The value "EXCLUDES" indicates the dependent job may proceed if the process is not executing.