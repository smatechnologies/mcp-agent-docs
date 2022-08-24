# *SMA/WFL/FILECOUNT

The WFL *SMA/WFL/FILECOUNT/xxx allows a job to be dependent on the presence/absence of a specified minimum number of files.

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