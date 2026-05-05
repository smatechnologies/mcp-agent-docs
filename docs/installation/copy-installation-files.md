---
title: Copy Installation Files to MCP
description: "Transfer the MCP LSAM container files from a Windows machine to the ClearPath MCP system via FTP before running the installer."
tags:
  - Procedural
  - System Administrator
  - Installation
  - Agents
---

# Copy Installation Files to MCP

## What is it?

This page provides step-by-step FTP procedures for transferring the MCP Agent installation container files from a Windows machine to the ClearPath MCP system and then unwrapping the installer program. It covers the binary transfer requirements and the UNWRAP command syntax needed to prepare the files for the installation run.

- Use this page when performing a new or upgrade installation to move the agent and installer container files onto the target MCP family before running `*SMA/INSTALL`.
- Use this page to verify a successful file transfer by reviewing the byte values returned in the FTP command window.

Before you install the `*SMA/INSTALL` program, you must FTP the agent container files from the OpCon installation media on a Windows machine to the MCP machine. To perform the FTP, complete the following steps:

1. Use menu path: ```Start > Run```.

2. Enter ```CMD``` in the Open text box.

3. Select the **OK** button. The Command window displays.

4. Enter the FTP command and the TCP/IP address of the ClearPath MCP: ```FTP<TCP/IP address>```.

5. Sign on to the ClearPath MCP with a system privileged usercode:
* *User (127.0.0.1: (none))*:```<Usercode>```
* *Password*:```<Password>```

6. Set the transfer type to binary: BIN.

7. Enter the command to put the wrap file onto the MCP:
* ```PUT <path>\LSAM_nnnnnn_LEV6 LSAM_nnnnnn_LEV6```; where ```nnnnnn``` is the 6-digit MCP LSAM version and LEV6 is the COMPILERTARGET of the MCP machine.

8. Enter the command to put the wrap file onto the ClearPath MCP:
* ```PUT <path>\INST_nnnnnn_LEV6 INST_nnnnnn_LEV6```; where ```nnnnnn``` is the 6-digit MCP LSAM version and LEV6 is the COMPILERTARGET of the MCP machine.

9. Exit the FTP program: BYE.

10. Review the output in the command window. Examine the byte value to verify that the Lsam_nnnnnn_LEV6 and Inst_nnnnnn_LEV6 files were transferred successfully.

11. Repeat the FTP procedure, if no byte value is indicated.

12. Unwrap the file ```*SMA/INSTALL/nnnnnn```. 
* From CANDE, type:

```

UNWRAP *NEW/SMA/INSTALL/nnnnnn/LEVEL6 AS *SMA/INSTALL/nnnnnn/LEVEL6 OUTOF INST_nnnnnn_LEV6 FROM <FAMILYNAME>(PACK) TO <FAMILYNAME> (PACK, RESTRICTED=FALSE). Transmit.

```

:::info Note 

```nnnnnn``` = the 6-digit MCP LSAM version number.

:::