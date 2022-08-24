# File Arrival Utility

## Overview

The MCP File Arrival utility has been created as a command-line alternative to implementing an OpCon File Arrival job for MCP. The utility is intended to serve the purpose of detecting a file on the MCP platform that has been created within a specified time frame on the date the utility is run. The time frame parameters are optional. Upon detecting a file meeting the criteria, a property will be set to the value of the MCP file title.
 
This utility consists of a WFL \*SMA/WFL/FILEARRIVAL and a program \*SMA/OBJ/FILEARRIVAL. The WFL utilizes \*SMA/EVENTGEN to construct a ```$PROPERTY:SET``` event. The File Arrival program calls the SEARCH_MIX_OR_FILES API within the \*SMA/ALGOLPROCS library, making this utility dependent upon a valid installation of the MCP Agent.

## Initial Requirements

The following are initial requirements for File Arrival jobs on the MCP Agent platform:

* The job will stay running during the determined duration if the file is not present.
* If the file appears during the determined duration, the job will Finish OK.
* If the file arrived before the job has started, but after the determined time window, the job will Finish OK.
* If the file is not present by the end of the determined duration, the job will fail.
* If the file is arrived before the determined time window, the job will not detect it.
 
:::info Note 

The initial requirement for a time to wait for the file to achieve a stable size is not applicable to the MCP platform.

:::

## Required Parameters

* File Title (File name and Family)
* Start Window
* End Window
* Name of property to set to title of found file

## Post Processing Requirements

A ```$PROPERTY:SET``` supporting each of the ```$FILEARRIVED``` properties needs to be able to be sent:

* ```$ARRIVED BASE FILE NAME```: The last node of the File Title.
* ```$ARRIVED FILE NAME```: The full file name without the family name.
* ```$ARRIVED FILE PATH```: The directory without the File Name. (Last node)
* ```% < Add a JI Property Explanation Here>```


:::info Note

The alternative to complying with the above post-processing requirement is to accept a fourth WFL parameter which contains the name of OpCon property to be set to the full file title of the file found.

If no file is found, the property will be set to null (if supported).

:::

## Using the File Arrival Utility

Create a property within OpCon to be used to contain the file title of the file which meets the specified criteria.
 
If running this utility within a unique instance of the MCP LSAM, modify the RUN statements for \*SMA/OBJ/FILEARRIVAL and \*SMA/EVENTGEN to reflect the unique instance name.
 
Define an MCP Job to start the \*SMA/WFL/FILEARRIVAL utility. There are four parameters defined:

* **Parameter 1**: The full file title of the file to be interrogated. Wildcarding is supported for the purpose of masking unknown portions of the file name. Only a single file title will be returned, even if multiple files meet the criteria.
* **Parameter 2**: The earliest acceptable ALTERTIME of the file. Currently, the date will still have to match the date the job is run.
* **Parameter 3**: The latest acceptable ALTERTIME of the file. Currently, the date will still have to match the date the job is run.
* **Parameter 4**: The name of the user-defined OpCon property to be populated with the file title of the file.

During this initial testing phase, it is not actually necessary to set up anything in OpCon because there are quite a few displays that show the status of the job and the PROPERTY:SET event.
 