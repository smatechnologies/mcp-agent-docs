# Update the "Max Number Concurrent Jobs" Field

If the "Max number concurrent jobs" configuration variable is changed, it is necessary to remove the LSAM's checkpoint files and tracking file before restarting the LSAM. Refer to [MCP Known Issues](/reference-information/mcp-known-issues) concerning a Known Issue about the "Max number concurrent jobs" field and startup errors.

## Remove Checkpoint and Tracking Files

1. Determine whether jobs were active the last time the LSAM was stopped. If jobs were active, start the LSAM to allow recovery to take place and the active jobs to complete.
2. Stop the LSAM. For instructions on stopping the LSAM, refer to [Stop the LSAM](/operations-and-components/sma-manager/initiate-the-lsam#stop-the-lsam-stoplsam).
3. Modify the configuration file to reflect the desired "Max number of concurrent jobs." For more information on configuration, refer to [Max number concurrent jobs](/configuration/processing-variables#max-number-concurrent-jobs).
4. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/CP/MCS/xxx/=. Transmit the line.
5. From the Action line of MARC, the ODT, or the home position of CANDE, type: REMOVE*SMA/TRACKING/FILE/xxx. Transmit the line.
6. Start the LSAM. For instructions on starting the LSAM, refer to [MCP LSAM Operation](/operations-and-components/mcp-lsam-operation).