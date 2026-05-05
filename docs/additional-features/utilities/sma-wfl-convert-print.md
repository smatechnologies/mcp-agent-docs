---
title: "*SMA/WFL/CONVERT/PRINT (MCP Print File Conversion)"
description: "A utility that converts an MCP printer backup print file to an ASCII text file to enable distribution via SMA File Transfer."
tags:
  - Procedural
  - Automation Engineer
  - Agents
---

# *SMA/WFL/CONVERT/PRINT (MCP Print File Conversion)

## What is it?

\*SMA/WFL/CONVERT/PRINT converts an MCP print file (kind=BACKUPPRINTER) to an ASCII text file, making it suitable for distribution to users on Windows, UNIX, or other ASCII-based platforms via an SMA File Transfer job. The utility consists of two modules — \*SMA/WFL/CONVERT/PRINT and \*SMA/OBJ/CONVERT/PRINT — and accepts the source print file title and the destination ASCII file title as parameters.

- Convert an MCP printer backup file to ASCII text as a preliminary step before an SMA File Transfer job
- Distribute MCP print output to users on non-MCP platforms as part of a scheduled OpCon workflow


## Syntax

On the MCP Job Details screen, use the syntax specified in these next two subsections.

### File Title
\*SMA/WFL/CONVERT/PRINT/xxx

### Arguments

"```<MCP print file>```","```<ascii text file>```"
* ```<MCP print file>``` is the title of the MCP print file to be converted.
* ```<ASCII text file>``` is the title of the ASCII test file created as output.