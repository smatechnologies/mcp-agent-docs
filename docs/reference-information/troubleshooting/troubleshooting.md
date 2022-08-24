# Troubleshooting

## Troubleshooting Categories

These troubleshooting tables, organized by problem category, present symptoms and the location of their possible explanation and solution.

### AutoResponse Troubleshooting Categories

| AutoResponse Symptom | Explanation |
| -------------------- | ----------- | 
| AutoResponse is configured, but does not appear to be responding to displays.	| Display Monitor Rules not Applied |
| External Events do not appear to have been sent to the SAM. | External Events not Sent to SAM |
| Displays file changes were not applied. | Changes to Display Monitor Rules not Applied | 
| ATTRIBUTE ERROR:JOB-DISPLAYS TITLE MISSING "." @41800 is displayed by \*SMA/DISPLAY/HANDLER/xxx. | Title Missing "." @41800 |
| Jobs stay in a waiting state too long. | Jobs Stuck in "Waiting" State | 
| A very high number of messages are awaiting processing (as evidenced by Manager MSGCOUNT inquiry) and defined actions are not taking place. | High Message Count |

### Communication Troubleshooting Category


| Communicating Symptom | Explanation |
| --------------------- | ----------- |
| Although a task and its subtasks are completed, the job's status in the Enterprise Manager's Operations remains "Job Running." | Jobs Stuck in "Running" State |
| The LSAM is not communicating with SMANetCom, and/or jobs fail to start (i.e., the Enterprise Manager displays "Wait Machine"), and/or job status information is not up-to-date in the Enterprise Manager. | LSAM not Communicating |
| The message, "Arithmetic overflow error for data type smallint, value = 32768," is observed in the OpCon log. | Arithmetic Overflow Error |

### Configuration Troubleshooting Categories

| Configuration Symptom | Explanation |
| --------------------- | ----------- |
| "Insufficient screen size" error occurs when starting the \*SMA/CONFIG/xxx program. | Insufficient Screen Size |
| Configuration changes were not applied. | Configuration Changes not Applied |
| Config file is too short - Use SMA/MANAGER to update config file.	Config File is Too Short |

### File Monitoring Troubleshooting Categories

| File Monitoring Symptom | Explanation |
| ----------------------- | ----------- |
| Event is not sent to the Schedule Activity Monitor (SAM). | Event not Sent |
| Changes to *SMA/FILEMON/DEFS/xxx were not applied. | Changes to File Monitor Rules not Applied |
| Some files are not being monitored as defined. | Files not Monitored |

### File Transfer Troubleshooting Category

| File Transfer Symptom | Explanation |
| --------------------- | ----------- |
| The job appears as Failed with a status description of P-DS. | Job Fails with P-DS |
| The following message appears on the MCP console: Warning 86: ```STREAM FILESTRUCTURE should be ruled out before interrogating any block-related attributes. @ (00100000)``` | Warning 86 |

### Job Initiation/Monitoring Troubleshooting Categories

| Job Initiation/Monitoring Symptom | Explanation | 
| --------------------------------- | ----------- | 
| Job stays in "QUEUED" state. | Job Stuck in "QUEUED" State |
| Job stays in a "Start Attempted" state. | Job Stuck in "Start Attempted" State |
| Job stays in "Wait Machine" state. | Job Stuck in "Wait Machine" State | 
| Receiving a 0SNTX/SECRTY ERR status. | Job Status "0SNTX/SECRTY" Error |
| Receiving a NOT JOB FILE error. | Job Status "NOT JOB FILE" Error | 
| Receiving a PARAM/ATTR ERR status. | Job Status "PARAM/ATTR" Error | 
| \*SMA/WFL/PROCESSCHECK/xxx does not find WFL jobs that are active. | PROCESSCHECK not Working | 

### Job Output Retrieval System (JORS) Troubleshooting Category

| JORS Symptom | Explanation |
| ------------ | ----------- |
| "No output file" is the response to "View Print File." | No Output File |
| JORS is not running. | JORS not Working |

### LSAM Initialization/Stopping Troubleshooting Categories

| LSAM Initialization/Stopping Symptom | Explanation |
| ------------------------------------ | ----------- | 
| The LSAM reports the configuration file is absent. | Configuration File Missing |
| The \*SMA/TCPIP/xxx module reports "seg array error @00081445." | SEG ARRAY ERR @ 00081445 |
| \*SMA/COMM/xxx goes I-DS @ 66100.	| I-DS @ 66100 | 
| The LSAM takes too long to come down.	| LSAM Slow to Come Down |
| \*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 2435000.	| SEG ARRAY ERR @ 2435000 |
| \*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 178600.	| SEG ARRAY ERR @178600 | 
| \*SMA/COMM/xxx gets ASSERTION FAILURE ON RANGE TEST @ (Expression out of range 91700). | ASSERTION FAILURE @91700 |
| LSAM modules are in the waiting mix awaiting the SMALIBRARYxxx>.	| LSAM Waiting for SMALIBRARY |
| \*SMA/MCP/INTERFACE/xxx gets INVALID INDEX @ (04637000). | INVALID INDEX @ 02412000 or 04637000 |
| The \*SMA/MCP/INTERFACE module displays the following messages when an LSAM begins a job, and when a user WFL is submitted via OpCon:<br></br> ```12131 14:56 This 47.1 codefile will not run on software released on or after January 1, 2006. Refer to the Release and Support Policy Overview. 12131 14:56 Warning 137: This codefile must be recompiled in order to run on future releases. @ (00146000)``` | Codefile will not Run... |
| \*SMA/ALGOLPROCS/xxx fails with SEQ ARRAY ERR around 924100. | SEG ARRAY ERR around 924100 |
| The LSAM begins to come up, but soon goes down again. | LSAM Stops Soon after Starting |
| Upon LSAM initiation or job initiation, the \*SMA/MCP/INTERFACE goes into the waiting mix, unable to locate SMALIBRARY or \*SMA/ALGOLPROCS. | SMA/MCP/INTERFACE Goes Waiting |
| \*SMA/MCP/INTERFACE gets Invalid index @ 02430350. | INVALID INDEX @ 02430350 | 
| \*SMA/MCP/INTERFACE/xxx gets Invalid Operator @ 02693716. | INVALID OPERATOR @ 02693716 | 