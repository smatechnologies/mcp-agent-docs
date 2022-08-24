# Pre-Installation Worksheet

The Pre-installation Worksheet has fields of required information for a successful MCP LSAM installation as well as fields for optional features which aid in implementing all of the LSAM features.

## Required Information

| Question | Installation or Configuration Requirement | Answer |
| -------- | ----------------------------------------- | ------ |
| What is the MCP Queue to be used to submit the LSAM initiation WFL? | Configuration |
| What is the MCP usercode to be used to submit the LSAM initiation WFL? | Configuration | 	 
| What is the primary family of the usercode used to submit the LSAM initiation WFL? | Configuration | 	 
| What is the alternate family of the usercode used to submit the LSAM Initiation WFL? | Configuration |  
| Should the Resource Monitor be included in the WFL that is used to initiate the LSAM? | Configuration | 	 
| What is the MCP Queue to be used to submit the Resource Monitor initiation WFL? | Configuration | 	 
| What is the MCP usercode to be used to submit the Resource Monitor initiation WFL? | Configuration |	 
| What is the primary family of the usercode used to submit the Resource Monitor initiation WFL? | Configuration | 
| What is the alternate family of the usercode used to submit the Resource Monitor Initiation WFL? | Configuration | 
| Is the size of the terminal screen at least 1,920 bytes (i.e., 24 lines by 80 characters)? <br></br><br></br> Caution: If the screen is not 1,920 bytes or larger, the configuration program fails. | Configuration |
| On which family is the LSAM going to be installed? | Installation |
| What is the name of the system-privileged usercode under which the files should be uploaded to the ClearPath MCP? | Installation |
| What is the password and default family (or pack) associated with the ClearPath MCP usercode listed above? | Installation |
| What is ClearPath MCP TCP/IP port to be used to communicate with SMANetCom? | Configuration |
| What is the name of the DATACOMINFO file used by IDC? | Installation |
| What is the maximum number of concurrent jobs that should be monitored by the MCP LSAM? | Configuration |
| Which method of failure determination is used most often in this environment? <br></br><br></br> 1. WFLs fail if a subordinate task fails. <br></br><br></br> 2. WFLs may complete successfully when a subordinate task fails. | Configuration |

| | | LSAMs | LSAM Identifier  | 
| ---- | ---- | ---- | --- |
| If installing one or more additional concurrent LSAMs, what is the unique LSAM identifier for each additional LSAM? | Installation, Configuration | 1 <br></br> 2	<br></br> 3 <br></br> 4 | |

## Optional Features

| Checklist |
| --- | 
| File Monitor |
| Job Output Retrieval | 
| User-defined Checkpoints | 
| Automated Response |
| Task Level Checking |
| File Transfer |
| External Event Interface Library |
| Tracking External Jobs |
| Resource Monitor |
| Secure Communications Using TLS |

| Feature | Question | Answer |
| ------- | -------- | ------ |
| Job Output Retrieval | What is the port number to be used for the JORS server? |
| File Transfer | What is the port number to be used for the SMAFT server? |
| File Transfer | What is the port number to be used for the SMAFT agent? |
| File Transfer | Maximum number of expected concurrent outgoing SMA File Transfers (1-9).	|
| User-defined Restart/Recovery Checkpoints | What is more important? Data recovery or processing performance? |
| Secure Communications	| What is the port number to be used by the FTServer to communicate using TLS? <br></br><br></br> Will both secure and unsecured communications be permitted for the FTAgent? <br></br><br></br> Is the security certificate self-signed? What is the key associated with this certificate? |

 

