# *SMA/WFL/PROCESSCHECK

The WFL \*SMA/WFL/PROCESSCHECK/xxx allows a job to be dependent on the existence/absence of a given process in the list of executing processes on the platform.

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