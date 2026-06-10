---
sidebar_label: 'Release notes'
title: MCP Agent release notes
description: "Version history and change details for the OpCon MCP Agent, including new features, improvements, and bug fixes."
tags:
  - Reference
  - System Administrator
  - Agents
---

# MCP Agent release notes

## 21

### 21.06.00

April 2025

:white_check_mark: **OC-1761**: Fixed a bug in the MCP Agent which was generating large debug print files through the Resource Monitor component, causing it to crash even when debug mode was not turned on.

:white_check_mark: **MCP-606**: Resource Monitor was excessively logging activity in the debug log when debugging was turned off, causing heavy CPU usage. Fixed Resource Monitor to only log detailed activity when debugging is turned on.

### 21.05.00

December 2024

:white_check_mark: **MCP-605**: Fixed an issue in the Resource Monitor where debug logging was not activating when SW2 was set.

### 21.04.00

September 2023

:white_check_mark: Fixed processing DISPLAY tokens containing a period (.) character as a token separator. Fixed a crash in the TCPIP module when an incoming message header gets defragmented.

:white_check_mark: Fixed a crash (SEG ARRAY error) in MCP JORS during program startup.

:white_check_mark: Fixed a crash (SEG ARRAY error) in the SMA/TCPIP program.

### 21.00.00

July 2021

:white_check_mark: Using a common global storage for the JobStart command was causing incorrect reporting of JobStart information when several jobs were started at the same time. Changed the MCP/INTERFACE to store the job start command in the array of job-specific tracking information.

:white_check_mark: If querying for MYSELF.NAME did not return information about the PACK on which the MANAGER program was running, the program was not handling it correctly to identify the location for storing DISPLAYS files. Modified the MANAGER program to work with that scenario as well.

:white_check_mark: Enhanced the MANAGER program to allow for USERCODES without passwords to start the LSAM and Resource Monitor. If you have a blank password for a USERCODE you want to use, enter a period (.) in the password field.

## 20

### 20.00.00

June 2020

### What's new

:eight_spoked_asterisk: It is now possible to request that the Resource Monitor be stopped when the LSAM has been requested to stop. Use the STOPLSAM screen to accomplish this.

:eight_spoked_asterisk: With the release of MCP LSAM 20.00.00 (compiled on MCP 60.1), versions of MCP LSAM 19.00.00 and 19.01.00 have been compiled on MCP 60.1 and are now available. Previously, MCP LSAM versions 19.00.00 and 19.01.00 were originally compiled on MCP 58.1.

:eight_spoked_asterisk: A new utility, SMA/WFL/FILEARRIVAL, has been added to the suite of MCP LSAM utilities. It allows you to monitor, within an optional time frame, the arrival of a file on the current day. Upon detecting the file has met the title and optional time-altered constraints, the user-defined global property is updated to reflect the full file title of a file meeting the selection criteria. If no file is found during the specified timeframe, the job fails. FILEARRIVAL runs as an OpCon job and does not require LSAM configuration or definition files.

### Why this matters

The STOPLSAM integration with Resource Monitor simplifies shutdown procedures by stopping both components together. The new SMA/WFL/FILEARRIVAL utility enables file arrival monitoring as a native OpCon job, removing the need for custom WFL scripts and providing a supported, configuration-free option for time-windowed file detection.

#### Fixes

:white_check_mark: Fixed an issue where the two fields on the LOADDISP screen are longer than one character but should be the length of one.

:white_check_mark: Upon creating a new LSAM configuration file from scratch, the SMAGEN screen of the SMA/MANAGER program displayed corrupted data. This has been resolved.

:white_check_mark: USERCODES longer than 11 characters caused SMA/JORS to F-DS. This has been resolved.

## 19

### 19.01.00

December 2019

:white_check_mark: When using the INITLSAM option within the Manager program and an LSAM and/or Resource Monitor USERCODE had been defined on the GEN screen, the Manager program failed to include the USER= statement in the WFL used to start the LSAM and/or Resource Monitor. This has been corrected.

In conjunction with the above change, the following changes were made to the GEN screen and start WFLs:

* Fields were created to accommodate the use of ACCESSCODE in the WFLs generated for initiating the LSAM and/or Resource Monitor.
* All password fields are masked on the GEN screen.

:white_check_mark: When the SMASUP program ran, it was waiting on a file incorrectly named \*SMA/CONFIG/AUDIT. This has been corrected.

:white_check_mark: When the MCP LSAM was configured to connect only with specified IP addresses, the LSAM would report that the IP address was invalid even though the OpCon IP address was in the list of allowed IP addresses. This has been corrected.

:white_check_mark: When the user specified an allowed IP address, all other allowed IP address fields required an entry. This has been corrected.

## 18

### 18.01.00

December 2018

### What's new

:eight_spoked_asterisk: The SMA/MANAGER program has been updated to automatically back up configuration and definition files and to allow the user to restore a backup file as the production file.

