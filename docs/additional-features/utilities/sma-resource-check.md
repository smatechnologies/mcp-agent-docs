# *SMA/RESOURCE/CHECK

The WFL \*SMA/WFL/RESOURCE/CHECK/xxx checks for the existence/absence of a given process in the list of executing processes on the platform or checks on the presence/absence of a file. The program \*SMA/RESOURCE/CHECK sets the TASKVALUE to 1 if the requested criteria have been met; otherwise, the program sets the TASKVALUE to 0.
 
\*SMA/WFL/PROCESSCHECK and \*SMA/WFL/FILECHECK use this program; however, a user-written WFL may call \*SMA/RESOURCE/CHECK.

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