---
title: File Arrival Utility
description: "A command-line alternative to the OpCon File Arrival job type for detecting files on the MCP platform within a specified time frame."
tags:
  - Procedural
  - Automation Engineer
  - Agents
---

# File Arrival Utility

## What is it?

The MCP File Arrival utility detects whether a file has been created on the MCP platform within a specified time frame on the date the utility runs, then sets an OpCon property to the value of the file title when a matching file is found. It consists of the WFL \*SMA/WFL/FILEARRIVAL and the program \*SMA/OBJ/FILEARRIVAL, and depends on a valid installation of the MCP Agent.

- Detect a file arrival within a configurable time window and report the file title via an OpCon property
- Use as a batch alternative to the OpCon File Arrival job type for MCP platform workflows

## Overview

The WFL \*SMA/WFL/FILEARRIVAL and the program \*SMA/OBJ/FILEARRIVAL make up the utility. The WFL uses \*SMA/EVENTGEN to construct a ```$PROPERTY:SET``` event. The File Arrival program calls the SEARCH_MIX_OR_FILES API within the \*SMA/ALGOLPROCS library, making this utility dependent upon a valid installation of the MCP Agent.

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
 
If running this utility within a unique instance of the MCP Agent, modify the RUN statements for \*SMA/OBJ/FILEARRIVAL and \*SMA/EVENTGEN to reflect the unique instance name.
 
Define an MCP Job to start the \*SMA/WFL/FILEARRIVAL utility. There are four parameters defined:

* **Parameter 1**: The full file title of the file to be interrogated. Wildcarding is supported for the purpose of masking unknown portions of the file name. Only a single file title will be returned, even if multiple files meet the criteria.
* **Parameter 2**: The earliest acceptable ALTERTIME of the file. Currently, the date will still have to match the date the job is run.
* **Parameter 3**: The latest acceptable ALTERTIME of the file. Currently, the date will still have to match the date the job is run.
* **Parameter 4**: The name of the user-defined OpCon property to be populated with the file title of the file.

During this initial testing phase, it is not actually necessary to set up anything in OpCon because there are quite a few displays that show the status of the job and the PROPERTY:SET event.
 