# File Transfer Troubleshooting

## Job Fails with P-DS

#### Full Description

The job appears as Failed with a status description of P-DS.
 
#### First Possible Explanation:
 
If encryption and/or compression are "Preferred", the transfer will take place yet the job will appear as Failed with a status description of P-DS.

##### First Operator Response:

Check the Job Configuration table to determine the true success or failure of any file transfer job that has a status description of "P-DS".

#### Second Possible Explanation:
 
If there has not been sufficient time for the TCP/IP protocol to mark the FTSERVER socket available for reuse, the job will appear as Failed with a status description of P-DS.

##### Second Operator Response:

Check the Job Configuration table to determine the true success or failure of any file transfer job that has a status description of "P-DS". If the error "FTServer OPEN error:246 for IP:…" is observed, restart the job. If this error persists, it may be that the *SMA/FTSERVER/xxx has left the mix. Investigation into the reason for the disappearance of FTSERVER is warranted.
 
## Warning 86

#### Full Description

The following message appears on the MCP console:
 
Warning 86: STREAM FILESTRUCTURE should be ruled out before interrogating any block-related attributes. @ (00100000)
 
#### Possible Explanation:
 
This warning message is caused when the SMAFT server (SMA/FTHANDLERn) interrogated the blocksize of the source file in preparation for transfer.

##### Operator Response:

No response is required.