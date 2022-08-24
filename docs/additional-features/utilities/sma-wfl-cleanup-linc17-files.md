# *SMA/WFL/CLEANUP/LINC17/FILES

The WFL \*SMA/WFL/CLEANUP/LINC17/FILES utility is used to clean up the \*SMA/LINC17/FILES directory on the MCP. This directory contains files created when an EAE/AB Suite MCP job is run using an ACCEPTFILE. When the EAE/ABSUITE job is run, the Acceptfile is created using the name specified in the Job Details. This file is copied to the *SMA/LINC17/FILES directory, and the original file is removed when the job completes or fails. A copy remains under \*SMA/LINC/17/FILES. For example, an Acceptfile named (MYUC)MY/ACCEPTFILE/TEST will appear in the \*SMA/LINC17/FILES directory as \*SMA/LINC17/FILES/MYUC/MY/ACCEPTFILE.
 
The \*SMA/WFL/CLEANUP/LINC17/FILES utility accepts two parameters. The first is the number of days' worth of Acceptfiles to keep; the second is the family on which to search for the \*SMA/LINC17/FILES directory.