### 18.00.00

June 2018

### What's new

:eight_spoked_asterisk: Effective with this release, a new MCP-based user interface, \*SMA/MANAGER, is available for configuring the LSAM and utilities and for managing operational tasks associated with the LSAM. This new interface should be used in place of the \*SMA/CONFIG program, which will be de-implemented in a subsequent LSAM release.

The SMA/MANAGER program provides a single interface for performing configuration and operations tasks related to the MCP LSAM. It replaces the \*SMA/CONFIG program, and reduces the MCP-specific knowledge required to perform routine operational tasks. Upon accessing \*SMA/MANAGER, the user is presented with a main menu. All activities are performed by navigating successive screen choices until the final screen is reached. In most cases, the user need only make a selection from the Main Menu to arrive at the final screen.

:eight_spoked_asterisk: MCP LSAM Resource Monitor now detects if there is already an instance of this Resource Monitor running. If so, it displays and writes to the debug log an error, and then exits.

:eight_spoked_asterisk: The SMA/INSTALL program now edits the user's FAMILY statement to determine if the target family for the LSAM installation or upgrade is the same as the user's only family. If there is a difference, the user is asked for permission to change the family statement for the duration of the install/upgrade. If differences exist and permission is not granted, the SMA/INSTALL program exits without performing the install/upgrade.

:eight_spoked_asterisk: The MCP LSAM no longer creates print files named as \*REMLPnn, where nn is the MCS number (in IDC) of the MCP LSAM.

:eight_spoked_asterisk: If a job fails with the error DATA TOO LONG, the Job Details field that contains the long data can be identified by viewing the job information in OpCon under Configuration > Operations Related Information > Detailed Job Messages.

:eight_spoked_asterisk: If the user attempts to use a config file that is less than seven records, the Algolprocs library unconditionally logs an error in the debug log and exits. The error message is "Config file is too short - Use SMA/MANAGER to update config file."

### Why this matters

The new SMA/MANAGER interface centralizes configuration and operational tasks for the MCP LSAM, replacing SMA/CONFIG and reducing the MCP-specific knowledge required for routine operations. Resource Monitor now self-detects duplicate instances to prevent conflicts, and SMA/INSTALL validates the FAMILY statement to prevent installation to the wrong target.

## 17

### 17.01.00

2017 September

### What's new

:eight_spoked_asterisk: The MCP LSAM installation and configuration documentation has been modified to emphasize the importance of a correct FAMILY assignment in order to prevent issues that arise from an improper FAMILY statement.

### 17.00.01

2017 September

:white_check_mark: For MCP LSAM 17.0, two LSAM components, SMA/RESOURCE/CHECK and SMA/FTAGENT, were excluded from the installation/upgrade activity. This issue has been corrected in MCP LSAM 17.00.01.

### 17.0

2017 May

:white_check_mark: When multiple file transfers were run in rapid succession, occasionally the \*SMA/FTSERVER component would display an error, "No matching port...", the transfer would fail, and the resolution was to restart the FTSERVER. This has been corrected.

## 16

### 16.02.01

2017 September

:white_check_mark: For MCP LSAM 16.02, two LSAM components, SMA/RESOURCE/CHECK and SMA/FTAGENT, were excluded from the installation/upgrade activity. This issue has been corrected in MCP LSAM 16.02.01.

### 16.02

2017 January

### What's new

:eight_spoked_asterisk: Effective with MCP LSAM 16.02, the user is able to modify the \*SMA/WFL/REMOVEJOB WFL to elect to have the WFL complete OK even if there are no files deleted. Security errors and locked files still cause the REMOVEJOB WFL to be reported as failed in this case.

To implement the alternate behavior, modify a working copy of \*SMA/WFL/REMOVEJOB to comment out sequence #26600 and un-comment sequence 26650. Because the default behavior is to fail the REMOVE MCP job if there are no files to remove, it is necessary to re-implement this modification each time the MCP LSAM is upgraded if the alternate behavior is desired.

:eight_spoked_asterisk: Effective with MCP LSAM 16.02, two versions of the compiled MCP LSAM software are made available. One version is compiled for LEVEL5 machines, the other for LEVEL6 machines. To determine the appropriate version for your site, interrogate the COMPILERTARGET system option.

:eight_spoked_asterisk: The \*SMA/INSTALL/nnnnnn program has been modified to confirm that a numeric version number is part of the Install program name.

:eight_spoked_asterisk: TLS certificates must be installed for the same USERCODE that is used for all SMA File Transfer jobs. This is a requirement because certificates are stored with a USERCODE and only the specified USERCODE may access the certificate.

#### Fixes

:white_check_mark: The following errors were displayed upon startup of the SMA/FTSERVER:

* ATTRIBUTE ERROR:TCP_PORT.SECUREPROTOCOL INVALID SUBFILE INDEX @ 01C:007D:1
* ATTRIBUTE ERROR:TCP_PORT.SSLSECUREMODE INVALID SUBFILE INDEX @ 01C:0071:5
* ATTRIBUTE ERROR:TCP_PORT.SSLERROR INVALID SUBFILE INDEX @ 01C:0063:5

