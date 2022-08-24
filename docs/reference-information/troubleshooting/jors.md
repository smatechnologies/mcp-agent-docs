# Job Output Retrieval System (JORS)

## No Output File

#### Full Description

"No output file" is the response to "View Print File".
 
#### First Possible Explanation:
 
There are no print files for the job.

##### First Operator Response:

No action is necessary.

#### Second Possible Explanation:
 
The \*SMA/JORS/xxx module is unable to detect the print files.

##### Second Operator Response:

If the family on which print files is located is absent from the FAMILY statement of the usercode under which the LSAM started:

1. DS the \*SMA/JORS/xxx module.

2. Initiate \*SMA/JORS/xxx using a WFL started under a usercode that has access to the print family. For more information on this response, refer to \*[SMA/JORS](/operations-and-components/optional-programs-and-files#smajors-associated-files).
 
## JORS not Working

#### Full Description

JORS is not running.
 
#### Possible Explanation:
 
"Neither JORS nor outgoing File Transfer is configured – terminating" is displayed on the console. If neither JORS nor the outgoing file transfers have been enabled in the LSAM's configuration file and the user attempts to initiate *SMA/JORS in lieu of having the LSAM initiate JORS, the message above will be displayed on the system console.

##### Operator Response:

Configure JORS in the LSAM's configuration file. For more information on configuring JORS in the LSAM's configuration file, refer to [Configure JORS in the LSAM Configuration](/additional-features/lsam-features/jors#configure-jors-in-the-lsam-configuration).