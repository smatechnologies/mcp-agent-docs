---
title: MCP Agent Initialization/Stopping Troubleshooting
description: "Troubleshooting guidance for MCP Agent startup and shutdown issues including configuration file missing, seg array errors, INVALID INDEX errors, and LSAM stopping unexpectedly."
tags:
  - Reference
  - System Administrator
  - Agents
---

# LSAM Initialization/Stopping

## Configuration File Missing

#### Full Description
The agent reports the configuration file is absent.
 
#### Possible Explanation:
 
The SMA/CONFIG/FILE/xxx is not present under the same usercode used to start the agent.

##### Operator Response:

Copy the SMA/CONFIG/FILE/xxx under the appropriate usercode. For more information on this response, refer to \*[SMA/CONFIG](../../operations-and-components/core-programs-and-files#smaconfig).
 
## SEG ARRAY ERR @ 00081445

#### Full Description

The *SMA/TCPIP module reports "seg array error @ 00081445".
 
#### Possible Explanation:
 
Both JORS and the agent are configured to use the same port. They each need their own unique port number.

##### Operator Response:

Change the JORS port number in the agent configuration file and change the Advanced Machine setting for JORS port number in the Enterprise Manager to match the unique JORS port number in the agent configuration file.
 
## I-DS @ 66100

#### Full Description

\*SMA/COMM/xxx goes I-DS @ 66100.
 
#### Possible Explanation:
 
The \*SMA/MCP/INTERFACE/xxx module is not defined to IDC.

##### Operator Response:

Define \*SMA/MCP/INTERFACE/xxx as an MCS to IDC.
 
## LSAM Slow to Come Down

#### Full Description

The LSAM takes too long to come down.
 
#### Possible Explanation:
 
Depending on current agent activity, the ```<mix# *SMA/COMM/xxx >```HI 99 command may bring the agent down too slowly.

##### Operator Response:

Issue a HI 2 to the *SMA/TCPIP/xxx module. DS'ing the agent is also an alternative, although it is not recommended. For more information on this response, refer to *[SMA/TCPIP](../../operations-and-components/core-programs-and-files#smatcpip-associated-files).
 
## SEG ARRAY ERR @ 2435000

#### Full Description

\*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 2435000.
 
#### Possible Explanation:
 
This can occur if the agent has just been upgraded and one or more OpCon jobs were left running prior to the upgrade.

#### Operator Response:

1. Remove \*SMA/CP/MCS/xxx/= ON ```<packname>```

2. Start the agent.

For more information on this response, refer to [MCP Agent Installation](../../installation/overview).
 

## SEG ARRAY ERR @ 178600

#### Full Description

\*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 178600.
 
#### Possible Explanation:
 
The "max number of concurrent jobs" configuration value has been changed.

#####  Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the agent:

1. \*SMA/TRACKING/FILE/xxxON ```<packname>```

2. \*SMA/CP/MCS/xxx/= ON ```<packname>```

3. Be sure to check all families on the system - not just the family on which the agent runs.

For more information on this response, refer to [Update the "Max Number Concurrent Jobs" Field](../../configuration/update-max-concurrent-jobs).
 
## ASSERTION FAILURE @ 91700

#### Full Description

\*SMA/COMM/xxx gets ASSERTION FAILURE ON RANGE TEST @ (Expression out of range 91700).
 
#### Possible Explanation:
 
The "max number of concurrent jobs" configuration value has been changed.

##### Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the agent:

1. \*SMA/TRACKING/FILE/xxxON ```<packname>```

2. \*SMA/CP/MCS/xxx /= ON ```<packname>```

3. Be sure to check ALL families on the system - not just the family on which the agent runs.
 
## LSAM Waiting for SMALIBRARY

#### Full Description

Agent modules are in the waiting mix awaiting the SMALIBRARYxxx.
 
#### Possible Explanation:
 
The \*SMA/ALGOLPROCS/xxx module has not been declared as a library.

##### Operator Response:

Declare the \*SMA/ALGOLPROCS/xxx module as a library with the following command:
```SL SMALIBRARYxxx= *SMA/ALGOLPROCS/xxxONEONLY```
 
## INVALID INDEX @ 02412000 or 04637000

#### Full Description

\*SMA/MCP/INTERFACE/xxx has left the active mix with the following error: "F-DS INVALID INDEX @ 02412000" - or -
 
\*SMA/MCP/INTERFACE/xxx gets INVALID INDEX @ (04637000).
 
#### Possible Explanation:
 
The cause of this situation is failure to remove the *SMA/CP/MCS/xxx/= and *SMA/TRACKING/FILE/xxx files after changing the "max number of concurrent jobs" configuration variable.

##### Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the agent:

1. \*SMA/TRACKING/FILE/xxx ON ```<packname>```

2. \*SMA/CP/MCS/xxx/= ON ```<packname>```

3. Be sure to check ALL families on the system - not just the family on which the agent runs.
 
## Codefile will not Run...

#### Full Description

The \*SMA/MCP/INTERFACE module displays the following messages when an LSAM begins a job, and when a user WFL is submitted via OpCon:
 
12131 14:56 This nn.n codefile will not run on software released on or after.... Refer to the Release and Support Policy Overview.
 
12131 14:56 Warning 137: This codefile must be recompiled in order to run on future releases. @ (00146000)
 
#### Possible Explanation:
 
The active MCP Agent was compiled on an older version of MCP.

##### Operator Response:

Obtain and install a version of the MCP Agent compiled on a newer version of MCP.
 
## SEG ARRAY ERR around 924100

#### Full Description

\*SMA/ALGOLPROCS/xxx fails with SEG ARRAY ERR around 924100.
 
#### Possible Explanation:
 
The \*SMA/CP/LIB/= files were not removed after changing the maximum number of concurrent jobs.

##### Operator Response:

Remove the \*SMA/CP/LIB/= files. For more information on this response, refer to [Remove Checkpoint and Tracking Files](../../configuration/update-max-concurrent-jobs#remove-checkpoint-and-tracking-files)
 
## LSAM Stops Soon after Starting

#### Full Description

The agent begins to come up, but soon goes down again. One of these scenarios may be true:
 
The notation "DCWRITE error 66" is present in the debug print file of the SMA/MCP/INTERFACE/xxx module - or -
 
The message "EOT \*SMA/MCP/INTERFACE" is displayed on the system console as the agent begins to come up, but soon goes down again - or -
 
The notation "Linkage class violation in interface SMALIBRARYxxx to Library \*SMA/ALGOLPROCS/xxx" is present in the system log and on the system console.
 
#### First Possible Explanation:
 
The SMA/MCP/INTERFACE/xxx module has been installed as a usercoded file instead of a non-usercoded file. The SMA/MCP/INTERFACE/xxx must be non-usercoded because IDC does not permit the definition of a usercoded MCS. Attempting to initiate the agent without first defining SMA/MCP/INTERFACE/xxx as an MCS results in a DCWRITE error 66 (MCS not defined in NDLII). This error causes the SMA/MCP/INTERFACE/xxx module to terminate.
 
The agent expects all of its files to be located in the same directory as the module; consequently, running all modules, except the SMA/MCP/INTERFACE/xxx, under a usercode causes the SMA/MCP/INTERFACE/xxx to be unable to locate the necessary files.

##### First Operator Response:

Ensure the \*SMA/MCP/INTERFACE/xxx ON ```<diskpack>``` is present and define this program to IDC as an MCS. For more information on this response, refer to [Define LSAM to IDC](../../installation/new-installation#define-the-agent-to-idc).

#### Second Possible Explanation:
 
During the process of upgrading the MCP operating system, the definition of the SMA/MCP/INTERFACE/xxx module to IDC has been lost. Attempting to initiate the agent without first defining SMA/MCP/INTERFACE/xxx as an MCS results in a DCWRITE error 66 (MCS not defined in NDLII). This error causes the SMA/MCP/INTERFACE/xxx module to terminate, bringing the entire agent to EOJ shortly thereafter.

##### Second Operator Response:

Ensure the \*SMA/MCP/INTERFACE/xxx ON ```<diskpack>``` is present and define this program to IDC as an MCS. For more information on this response, refer to [Define LSAM to IDC](../../installation/new-installation#define-the-agent-to-idc).

#### Third Possible Explanation:
 
The SMA/ALGOLPROCS/xxx module was not marked as a privileged program during installation.

##### Third Operator Response:

Ensure the \*SMA/ALGOLPROCS/xxx module was not marked as a privileged program during installation.
 
SMA Technologies strongly recommends that the MCP Agent installation utility, \*SMA/INSTALL, be used for installations and upgrades in lieu of performing the installation steps manually.
 
## SMA/MCP/INTERFACE Goes Waiting

#### Full Description

Upon agent initiation or job initiation, the \*SMA/MCP/INTERFACE goes into the waiting mix, unable to locate SMALIBRARY or \*SMA/ALGOLPROCS.
 
#### Possible Explanation:
 
The usercode used to install the agent and then run the agent does not have as its primary family the family on which the agent resides.

##### Operator Response:

Either change the primary family of the usercode to match the agent's family, or use a different usercode that already meets this requirement and re-initialize the agent. In some cases, it may be necessary to completely re-install the agent.
 
## INVALID INDEX @ 02430350

#### Full Description

Upon LSAM initiation or job initiation, \*SMA/MCP/INTERFACE gets Invalid index @ 02430350.
 
#### Possible Explanation:
 
The site has upgraded agent versions and failed to remove the \*SMA/CP/MCS/= files after stopping the old version of the agent and prior to starting the new version.

##### Operator Response:

Remove the \*SMA/CP/MCS/= files from the family on which the agent resides. Restart the agent.
 
## INVALID OPERATOR @ 02693716

#### Full Description

Upon starting a MCP REMOVE job, the \*SMA/MCP/INTERFACE/xxx gets Invalid Operator @ 02693716.
 
#### Possible Explanation:
 
The site has multiple agent instances and a REMOVE MCP job follows a job with a very long file title.

##### Operator Response:

Upgrade the MCP Agent to version 05.03.00, or higher.