This has been corrected.

:white_check_mark: The instructions within the discussion of MSGIN were inaccurate and have been corrected.

### 16.01.00

2016 July

### What's new

:eight_spoked_asterisk: Effective with MCP LSAM 16.01.00, the SMASUP program runs automatically any time one of the MCP LSAM modules terminates abnormally (-DS). If debugging had not been enabled when the module stopped, minimal information is contained within the containers created by SMASUP. However, these should be submitted with the Salesforce incident report nonetheless as they contain information that may be useful in researching the issue.

#### Fixes

:white_check_mark: The SMA/FTHANDLER was not refreshing the Append LF to Unix value when told to pick up new LSAM configuration values. This has been corrected.

:white_check_mark: Restarting a "tracked" job resulted in successive JOB ADOPT messages and confusing job status messages. Effective with this release, if a user restarts a tracked job, the job runs and is reported as an OpCon job, not as a tracked job.

:white_check_mark: When running an SMA File Transfer job, if a corresponding FTServer failed to comply with the maximum packet size and sent a message longer than the negotiated packet size, the MCP FTAgent did not exit gracefully. This has been corrected and the FTAgent now responds by reporting the condition and exiting in a controlled manner.

:white_check_mark: On rare occasion, a short-running MCP OpCon job submitted with a RUN command would be incorrectly reported as having failed. This has been corrected.

### 16.0

2016 July

### What's new

:eight_spoked_asterisk: With OpCon 16.0, new MCP Job Details tabs have been added for file and task attribute definitions. Identification of a job-specific or template displays file (SMADISPLAY identifier) has been isolated to a new field on the job definition screen. The SMATASK identifier has been replaced by a check box on the job definition screen.

MCP LSAM 16.0 continues to support older versions of OpCon, as well as OpCon 16.0 and up, eliminating the need to upgrade both the MCP LSAM and the core OpCon components simultaneously. Versions of the MCP LSAM prior to 16.0 do NOT support the new Job Details fields in OpCon 16.0.

:::info Note

With the addition of the new Job Details fields, the sizes of the checkpointed arrays have changed. When upgrading to MCP LSAM 16.0 from an older MCP LSAM version, you must remove the checkpoint files after bringing down the LSAM and before starting the upgrade process. Failure to do this results in the MCP LSAM failing shortly after initiation has been attempted.

:::

:eight_spoked_asterisk: Effective with MCP LSAM 16.0, you may elect to secure your scheduling (SMANetcom) and View Job Output (JORS) communications using TLS. At this time, your TLS configuration options for scheduling automatically also apply to View Job Output. MCP SMA File Transfer does not support communications using TLS.

:eight_spoked_asterisk: The File Monitor has been modified to persist in trying to send an external event if the original attempt failed due to a file lock.

:eight_spoked_asterisk: Added support for a new System Property named $START COMMAND. The value of this property resolves to the value of the start command the Agent attempted. If for any reason the Agent does not set the value for this property, the value returns as "Unavailable."

:eight_spoked_asterisk: Effective with this release, the installation procedures for the MCP LSAM have changed. The two container files required for installation or upgrade are now contained within a single zipped file. Both the container files and the zip file now contain the MCP LSAM release number as part of the name. Note that the \*SMA/INSTALL program is now uniquely named during the unwrap process. It is critical that you use the 6-digit version number to name the SMA/INSTALL program because this version number is used to identify which container from which to unwrap the LSAM executables and files.

:eight_spoked_asterisk: Access to MCP LSAM configuration settings is now provided via an API exported by the SMA/ALGOLPROCS library. With the exception of the \*SMA/CONFIG program, MCP LSAM components no longer access the configuration file directly. This reduces the IO overhead required at BOJ and upon delivery of the AX CONFIG command.

### Why this matters

MCP LSAM 16.0 adds TLS support for scheduling and JORS communications, the File Monitor's resilience to file lock events, and a new $START COMMAND system property for job diagnostics. The consolidated installation archive and version-stamped installer name simplify version management when working with multiple LSAM versions concurrently.

#### Fixes

:white_check_mark: Fixed an issue where a parameter to a user program was truncated by the MCP Agent when it required double quotes. The parameter is now passed in its entirety.

:white_check_mark: Occasionally some \*TEMP/SMA/= files remain present after the OpCon job completes. Additional code was added to remove these files at a second point in the process flow.

:white_check_mark: When using the CONVERT/PRINT utility, some print files were incomplete after using SMA File Transfer to place them on a Windows machine. The cause of this was in the CONVERT/PRINT utility and the issue has been corrected.

:white_check_mark: The SYNTAX/CHECK program was incorrectly reporting an error if a valid token name within the perfmon definitions file was not followed immediately by a space. This has been corrected.
