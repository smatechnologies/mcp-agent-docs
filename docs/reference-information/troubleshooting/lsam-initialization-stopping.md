# LSAM Initialization/Stopping

## Configuration File Missing

#### Full Description
The LSAM reports the configuration file is absent.
 
#### Possible Explanation:
 
The SMA/CONFIG/FILE/xxx is not present under the same usercode used to start the LSAM.

##### Operator Response:

Copy the SMA/CONFIG/FILE/xxx under the appropriate usercode. For more information on this response, refer to \*[SMA/CONFIG](../../operations-and-components/core-programs-and-files#smaconfig).
 
## SEG ARRAY ERR @ 00081445

#### Full Description

The *SMA/TCPIP module reports "seg array error @ 00081445".
 
#### Possible Explanation:
 
Both JORS and the LSAM are configured to use the same port. They each need their own unique port number.

##### Operator Response:

Change the JORS port number in the LSAM configuration file and change the Advanced Machine setting for JORS port number in the Enterprise Manager to match the unique JORS port number in the LSAM configuration file.
 
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
 
Depending on current LSAM activity, the ```<mix# *SMA/COMM/xxx >```HI 99 command may bring the LSAM down too slowly.

##### Operator Response:

Issue a HI 2 to the *SMA/TCPIP/xxx module. DS'ing the LSAM is also an alternative although is not recommended. For more information on this response, refer to *[SMA/TCPIP](../../operations-and-components/core-programs-and-files#smatcpip-associated-files).
 
## SEG ARRAY ERR @ 2435000

#### Full Description

\*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 2435000.
 
#### Possible Explanation:
 
This can occur if the LSAM has just been upgraded and one or more OpCon jobs were left running prior to the upgrade.

#### Operator Response:

1. Remove \*SMA/CP/MCS/xxx/= ON ```<packname>```

2. Start the LSAM.

For more information on this response, refer to [MCP LSAM Installation](../../installation/introduction).
 

## SEG ARRAY ERR @ 178600

#### Full Description

\*SMA/MCP/INTERFACE/xxx gets SEG ARRAY ERR @ 178600.
 
#### Possible Explanation:
 
The "max number of concurrent jobs" configuration value has been changed.

#####  Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the LSAM:

1. \*SMA/TRACKING/FILE/xxxON ```<packname>```

2. \*SMA/CP/MCS/xxx/= ON ```<packname>```

3. Be sure to check all families on the system - not just the family on which the LSAM runs.

For more information on this response, refer to [Update the "Max Number Concurrent Jobs" Field](../../configuration/update-max-concurrent-jobs).
 
## ASSERTION FAILURE @ 91700

#### Full Description

\*SMA/COMM/xxx gets ASSERTION FAILURE ON RANGE TEST @ (Expression out of range 91700).
 
#### Possible Explanation:
 
The "max number of concurrent jobs" configuration value has been changed.

##### Operator Response:

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the LSAM:

1. \*SMA/TRACKING/FILE/xxxON ```<packname>```

2. \*SMA/CP/MCS/xxx /= ON ```<packname>```

3. Be sure to check ALL families on the system - not just the family on which the LSAM runs.
 
## LSAM Waiting for SMALIBRARY

#### Full Description

LSAM modules are in the waiting mix awaiting the SMALIBRARYxxx.
 
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

After changing the configuration variable "max number concurrent jobs", remove the following files before starting the LSAM:

1. \*SMA/TRACKING/FILE/xxx ON ```<packname>```

2. \*SMA/CP/MCS/xxx/= ON ```<packname>```

3. Be sure to check ALL families on the system - not just the family on which the LSAM runs.
 
## Codefile will not Run...

#### Full Description

The \*SMA/MCP/INTERFACE module displays the following messages when an LSAM begins a job, and when a user WFL is submitted via OpCon:
 
12131 14:56 This nn.n codefile will not run on software released on or after.... Refer to the Release and Support Policy Overview.
 
12131 14:56 Warning 137: This codefile must be recompiled in order to run on future releases. @ (00146000)
 
#### Possible Explanation:
 
The active MCP LSAM was compiled on an older version of MCP.

##### Operator Response:

Obtain and install a version of the MCP LSAM compiled on a newer version of MCP.
 
## SEG ARRAY ERR around 924100

#### Full Description

\*SMA/ALGOLPROCS/xxx fails with SEG ARRAY ERR around 924100.
 
#### Possible Explanation:
 
The \*SMA/CP/LIB/= files were not removed after changing the maximum number of concurrent jobs.

##### Operator Response:

Remove the \*SMA/CP/LIB/= files. For more information on this response, refer to [Remove Checkpoint and Tracking Files](../../configuration/update-max-concurrent-jobs#remove-checkpoint-and-tracking-files)./installation/new-installation#define-lsam-to-idc
 
## LSAM Stops Soon after Starting

#### Full Description

The LSAM begins to come up, but soon goes down again. One of these scenarios may be true:
 
The notation "DCWRITE error 66" is present in the debug print file of the SMA/MCP/INTERFACE/xxx module - or -
 
The message "EOT \*SMA/MCP/INTERFACE" is displayed on the system console as the LSAM begins to come up, but soon goes down again - or -
 
The notation "Linkage class violation in interface SMALIBRARYxxx to Library \*SMA/ALGOLPROCS/xxx" is present in the system log and on the system console.
 
#### First Possible Explanation:
 
The SMA/MCP/INTERFACE/xxx module has been installed as a usercoded file instead of a non-usercoded file. The SMA/MCP/INTERFACE/xxx must be non-usercoded because IDC does not permit the definition of a usercoded MCS. Attempting to initiate the LSAM without first defining SMA/MCP/INTERFACE/xxx as an MCS results in a DCWRITE error 66 (MCS not defined in NDLII). This error causes the SMA/MCP/INTERFACE/xxx module to terminate.
 
The LSAM expects all of its files to be located in the same directory as the module; consequently, running all modules, except the SMA/MCP/INTERFACE/xxx, under a usercode causes the SMA/MCP/INTERFACE/xxx to be unable to locate the necessary files.

##### First Operator Response:

Ensure the \*SMA/MCP/INTERFACE/xxx ON ```<diskpack>``` is present and define this program to IDC as an MCS. For more information on this response, refer to [Define LSAM to IDC](../../installation/new-installation#define-lsam-to-idc).

#### Second Possible Explanation:
 
During the process of upgrading the MCP operating system, the definition of the SMA/MCP/INTERFACE/xxx module to IDC has been lost. Attempting to initiate the LSAM without first defining SMA/MCP/INTERFACE/xxx as an MCS results in a DCWRITE error 66 (MCS not defined in NDLII). This error causes the SMA/MCP/INTERFACE/xxx module to terminate, bringing the entire LSAM to EOJ shortly thereafter.

##### Second Operator Response:

Ensure the \*SMA/MCP/INTERFACE/xxx ON ```<diskpack>``` is present and define this program to IDC as an MCS. For more information on this response, refer to [Define LSAM to IDC](../../installation/new-installation#define-lsam-to-idc).

#### Third Possible Explanation:
 
The SMA/ALGOLPROCS/xxx module was not marked as a privileged program during installation.

##### Third Operator Response:

Ensure the \*SMA/ALGOLPROCS/xxx module was not marked as a privileged program during installation.
 
SMA Technologies strongly recommends that the MCP LSAM installation utility, \*SMA/INSTALL, be used for installations and upgrades in lieu of performing the installation steps manually.
 
## SMA/MCP/INTERFACE Goes Waiting

#### Full Description

Upon LSAM initiation or job initiation, the \*SMA/MCP/INTERFACE goes into the waiting mix, unable to locate SMALIBRARY or \*SMA/ALGOLPROCS.
 
#### Possible Explanation:
 
The usercode used to install the LSAM and then run the LSAM does not have as its primary family the family on which the LSAM resides.

##### Operator Response:

Either change the primary family of the usercode to match the LSAM's family, or use a different usercode that already meets this requirement and re-initialize the LSAM. In some cases, it may be necessary to completely re-install the LSAM.
 
## INVALID INDEX @ 02430350

#### Full Description

Upon LSAM initiation or job initiation, \*SMA/MCP/INTERFACE gets Invalid index @ 02430350.
 
#### Possible Explanation:
 
The site has upgraded LSAM versions and failed to remove the \*SMA/CP/MCS/= files after stopping the old version of the LSAM and prior to starting the new version.

##### Operator Response:

Remove the \*SMA/CP/MCS/= files from the family on which the LSAM resides. Restart the LSAM.
 
## INVALID OPERATOR @ 02693716

#### Full Description

Upon starting a MCP REMOVE job, the \*SMA/MCP/INTERFACE/xxx gets Invalid Operator @ 02693716.
 
#### Possible Explanation:
 
The site has multiple LSAM instances and a REMOVE MCP job follows a job with a very long file title.

##### Operator Response:

Upgrade the MCP LSAM to version 05.03.00, or higher.