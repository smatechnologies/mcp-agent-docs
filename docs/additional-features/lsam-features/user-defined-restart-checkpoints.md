# User-defined Restart/Recovery Checkpoints

To minimize possible data loss, the MCP LSAM backs up job array and tracking information at user-specified intervals and at a normal shutdown. These periodic backups are called checkpoints. During a restart/recovery, the LSAM automatically falls back to the data in latest checkpoint.
 
User-defined checkpoint frequencies are per minute, per job array update, or never. The interval (in minutes or updates) between these checkpoints can also be defined. To update these configuration values, refer to the procedure in the related topic.
 
With this feature, consider the risk of data loss versus processing performance. More checkpoints may burden and slow processing, but improve data recovery. Fewer checkpoints may improve processing performance, but diminish data recovery. Try to balance the costs and benefits of checkpoints. If the computing environment is unstable and prone to crashes, faster processing may be traded for greater data protection. If the environment is more stable, fewer checkpoints may be desired to achieve better processing performance.

## Update the Configuration File

If User-defined Checkpoints were not defined during the installation, the configuration file must be updated.
 
Modify the following fields under [Optional Modules (OPT)](../../operations-and-components/sma-manager/optional-modules):

a. Freq

b. Interval