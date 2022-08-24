# Error and Informational Messages

| Message | Type (Error/Info) | Description/Action Required |
| ------- | ----------------- | --------------------------- |
| ```<file>``` already exists | E | The user attempted to create a definitions file that already exists. Use "E" to edit this definitions file. |
| ```<file>``` does not exist | E | The user attempted to edit a definitions file that does not exist. Use "C" to create the definitions file. |
| Changes saved. REMOVE TRACKING AND CHECKPOINT FILES. | I | The number of maximum jobs has been changed. You must remove the \*SMA/TRACKING/FILE/xxx and \*SMA/CP/= files before starting the LSAM again to avoid a mismatch in file and arrays sizes. |
|Communication configuration saved | I  | Changes made on the SMACOMM screen have been saved to the LSAM configuration file. |
| Enter a valid Action or Choice | E | A menu screen was transmitted without data in both the Action and Choice fields. |
| Enter ALL or valid IP address format | E | The user has 1) left all the IP Address fields blank or 2) has entered an IP address using an incorrect format on the Communication Parameters screen. Enter ALL for the first IP address or correct IP address entries to be in the format directed on this screen. |
| Enter valid IP address format	| E	| The user has entered an IP address using an incorrect format on the Communication Parameters screen. Correct IP address entries to be in the format directed on this screen. |
| General configuration saved | I | Changes made on the General LSAM Configuration screen have been saved. |
| Global displays file already exists | E | User elected to create a global displays file on the DISPMENU screen but the file already exists. |
| Invalid screen name received | E | An invalid screen name was received causing the Main Menu to be displayed. Do not modify the field in the top left corner of each screen. This message is also seen if the user is on the SMAMGR window and transmits a blank screen. |
| Key required for TLS | E | TLS has been enabled but the TLS Key field has been left blank. If TLS is to be used, enter a valid certificate key in this field. If a certificate has not yet been obtained and installed, turn off TLS. |
| LSAM and Resource Monitor submitted for start	| I | The user has configured the LSAM WFL to start both the LSAM and the Resource Monitor, and requested this WFL be started (INITLSAM). Use the STATUS screen to confirm a successful initialization. |
| LSAM submitted for start | I | The user has defined the necessary fields to start the LSAM, and requested this WFL be started (INITLSAM). Use the STATUS screen to confirm a successful initialization. |
| LSAM was instructed to load configuration file | I | The user requested that the LSAM reload the configuration values from the latest config file (LOADDISP). All configuration fields except for the Maximum Concurrent Number of Jobs value are refreshed. <br></br><br></br> To refresh the Maximum Concurrent Number of Jobs, you must: <br></br><br></br> 1. Allow all active jobs to complete <br></br> 2. Stop the LSAM <br></br> 3. Remove the \*SMA/TRACKING/FILE/xxx and \*SMA/CP/= files <br></br> 4. Start the LSAM |
| LSAM was instructed to load global displays file | I | The user requested that the Display Handler reload the global displays file, \*SMA/DISPLAYS. |
| LSAM was instructed to start debug (for n minutes) | I | The user requested the LSAM to start debugging. If a time limit was entered on the INITDEBUG screen, it is also included in the message. |
| LSAM was instructed to stop | I | The user has requested that the LSAM be stopped (STOPLSAM). |
| LSAM was instructed to stop debug | I | The user has manually requested that the LSAM discontinue debugging (STOPDEBUG). |
| Must be < 65536 | E | The optional port number must be 0 or a number less than 65536. |
| Must be = 0 OR > 29 and < 86401 | E | The Resource Monitor timer must be 1) 0 if no system resources are to be monitored, or 2) between 30 and 86400 if monitoring is to occur. | 
| Must be > 0 | E | A numeric value is required to be greater than zero. | 
| Must be > 0 and < 301 | E | A numeric value is required to be between 1 and 300, inclusive. | 
| Must be > 0 and < 501 | E | A numeric value is required to be between 1 and 500, inclusive. | 
| Must be > 0 and < 65536	| E | The required port number must be between 1 and 65535, inclusive. | 
| Must enter A, F, N, or R | E | |	 
| Must enter A, F, or N | E | |	 
| Must enter a numeric value | E | | 
| Must enter a valid family | E | |	 
| Must enter a valid usercode | E | |	 
| Must enter B, I, N, or O | E | |  
| Must enter B, N or Y | E | | 	 
| Must enter D, E, I, or blank | E | In editing message, file, or resource definitions, the user entered an invalid value in the first field of the definition (SMADISPLIST, SMAFILELIST, SMARESLIST screens). |
| Must enter M, N, or U	| E | |	 
| Must enter N, I, or T	| E | |  
| Must enter N or Y	| E | |
| No action selected on FILEMENU | I | The user failed to enter C or E to create or edit the file monitor definitions file. |
| No action selected on RESMENU | I | The user failed to enter C or E to create or edit the resource monitor definitions file. | 
| No changes saved | I | The user did not elect to save changes made on the prior screen. | 
| No file selected for edit on DISPMENU	| I	| The user did not enter a C or E for any of the possible definitions file selections. | 
| No file selected for edit on FILEMENU	| I | The user must enter a C or E to enable creating/updating the File Monitor definitions. | 
| No file selected for edit on RESMENU | I |The user must enter a C or E to enable creating/updating the Resource Monitor definitions. | 
| No files selected for restore	| I	| There were no files selected on SMARESTORE, so no backup files were copied as production files. |
| No mix entries found for this LSAM instance | I | The user inquired into the STATUS and no processes associated with this LSAM instance were found to be active. |
| Optional modules configuration saved | I | Changes made on the Optional Modules screen have been saved. |
| Please enter template filename | E | The user elected to edit or create a job-specific or template displays definitions file but failed to enter the name of this file. |
| Please select a valid Choice or Action | E |The Main Menu screen was transmitted but no valid entry was made in the Action or Choice fields. |
| Processing variables configuration saved | | Changes made on the Processing Variables screen have been saved. |
| Resource Monitor is included in LSAM WFL | E | The user attempted to start the Resource Monitor using INITRM option and the Resource Monitor is configured to be included within the WFL that starts the LSAM. Use INITLSAM to start both the LSAM and Resource Monitor. Alternatively, you can use the General Configuration screen to elect NOT to include the Resource Monitor within the LSAM WFL. |
| Resource Monitor submitted for start | I | The user has defined the necessary fields to start the Resource Monitor and requested this WFL be started (INITRM). Use the STATUS screen to confirm a successful initialization. |
| Resource Monitor was instructed to load file definitions | I | The user has requested that the Resource Monitor and File Monitor reload the file monitor definitions. Each file definition in the new file will be analyzed and acted upon if the specified condition occurs. |
| Resource Monitor was instructed to load resource definitions | I | The user has requested that the Resource Monitor and reload the performance monitor definitions. Each resource definition in the new file will be analyzed and acted upon if the specified condition occurs. |
| Resource Monitor was instructed to load display defs | I | The user has requested that the Resource Monitor and reload the system message definitions. |
| Resource Monitor was instructed to stop | I | The user has requested that the Resource Monitor be stopped (STOPRM). The Resource Monitor must be stopped independently of the LSAM regardless of how it was initiated (with the LSAM or without). |
| Start was not selected | I | The user visited the INITLSAM or INITRM screens and exited the screen without placing an "X" in the field to start the process. |
| This instance of the LSAM is not active | E | The user submitted a screen that is used to act upon the LSAM but the LSAM is not active (INITDEBUG, STATUS, STOPDEBUG, STOPLSAM). |
| This instance of Resource Monitor is not active	| E | The user submitted the STOPRM screen, but the Resource Monitor is not active. |
| Too many config files selected | E | The user selected multiple LSAM config backup files to restore. Only one file of each type may be selected. | 
| Too many File Monitor files selected | E | The user selected multiple File Monitor definitions backup files to restore. Only one file of each type may be selected. | 
| Too many Global Displays files selected	| E | The user selected multiple Global Displays backup files to restore. Only one file of each type may be selected. |
| Too many Performance Monitor files selected | E | The user selected multiple Performance Monitor definitions backup files to restore. Only one file of each type may be selected. |
| Too many System Displays files selected | E | The user selected multiple System Displays backup files to restore. Only one file of each type may be selected. |
| Use GEN option to configure required information | E | The user attempted to start the LSAM using the INITLSAM screen but required data has not been configured on the GEN screen, or the user attempted to start the Resource Monitor using the INITRM screen but required data has not been configured on the GEN screen. |