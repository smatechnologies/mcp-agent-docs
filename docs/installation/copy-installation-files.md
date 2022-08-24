# Copy Installation Files to MCP

Before you install the *SMA/INSTALL program, you must FTP the LSAM container files from the OpCon installation media on a Windows machine to the MCP machine. Follow the procedures here to perform the FTP.

1. Use menu path: ```Start > Run```.

2. Enter ```CMD``` in the Open text box.

3. Click the OK button. The Command window displays.

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