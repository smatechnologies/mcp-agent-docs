---
title: "*SMA/WFL/FILECHECK"
description: "A utility WFL that makes an OpCon job dependent on the presence or absence of a file on the MCP platform."
tags:
  - Procedural
  - Automation Engineer
  - Agents
---

# *SMA/WFL/FILECHECK

## What is it?

\*SMA/WFL/FILECHECK/xxx allows a job to proceed only when a specified file is either present or absent on the MCP platform, supporting both exact file names and wildcard patterns. The utility accepts the file name, a criterion value (REQUIRES or EXCLUDES), and an optional family name as parameters.

- Gate a dependent job so it runs only when a required input file is present on the MCP platform
- Gate a dependent job so it runs only when a lock or indicator file has been removed from the MCP platform


## Syntax
On the MCP Job Details screen, use the syntax specified in these next two subsections

### File Title

\*SMA/WFL/FILECHECK/xxx

### Arguments

"```<File Name>```","```<Criterion Value>```",```<"Family">```

* ```<File Name>``` is the name of the file to be interrogated.
    * Wildcarding is accomplished using the rules defined for the ASERIES_INFO MCP procedure.

:::tip Example 

The following example shows a wildcard search string:

```

=CANDE=

```

:::

* In the case of non-standard MCP file names, such as a file name that contains an embedded period, do NOT use quotation marks - the utility will construct the filename before performing the inquiry as to the file's presence.

* ```<Criterion Value>``` is the criterion used to determine if the prerun was successful.
    * The value "REQUIRES" indicates the dependent job may proceed if the file is present.
    * The value "EXCLUDES" indicates the dependent job may proceed if the file is not present.

* ```<"Family">``` is the family name on which to search for the target file(s). This parameter is optional. If unnecessary, omit the parameter or insert a pair of double quotes to indicate a null value.

:::tip Example

The following commands search under all usercodes for a file containing the string "JUNK" and residing on the family PROD. The commands' executions depend on the privileges associated with the usercode under which the WFLs are started.

```

START *SMA/WFL/FILECHECK("=JUNK/=","REQUIRES","PROD")

```

\- or -

```

START *SMA/WFL/FILECHECK/WS("=JUNK/=","REQUIRES","")

```

:::