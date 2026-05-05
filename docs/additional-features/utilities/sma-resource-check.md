---
title: "*SMA/RESOURCE/CHECK"
description: "A utility program that checks for the existence or absence of a file or executing process on the MCP platform and reports the result via TASKVALUE."
tags:
  - Reference
  - Automation Engineer
  - Agents
---

# *SMA/RESOURCE/CHECK

## What is it?

\*SMA/RESOURCE/CHECK is a program called by \*SMA/WFL/PROCESSCHECK and \*SMA/WFL/FILECHECK that searches for a file or a running process on the MCP platform and sets the TASKVALUE to 1 when the requested criteria are met, or to 0 when they are not. User-written WFLs may also call this program directly using the syntax described below.

- Check whether a specific file exists on the MCP platform before allowing a dependent job to proceed
- Check whether a specific process is currently running in the active mix before allowing a dependent job to proceed


## Syntax

In a user-written WFL, use the syntax specified in these next two subsections.

### File Title

\*```<user>```/WFL/RESOURCE/CHECK/xxx

### Arguments

* ```<Search Type>```,"```<Search String>```"

* ```<Search Type>``` determines if the utility searches for a file or for a process.
    * The integer value 1 indicates the utility is searching for a file.
    * The integer value 2 indicates the utility is searching for a process.

* ```<Search String>``` is the name of the process/file sought for in the search process.
    * Wildcarding is accomplished using the rules defined for the ASERIES_INFO MCP procedure.

:::tip Example

The following example shows a wildcard search string:

```

=CANDE=

```

:::