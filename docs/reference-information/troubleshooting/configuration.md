# Configuration Troubleshooting

## Insufficient Screen Size

#### Full Description

"Insufficient screen size" error occurs when starting the \*SMA/CONFIG/xxx program.
 
#### Possible Explanation:
 
The default screen size is less than 1,920 characters.

##### Operator Response:

Modify the screen size to at least 1,920 characters. For more information on this response, refer to [Run the Manager Program](../../configuration/configuration-settings#run-the-manager-program).
 
## Configuration Changes not Applied

#### Full Description

Configuration changes were not applied.
 
#### First Possible Explanation:
 
While running the \*SMA/CONFIG/xxx program, the operator performed an (I)nquiry following a (M)odification.

##### First Operator Response:
An (I)nquiry refreshes the screen with the saved configuration file. Following modifications, (Q)uit the \*SMA/CONFIG```<forward slash (/) and optional LSAM identifier>``` program and rerun the program to confirm changes. The (P)rint option may also be used to print a report of the modified file. For more information on this response, refer to [Run the Manager Program](../../configuration/configuration-settings#run-the-manager-program).
OpenSecond Possible Explanation:
 
The modified \*SMA/CONFIG/FILE/xxx is not present under the same usercode used to start the LSAM.
Second Operator Response:
Copy the modified \*SMA/CONFIG/FILE/xxx under the appropriate usercode. For more information on this response, refer to \*[SMA/CONFIG](../../operations-and-components/core-programs-and-files#smaconfig).
 
## Config File is Too Short

#### Full Description

Config file is too short - Use SMA/MANAGER to update config file.
 
#### First Possible Explanation:
 
If the user attempts to use a config file that is less than seven records, the Algolprocs library will unconditionally log an error in the debug log and exit.