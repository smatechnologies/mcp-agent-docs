# Dynamic LSAM Configuration

For all LSAM configuration variables, except 'Max number concurrent jobs', changes made to the LSAM configuration file may be applied while the LSAM is active. To apply the changes, you must select LOADCFG from the Main Menu of \*SMA/MANAGER/xxx. If any of the Optional Modules were not started when the LSAM was initiated, or have been stopped, and they have since been activated in the LSAM's configuration file, select LOADCFG from the Main Menu of \*SMA/MANAGER to initiate them. However, if you initiated one of those Optional Modules with the LSAM and have since deactivated it within the LSAM configuration file, the current execution of that module will not be stopped. It simply will not be initiated by the LSAM the next time the LSAM is started.

:::info Note

Changes to the 'Max number concurrent jobs' value will NOT be implemented while the LSAM is active.

:::

All modules unconditionally note within their respective log files that an update to the configuration values has been requested. If the update was unsuccessful, this is also noted within the log by one of the following messages:

* Unable to update configuration.
* Config values not updated.
* Unable to update using new config file.
* Unable to refresh configuration values: ```<name of configuration file>```.
* In addition to the log entry, the message, "CONFIG requested ACCEPTED", will be displayed upon the system console.

To view the previous information, refer to [Dynamic LSAM Configuration](../../reference-information/legacy#dynamic-lsam-configuration) in the Legacy Information topic.