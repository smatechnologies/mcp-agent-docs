# SMA File Transfer Messages

The following error and informational messages may be encountered in the \*SMA/FTAGENT.

| Message | Possible Cause/Recommended Action |
| ------- | --------------------------------- | 
| \** Bad CRC *** | Internal error – contact SMA Technologies. |
| \** Can't write to FTSERVER ** | Check the status of the FTServer on both machines. |
| Agent cannot delete source file | Verify privileges. |
| Bad CRC from Agent | Internal error – contact SMA Technologies. |
| Can't agree on a CommonCharSet | Internal error – contact SMA Technologies. |
| Can't create destination file | Verify privileges. |
| Can't read msg from Handler | Check the status of the SMA/FTHANDLER#. |
| Can't write to Agent | Check the status of the FTAgent on both machines. |
| Can't write to Handler | Check the status of the SMA/FTHANDLER#. | 
| Can't write to Server | Check the status of the FTServer on both machines. |
| Can't write to transfer file | Verify privileges. | 
| Compression is not supported | Remove Compression requirement from OpCon job. |
| Configuration file is missing | Check configuration. |
| Data type mismatch for appended file | Existing file EXTMODE does not match transfer type on an "Append" transfer. |
| Dest file exists; No overwrite | "Do Not Overwrite" has been specified on the transfer job. |
| Encryption is not supported | Remove Encryption requirement from OpCon job. |
| File exists and overwrite not permitted | "Do Not Overwrite" has been specified on the transfer job. |
| File is not available | Verify privileges. |
| FTAgent configured for non-TLS only; job requires TLS | The machine properties as defined within the OpCon database indicate that the MCP FTAGENT will support transfers using a connection secured by TLS, but the LSAM configuration setting for SMAFT security (the Sec? field) indicates that all transfers require that the connection NOT be secured with TLS. |
| FTAgent configured for TLS only; job requires non-TLS	| The machine properties as defined within the OpCon database indicate that the MCP FTAGENT will support transfers using an unsecure connection, but the LSAM configuration setting for SMAFT security (the Sec? field) indicates that all transfers require that the connection be secured with TLS. |
| FTAgent is unresponsive | Check the status of the FTAgent on both machines. |
| FTServer is unresponsive | Check the status of the FTServer on both machines. |
| FTServer OPEN error | Check the status of the FTServer on both machines. | 
| FTServer OPEN warning | Check the status of the FTServer on both machines. |
| Inv fileclass for src datatype | Usually caused by attempting to transfer a stream file using a text transfer mode.|
| Invalid ```<CommonCharSet>``` | Internal error – contact SMA Technologies. |
| Invalid destination file data type | The existing file's EXTMODE is not compatible with the job's destination file data type (usually ASCII vs EBCDIC). |
| Invalid destination file title | The destination file title does not conform to MCP file naming syntax (check for quotes if the file name contains a period). |
| Invalid FILECLASS for Source file | The source file's FILECLASS is not compatible with the job's source file data type (usually text vs binary). |
| Invalid source file data type | The source file's EXTMODE is not compatible with the job's source file data type (usually ASCII vs EBCDIC). |
| Invalid source file title | The source file title does not conform to MCP file naming syntax (check for quotes if the file name contains a period). |
| Invalid value for FTAGENT port | Check configuration. |
| Invalid value for SMAFT_IN_USE flag | Check configuration. |
| IP Addr Err: Insufficient space | Internal error – contact SMA Technologies. |
| IP Addr Err: Invalid Version | Internal error – contact SMA Technologies. |
| IP Addr Err: Invalid Address Version | Internal error – contact SMA Technologies. |
| IP Addr Err: Invalid Data | Internal error – contact SMA Technologies. |
| IP Addr Err: Missing right bracket | Internal error – contact SMA Technologies. |
| IP Addr Err: Internal library fault | Internal error – contact SMA Technologies. |
| IP Addr Err: Unspecified error | Internal error – contact SMA Technologies. |
| Msg size nnnnnn exceeds allowed len, where nnnnnn is the reported message size | This is a protocol error. Please enable debugging on both SMA File Transfer components, attempt to rerun the File Transfer job, and contact SMA Technologies. |
| No open sockets | Communication issue – check the status of the FTAgent and FTServer for both platforms. |
| No rec seps in max rec len (65535) | Specify a record length on the MCP file to circumvent this issue. |
| No rec seps in data - use ',REC=' | Specify a record length on the MCP file to circumvent this issue. |
| No record seps in data - use ',REC=' | Specify a record length on the MCP file to circumvent this issue. |
| Outgoing transfer not allowed | Check configuration. |
| Packet number error | Internal error – contact SMA Technologies. |
| Preferred settings not accommodated | This is a warning. It indicates that Compression/Encryption were preferred, but could not be accommodated. |
| Printerbackup file – use binary | The source file is a printerbackup file and a text mode (ASCII/EBCDIC/Default Text) was specified. Change the mode to Binary. |
| 'Push' transfer not allowed | "Run on Destination machine" was specified but either the FTAgent or FTServer cannot accommodate this request. |
| Received an invalid request |  Internal error – contact SMA Technologies. |
| Requested file not found | The source file could not be located. |
| Server cannot delete src file | The FTServer attempted to delete the source file following the transfer, but was unable to do so. Check privileges. |
| Server does not support 'delete' | The job specifies that the source file is to be deleted following the transfer, but the FTAgent or FTServer does not support this functionality. |
| Server does not support 'push' | "Run on Destination machine" was specified but the FTServer cannot accommodate this request. | 
| SMA File Transfer not allowed | Check configuration. |
| SMAFT is not enabled for this LSAM | Check configuration. |
| SMAFT is permitted for outbound xfr only | Check configuration. |
| Unable to read source file | The source file could not be read. Check privileges. |
| Unable to send status msg | The FTAgent is unable to insert a job status message into the SMA/OUTBOUND/FILE. Look for *SMA/ALGOLPROCS in the waiting mix, probably waiting on sectors. | 
| Unable to write to transfer file | The temporary, interim transfer file could not be written to. Check privileges and disk space. |
| Undefined msg type: | Internal error – contact SMA Technologies. |
| Unrecognized Action value | Internal error – contact SMA Technologies. |
| Unsupported file type: | Internal error – contact SMA Technologies. |
| Variable length records not specified. | Internal error – contact SMA Technologies. |