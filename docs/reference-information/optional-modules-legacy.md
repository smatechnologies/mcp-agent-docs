# Optional Modules (Legacy)

## General Settings

| Field | Default | Valid Values | Description |
| ----- | ------- | ------------ | ----------- |
| Autoresponse | N | Y <br></br> N | This field indicates whether the Auto-Response feature is active.
| File Transfer | N | - N <br></br> - B <br></br> - O <br></br> - I | This filed indicates the permitted directions for SMA File Transfer. <br></br><br></br> - If N, file transfer is not in use (default). <br></br> - If B, bi-directional transfer is okay. <br></br> - If O, only outgoing transfers are permitted. <br></br> - If I, only incoming transfers are permitted. |
| JORS | N | Y <br></br> N | This field determines whether or not the LSAM will initiate the *SMA/JORS/xxx program. <br></br><br></br> - If N, the LSAM will not initiate the *SMA/JORS/xxx program. <br></br> - If Y, the LSAM will initiate the *SMA/JORS/xxx program. |
| Mixwatcher | N | Y <br></br> N | This field determines whether or not the LSAM tracks external jobs. <br></br><br></br> - If Y, the LSAM tracks external jobs. <br></br> ---- **Note**: Once detected, tracked jobs are displayed in the OpCon Enterprise Manager. <br></br> - If N, the LSAM does not track external jobs. |
| File Monitor in use | N | Y <br></br> N | This field indicates whether File Monitor should be started by the Resource Monitor. |
| Resource Monitor Freq | 01800 (30 minutes) | 30 - 86400 | This field sets the approximate number of seconds the Resource Monitor should wait between performance metrics samples: <br></br><br></br> - 3600 = one hour <br></br> - 86400 = 24 hours |
| SAM auth | ```<None>``` | | This field allows you to enter the following credentials: <br></br><br></br> - A User Login ID defined in OpCon with the appropriate privileges to perform the commands to be submitted by the external events. <br></br> - The Events Password defined in OpCon for the User Login ID. |

## File Transfer

| Field | Default | Valid Values | Description |
| ----- | ------- | ------------ | ----------- |
| Add LF to Unix | Y | Y <br></br> N | This field determines how the file contents are stored and displayed on the UNIX system. <br></br><br></br> - If set to a value of Y, the SMA File Transfer process will append a line feed (carriage control) to the end of each MCP record prior to sending the record to a UNIX platform. <br></br> - The result on the UNIX platform is a text file that contains the UNIX newline character, which causes the MCP data to appear as records rather than a continuous stream of text. <br></br><br></br> **Note**: This option only applies to SMA File Transfers using the ASCII, EBCDIC, or Default Text options - it does not apply to Binary transfers. |
| Backup suffix | ```<None>``` | - All letters and numbers are permitted. <br></br> - Special characters, such as slashes (/), are not permitted. | This field specifies the suffix that should be appended to the name of the existing file prior to initiating a file transfer if backup is requested prior to the transfer. |
| TLS Allow Self-sign? | N | Y <br></br> N | **Note**: All TLS fields relative to SMA File Transfer are reserved for future use. This field allows the use of self-signed certificates in the SMA File Transfer TLS protocols. |
| Key | SMALSAM	| | This field specifies the presence of a key name implies that TLS will be used for communications. <br></br><br></br> - Using MCP Cryptographic Services, create a Key, associate it with the usercode you will run the MCP LSAM under, and generate a certificate request. Once a signed certificate has been received, install it for this key. The same key may be used for multiple instances and features of the MCP LSAM. <br></br> - This configuration variable must correspond to a key defined in the Trusted Keys store of MCP Cryptographic Services. A valid certificate is also required. |
| Agent Port | 00000 | 1024 – 65535 | This field specifies the port number used by *SMA/FTAGENT to communicate with the File Transfer server. <br></br><br></br> This port number does NOT have a corresponding entry in the Enterprise Manager. |
| Agent TLS | N	| - B <br></br> - N <br></br> T | **Note**: Reserved for future use. <br></br><br></br> Use this field to specify whether TLS is available to be used to secure communications between the MCP FTAgent and corresponding FTSERVER. <br></br><br></br> - If B, the MCP FTAgent will support both TLS and non-TLS secured communications. <br></br> - If N, the MCP FTAgent will support only non-secured connections. <br></br> - If T, the MCP FTAgent will support only communications secured by TLS. |
| Server Port | 00000 | 1024 - 65535 | This field specifies the port number used by *SMA/FTSERVER to communicate with the File Transfer agent WITHOUT using TLS. <br></br><br></br> - The FTSERVER port number must also be configured on the Administration > Machines > Advanced Settings > File Transfer Settings > File Transfer Port Number in the Enterprise Manager. |
| Server TLS Port | 00000 | 1024 - 65535 | **Note**: Reserved for future use. <br></br><br></br> This field specifies the port number used by *SMA/FTSERVER to communicate with the File Transfer agent WHEN using TLS. <br></br><br></br> - The FTSERVER port number must also be configured on the Administration > Machines > Advanced Settings > File Transfer Settings > File Transfer Port Number in the Enterprise Manager. |
| Num Servers | 0 | 0 - 9 | This field specifies the maximum permitted number of concurrent outgoing file transfers. <br></br><br></br> - If the File Transfer variable is set to a value other than "N," the Num Servers variable must be at least 1. |

