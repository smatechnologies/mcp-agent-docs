---
title: Problem Resolution and Debugging
description: "Gather and submit MCP LSAM debug information to SMA Technologies support for timely issue resolution."
tags:
  - Procedural
  - System Administrator
  - System Configuration
  - Agents
---

# Problem Resolution and Debugging

## What is it?

This page covers the resources and procedures for diagnosing issues with the MCP Agent, enabling and collecting debug output, and submitting that output to SMA Technologies support. It describes the SMASUP utility and the three output files it produces.

- Use this page when a job or agent issue cannot be resolved through the Machine Messages or Troubleshooting references and debug data must be captured and forwarded to SMA Technologies.
- Use this page to understand which debug files to collect, how to transfer them, and how to minimize the performance impact of running the agent in debug mode.

In many production MCP environments, print files are quickly dispatched. Because of this, the MCP Agent debug print files may no longer be available when you attempt to collect the information SMA Technologies requires to identify the cause of an issue quickly and accurately. Timely submission of the debug information discussed in this topic will result in more immediate attention to the issue. In some cases, it is not possible for SMA Technologies to address your concern without this information, and work on the issue will be suspended until the requisite information has been provided.

## Start at the Beginning

### Analyze an Issue
This section identifies the resources and support available to you when an issue occurs.

#### Resource One

If an issue occurs, first check [Machine Messages](reference-information/machine-messages) and [Troubleshooting](reference-information/troubleshooting/). Most issues that have occurred at other customer sites are documented in these sections. It may be possible to take the prescribed action and be up and running again in a very short time.

#### Resource Two

Another source of information is the OpCon User Community hosted through Salesforce. Under the Solutions tab in the Portal, you can search SMA Technologies' knowledge base to help resolve questions, issues, or errors. To learn more about how to access and use the Portal, refer to [OpCon User Community](https://smatechnologies.force.com/SMAOpConUserCommunity/s/login/?language=en_US&startURL=%2FSMAOpConUserCommunity%2Fs%2F&ec=302) in the Support online help.

#### Resource Three

If the particular issue has been addressed neither in the Troubleshooting section nor in the SMArt User Community, then all pertinent information needs to be gathered and provided to the SMA Technologies support representative.

##### Some questions to consider

1. Does this issue occur only on a particular job? If so, does it happen every time this job runs? If so, first check the Operations Related Information on the Enterprise Manager for this job. If there are still some questions as to the cause, enable agent debug, then resubmit the job via OpCon if possible, and then disable agent debug. This captures additional information for this job. If the job summary is available, retrieve it and forward it to the SMA Technologies support individual when the agent debug print files are submitted.

2. Did this issue occur immediately following an MCP Agent upgrade? Note the previous and current MCP Agent version.

3. Did this issue occur immediately following a change to the agent configuration?

4. Did this issue occur immediately after performing an MCP O/S upgrade? Note the previous and current MCP O/S versions.

5. What additional information can be provided that may be helpful in identifying the cause of the issue?

6. What day and time did the issue occur? Was anything unusual also going on at that time?

7. Supply the schedule name, job name, and specific details about the unexpected behavior of the OpCon job affected. Run the DataCollector to collect the OpCon logs that include the time during which the issue occurred.

### About Debugging

SMA Technologies strongly recommends that sites do NOT run continuously with debug set. The debug switches cause a very large volume of data to be written to the agent debug print files, which can result in excessive disk space usage and a decrease in agent throughput due to the additional I/O.
 
Also, be advised that if running an OpCon job whose processing path is altered via the use of program switches, the expected results with that program may not be achieved. Programs inherit the switch settings of the processes that initiated them, and the agent initiates OpCon jobs.
 
If the issue affects all jobs (or the agent itself), SMA Technologies recommends that debug switches for all agent components be activated. This may be accomplished in several ways.

### Enable Debug

Select INITDEBUG from the SMAMAINMENU and follow the screen prompts. The optional timer is the number of minutes for which to capture debug information. If the timer is omitted, debugging remains active until a) debugging is disabled via the SMA/MANAGER screen selection, STOPDEBUG, or b) the agent is brought down. This method sets debug switches for all the agent components, excluding the Resource and File Monitors. To enable debugging for the Resource and File Monitors, deliver an AX DEBUG ```<optional timer>``` to the \*SMA/RESOURCE/MONITOR/xxx module.
 
To view the previous information, refer to [Enable Debug](reference-information/legacy#enable-debug) in the Legacy Information topic.

### Collect Debug Information

The MCP Agent includes a utility, \*SMASUP, which gathers agent debug information. The SMASUP utility requires information about the agent environment in order to retrieve the information SMA Technologies requires.
If the debug switches were set using the AX DEBUG ```<optional timer>``` command and the timer was used, when the timer expires, the \*SMA/COMM/xxx and/or \*SMA/RESOURCE/MONITOR/xxx module(s) will automatically cause the \*SMASUP program to run using the environmental information supplied by \*SMA/COMM/xxx or \*SMA/RESOURCE/MONITOR/xxx.
 
If the ```<optional timer>``` was not used with the INITDEBUG command, stop debugging by selecting the STOPDEBUG option on the Main Menu in SMA/MANAGER. This causes the *SMASUP program to run automatically.

### SMASUP Output

The SMASUP utility creates three files: SMASUPTXT, SMASUPFILCON, and SMASUPPRTCON. Each of these files should be treated separately from each other and from any additional files that are being sent to SMA Technologies (such as job summaries). Each of these files need to be retrieved from the MCP to a Windows machine. Attach each of the files to the Support case created through the SMArt User Community, email the files to the first-line OpCon support individual, or place them on the SMA Technologies FTP site.

### SMASUPTXT

The SMASUPTXT file is an ASCII text file. It should be FTPed using ASCII (or text) transfer type. This file may be viewed on any machine that supports ASCII text files (such as a Windows machine). It contains environmental information, flat data files, the agent configuration audit log, copies of SMA WFLs, and so on, and is crucial to SMA Technologies support staff.

### SMASUPFILCON

The SMASUPFILCON file is a container file and has agent data files. It should be FTPed using binary transfer type. The contents of this file can only be utilized after the container has been unwrapped to an MCP machine. The data files are sometimes used by SMA Technologies development staff to attempt to duplicate the customer's agent state. If SMASUP is run while the agent is running, some agent data files will not be included in this container.

### SMASUPPRTCON

The SMASUPPRTCON file is a container file and has agent debug print files. It should be FTPed using binary transfer type. The contents of this file can only be utilized after the container has been unwrapped to an MCP machine. These files contain debug information captured by the agent and are crucial to SMA Technologies development staff in analyzing an issue. If SMASUP is run while the agent is running, not all debug print files may be captured within this container. If there are no print files to capture, this container file will not be created.
 
Avoid sending an entire sumlog to SMA Technologies when at all possible. The sumlog should NOT be viewed as an alternative to the agent debug print files. The agent debug print files contain data relative to the internal behavior of the agent — information that would not be present in the sumlog.