# File Monitor Messages

The table contains error messages that may be encountered in the \*SMA/FILE/MONITOR```<forward slash (/) and optional LSAM identifier>``` printer backup file.

| Message | Type | Description |
| ------- | ---- | ----------- | 
| A comma must separate file name & condition | F | There is no comma between the file title and file condition for which to monitor. |
| A period(.) must follow file title | F | There is no period (.) following the file title. |
| Accumulation value must be AVG, SUM, or blank | P	| If using an accumulation method for performance monitoring, the accumulation value must be AVG or SUM. If an accumulation method is not being used, the value  must be blank. |
| End time is required if using start time | P | If you specify a time to stop monitoring, you must also specify a time to start monitoring. |
| End time must be < 2400 | P | The latest time to stop monitoring is 2359. |
| Family name length exceeds maximum length | F	| Either there is no period following the file title, or the family name is longer than 18 characters. |
| File title length exceeds maximum length | F | The file title exceeds 63 characters in length, leaving insufficient room for the file condition. |
| Invalid comparison - use EQ,GE,GT,LE,LT,NE | P | Either the comparison was not specified, or an invalid mnemonic was used. |
| Invalid MCP command in 'M' record | P | The MCP command must be one of the following: <br></br> - CHANGE TO <br></br> - COPY AS <br></br> - DISPLAY <br></br> - REMOVE |
| Invalid metric | P | Refer to the list of permitted CPU and disk space monitoring metrics under Performance Monitor. |
| Invalid metric type - use 'U' or 'DU |'P | The only supported metric type are 'U' (CPU usage) and 'DU' (diskspace usage). |
| Invalid token: ```<token name>``` | P | The literal following the string 'Token:' is not a recognized token name; check the spelling and capitalization. |
| May use '=' or '?', but not both | F | You may not mix '=' and '?' in the same file definition ('F') record. |
| No 'A' or 'S' rec for prev definition rec | D | There are two or more consecutive definition ('D') records, but no action associated with the first one. Define at least one action record ('A' or 'S') for each definition ('D') record. |
| No 'M' or 'S' rec for prev definition rec | P | There are two or more consecutive definition ('D') records, but no action associated with the first one. Define at least one action record ('M' or 'S') for each definition ('D') record. |
| No 'M' or 'S' rec for previous file 'F' rec | F | There are two or more consecutive definition ('F') records, but no action associated with the first one. Define at least one action record ('M' or 'S') for each file definition ('F') record. |
| No equals signs (=) found | D | Message tokens are defined using '#Mn=', where 'n' is a number. Thus, at least one '=' is expected. |
| No message tokens (#M) defined | D | Message tokens are defined using '#Mn='. This string was not found in the 'D' record. |
| No target value specified | P | Either the target value is not specified, or there is an incorrect placement of commas. |
| Number of samples is required for AVG or SUM | P | If using an accumulation method for computing performance statistics, you must specify the number of samples to be taken (1 - 100). |
| Number of samples must be >0 and <= 100 | P | The number of samples specified was 0. |
| Sam message must start with dollar sign ($) | D,F,P | OpCon external events must start with a dollar sign ($). |
| Start time must be less than end time | P | A single performance monitor may not span midnight. Create two entries: one to start at the specified start time and end at 2359; the other to start at 0001 and end at the specified end time. |
| Too many commas | P | The definition ('D') record contains too many commas. Correct the syntax. |
| Unable to unstring family name | F | The family name could not be located in the file ('F') record. Check the syntax. |
| Unable to unstring file condition | F | The file condition could not be located in the file ('F') record. Check the syntax. |
| Unable to unstring file name. Correct input | F | The file name could not be located in the file ('F') record. Check the syntax. |
| Use commas to delimit values | P | No commas were found in the definition ('D') record. Commas are used to separate components of the definition. Refer to Performance Monitor discussion. |
| Use file title, including 'on ```<familyname>``` | 'F | The file title is missing a usercode or familyname specification. |
| Use ```<FILE>``` or full file title | F | The REMOVE, CHANGE TO, or COPY AS command does not use the full file title. You may substitute the token ```<FILE>``` for the file title of the monitored file. |
| Use: PRESENT, ALTERED, DELETED, or WARN=## | F | The file condition for which to monitor is not recognizable. |
| Warn= percentage must be 2 digits long, > 0 | F | The WARN= file condition was specified, but the percentage is 0. |
