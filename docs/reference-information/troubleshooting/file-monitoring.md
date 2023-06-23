# File Monitoring Troubleshooting

## Event not Sent

#### Full Description

Event is not sent to the Schedule Activity Monitor (SAM).
 
#### First Possible Explanation:
 
The Resource Monitor WFL was started from the ODT. In order for Resource/File Monitor to monitor files, the WFL must be started from a MARC or CANDE session into which the user has logged on with a privileged usercode.

##### First Operator Response:

Start the WFL under a MARC/CANDE session with an authentic, privileged usercode.

#### Second Possible Explanation:
 
The \*SMA/RESOURCE/MONITOR/xxx program itself must be privileged.

##### Second Operator Response:

Make the \*SMA/RESOURCE/MONITOR/xxx program privileged:
MP \*SMA/RESOURCE/MONITOR/xxx ON ```<packname>``` + PU
For more information on this response, refer to [Resource Monitor](../../additional-features/lsam-features/resource-monitor).

#### Third Possible Explanation:
 
The Resource and File monitors have had insufficient time to detect/process a change in the status of the monitored file.

##### Third Operator Response:

Wait.
For more information on this response, refer to [Run the Manager Program](../../configuration/configuration-settings#run-the-manager-program).

#### Fourth Possible Explanation:
 
In MCP LSAM versions prior to 04.14.02, there were instances in which file creations and deletions were not recognized. This issue was corrected in MCP LSAM version 04.14.02.

##### Fourth Operator Response:

Upgrade to MCP LSAM version 04.14.02 or higher.
 
## Changes to File Monitor Rules not Applied

#### Full Description

Changes to \*SMA/FILEMON/DEFS/xxx were not applied.
 
#### Possible Explanation:
 
The \*SMA/FILEMON/DEFS/xxx file was modified, but the *SMA/RESOURCE/MONITOR/xxx and/or *SMA/FILE/MONITOR/xxx programs were not notified of the changes.

##### Operator Response:

After making modifications to the \*SMA/FILEMON/DEFS/xxx file, copy it under the LSAM's usercode and deliver an "AX FILEMON" to the \*SMA/RESOURCE/MONITOR/xxx program. For more information on this response, refer to [File Monitor](../../additional-features/lsam-features/file-monitor).
 
## Files not Monitored

#### Full Description

Some files are not being monitored as defined.
 
#### Possible Explanation:
 
A logic error within \*SMA/RESOURCE/MONITOR/xxx caused corruption of family names if the family name was longer then 5 characters.

##### Operator Response:

Upgrade to MCP LSAM version 04.14.00 or higher.