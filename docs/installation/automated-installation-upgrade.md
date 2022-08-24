# Automated Installation/Upgrade

The \*SMA/INSTALL program automates most of the steps required for an installation or upgrade. To install and run the *SMA/INSTALL program, use a privileged MCP usercode obtained from the site administrator. This usercode must have as its ONLY family the same family on which the LSAM will reside. *SMA/INSTALL performs the following actions:

* Prompts the user for the following required environmental information:

:::info Note

With each prompt, the user is given the opportunity to abort the process. The installation/upgrade process does not start until all required information has been gathered.

:::

* The type of installation: INSTALL or UPGRADE.
* The family on which the LSAM resides. The user's FAMILY statement is retrieved and analyzed to determine if it is ```<LSAM family>``` ONLY. If it is not, the user will be asked to allow the SMA/INSTALL program to modify the FAMILY statement for the duration of the installation/upgrade. If permission is not granted, the SMA/INSTALL program will exit without performing the install/upgrade.
* The three-character LSAM identifier (or "NONE").

* If "UPGRADE" is specified, performs the following procedures:
    * Backs up the current LSAM programs, LSAM utility WFLs, and LSAM files.
    * The names of the backed up files are preceded with a node of SAVE (e.g., the backup saves ```*SMA/CONFIG/FILE``` as ```*SAVE/SMA/CONFIG/FILE```).
    * Removes the checkpoint, tracking, and message persistence files.
    * Removes the SMA library as a system library.
    * Restores the previously backed-up ```*SMA/CONFIG/FILE```, ```*SMA/FILEMON/DEFS```, ```*SMA/DISPLAYS```, ```*SMA/DISPLAYS/SYSMSG```, and ```*SMA/PERFMON/DEFS``` files.

* Unwraps the release container and names the files using the specified family and LSAM identifier.
* Makes the ```*SMA/ALGOLPROCS/xxx```, ```*SMA/COMMAND/xxx```, ```*SMA/RESOURCE/MONITOR/xxx```, ```*SMA/SURROGATE/xxx```, and ```*SMA/ANNOUNCE/xxx``` programs privileged.
* Makes the ```*SMA/ALGOLPROCS/xxx``` library security PUBLIC IO.
* Establishes ```*SMA/ALGOLPROCS/xxx``` as a system library.
* Sets up the SMAMGR program, window, and agenda in Transaction Server (COMS). The entities are named ```SMAMGRxxx```, where ```xxx``` is the 1-to-3-character identifier for this LSAM.

* If "INSTALL" is specified, performs the following procedures:
    * Sets up the LSAM window in Transaction Server (COMS). The window is named ```LSAMxxx```, where ```xxx``` is the 1-to-3-character identifier for this LSAM.
    * Sets up the SMAMGR program, window, and agenda in Transaction Server (COMS). The entities are named ```SMAMGRxxx```, where ```xxx``` is the 1-to-3-character identifier for this LSAM.
    * Prompts the installer to declare the ```*SMA/MCP/INTERFACE/xxx``` as an MCS using IDC.