## JORS

| Field | Default | Valid Values | Description | 
| ----- | ------- | ------------ | ----------- |
| Port | 3110 | 0 – 65535 | This field specifies the port number used for communicating job output information with the Enterprise Manager. <br></br><br></br> - The JORS port number must also be configured on the Administration > Machines > Advanced Settings > Communication Settings > JORS Port Number in the Enterprise Manager. |
| Sec? | N | N | This field specifies whether communications with the SAM-SS are to be secured using TLS. |
| Self-sign? | N | Y <br></br> N | This field allows the use of self-signed certificates in the JORS communications protocol. <br></br> **Note**: At this time, the same variables are used to configure TLS for both Netcom and for JORS. The SMA/CONFIG program automatically populates the JORS fields based on the Scheduling/Netcom field values. |
| Key | SMALSAM	| | This field specifies the presence of a key name implies that TLS will be used for communications. <br></br><br></br> - Using MCP Cryptographic Services, create a Key, associate with the usercode you will run the MCP LSAM under, and generate a certificate request. Once a signed certificate has been received, install it for this key. The same key may be used for multiple instances and features of the MCP LSAM. <br></br> This configuration variable must correspond to a key defined in the Trusted Keys store of MCP Cryptographic Services. A valid certificate is also required. | 
| Prefix | BD | Any | This field defines the initial node(s) of the print file names. <br></br><br></br> The LSAM uses this value and the mix number (and, optionally, the usercode of the job) to locate the print files by preceding the job's mix number with this prefix (e.g., *BD/00jjjjj). <br></br> Although multiple nodes may be used to define the print file prefix, multiple print file prefixes are not supported.
| Family | ```<None>``` | Any | This field specifies the diskpack on which print files are located. |

## MSGIN

| Field | Default | Valid Values | Description |
| ----- | ------- | ------------ | ----------- |
| Freq | 0000 | 0 – 9999 | This field sets the number of seconds between MSGIN file checks. <br></br><br></br> - Setting the MSGIN/= File check frequency to a low value increases overhead, but increases the frequency of file checking. <br></br> - Setting the MSGIN/= File check frequency to a high value minimizes overhead, but decreases the frequency of file checking. |
| Family | ```<None>``` | | This field specifies the family on which MSGIN/= files resides. <br></br><br></br> - If multiple LSAMs are in use, configure each LSAM to look for MSGIN/= files on unique families.

## IMPQ

| Field | Default | Valid Values | Description |
| ----- | ------- | ------------ | ----------- |
| (I)nquire, (M)odify, (P)rint, (Q)uit | I | - I <br></br> - M <br></br> - P <br></br> - Q | These are the Configuration screen commands. <br></br><br></br> - I: Allows you to inquire about the current data in the configuration file. Enter this option to discard any changes made. <br></br> - M: Allows you to modify the configuration file with all changes entered. <br></br> - P: Allows you to print a report of the configuration file. The print request name is \*SMA/CONFIG/xxx. <br></br> - Q: Allows you to quit the configuration program. |



