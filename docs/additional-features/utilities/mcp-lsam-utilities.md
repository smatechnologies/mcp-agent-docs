# Utilities Overview

Many utilities are provided with the MCP LSAM installation. In the table that follows, a short description of each utility is provided. Click on the link for a more in-depth discussion of the utility.
 
For all utilities accessible to the user, the JOBSUMMARY job variable is set to CONDITIONAL, which will cause a job summary to be created in the event the utility fails. If this is not the behavior desired at your site, you may comment out the JOBSUMMARY = CONDITIONAL; line in the WFL or modify the value to better suit your environment.

| Utility | Short Description |
| ------- | ----------------- |
| File Arrival | A command-line alternative to implementing an OpCon File Arrival job for MCP.The utility is intended to serve the purpose of detecting a file on the MCP platform that has been created within a specified time frame on the date the utility is run. The time frame parameters are optional. Upon detecting a file meeting the criteria, a property will be set to the value of the MCP file title. |
| \*SMA/SYNTAX/CHECK	| Validates the syntax of the contents of the definitions files used by various LSAM modules. These definitions files include \*SMA/DISPLAYS, \*SMA/DISPLAYS/SYSMSG, \*SMA/FILEMON/DEFS and \*SMA/PERFMON/DEFS. |
| *SMA/WFL/CHECK/MIX | Interrogates the Waiting mix or Scheduled mix. This utility provides a batch interface to be used in lieu of an operator logging onto the MCP system to perform the interrogations. |
| \*SMA/WFL/CHANGE | This WFL has been replaced by the MCP Job and Prerun type, CHANGE. Please refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help for a complete discussion of the MCP Job Details. | 
| \*SMA/WFL/CLEANUP/LINC17/FILES	| This utility is used to clean up the *SMA/LINC17/FILES directory on the MCP. The directory contains files created when an EAE/AB Suite MCP job is run using an ACCEPTFILE. |
| \*SMA/WFL/COMMAND | For more information, refer to [Command-line Interface Utility](../../additional-features/lsam-features/command-line-interface-utility). |
| \*SMA/WFL/CONVERT/PRINT (MCP Print File Conversion) | The print conversion utility converts an MCP print file (kind=BACKUPPPRINTER) to an ASCII text file. Sites may find this utility helpful as a preliminary step to a SMA File Transfer job in distributing print files to users for viewing in an ASCII environment (Windows, UNIX, etc.). |
| \*SMA/WFL/COPY	| This WFL has been replaced by the MCP Job and Prerun type, COPY. Please refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help for a complete discussion of the MCP Job Details. |
| \*SMA/WFL/FILECHECK | Allows an OpCon job to be dependent on the presence/absence of a file. |
| \*SMA/WFL/FILECOUNT | Allows an OpCon job to be dependent on the presence/absence of a specified minimum number of files. |
| \*SMA/WFL/PROCESSCHECK	| Allows an OpCon job to be dependent on the existence/absence of a given process in the list of executing processes on the MCP platform. | 
| \*SMA/WFL/REMOVE | This WFL has been replaced by the MCP Job and Prerun type, REMOVE. Please refer to [MCP Job Details](https://help.smatechnologies.com/opcon/core/job-types/mcp) in the Concepts online help for a complete discussion of the MCP Job Details. |
| \*SMA/RESOURCE/CHECK | This utility program checks for the presence of specifies processes or files. It must be run within a user WFL, which can be scheduled using OpCon. |