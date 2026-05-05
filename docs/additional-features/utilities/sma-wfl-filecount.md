---
title: "*SMA/WFL/FILECOUNT"
description: "A utility WFL that makes an OpCon job dependent on a minimum number of matching files being present or absent on the MCP platform."
tags:
  - Procedural
  - Automation Engineer
  - Agents
---

# *SMA/WFL/FILECOUNT

## What is it?

\*SMA/WFL/FILECOUNT/xxx allows a job to proceed only when at least a specified minimum number of files matching a given name pattern are present (or fewer than that number are present) on the MCP platform. The utility accepts the file name pattern, a criterion value (REQUIRES or EXCLUDES), a family name, and the minimum file count as parameters.

- Gate a downstream job so it runs only after a minimum number of input files have arrived on the MCP platform
- Hold a job until fewer than a specified number of files matching a pattern are present


## Syntax

On the MCP Job Details screen, use the syntax specified in these next two subsections.

### File Title

\*SMA/WFL/FILECOUNT/xxx

### Arguments

"```<File Name>```","```<Criterion Value>```",```<"Family">```,```<Number of Files>```

* ```<File Name>``` is the name of the file to be interrogated.
    * Wildcarding is accomplished using the rules defined for the ASERIES_INFO MCP procedure.

:::tip Example

The following example shows a wildcard search string:

```

(OPS)FROM/CLIENTS/=

```

:::

* In the case of non-standard MCP file names, such as a file name that contains an embedded period, do NOT use quotation marks - the utility will construct the filename before performing the inquiry as to the file's presence.

* ```<Criterion Value>``` is the criterion used to determine if the prerun was successful.
    * The value "REQUIRES" indicates the dependent job may proceed if at least the Number of Files is present.
    * The value "EXCLUDES" indicates the dependent job may proceed if the actual number of files is less than the "Number of Files" specified in the parameter.
* ```<"Family">``` is the family name on which to search for the target files. This parameter is not optional.
* ```<Number of Files>``` is the minimum number of files matching the search criteria that must be found in order to determine success or failure of the job. A number greater than 0 must be supplied.