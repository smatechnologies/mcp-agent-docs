# MCP LSAM Configuration

The LSAM configuration file contains information needed to set the correct options for LSAM communication with SMANetCom and to activate optional features. After installation of the LSAM, the configuration file should be reviewed before the LSAM is started.

:::info Note 

If upgrading to MCP LSAM 18.00.00 or higher from a version earlier than 18.00.00, you MUST access the SMAMGR window to update the new configuration fields on the GEN screen.
 
:::


:::info Note 

The configuration file must reside on the same family and under the same usercode as the LSAM.

:::

* The following settings are critical to the operation of the LSAM with OpCon:
    * OpCon port: This value is used for communication between the LSAM and the SMANetCom. The value for this setting and the value for the Socket Number on the Machines screen in the Enterprise Manager must match.
    * Hostname alias: The default value of ```<None>``` for the hostname causes the LSAM to automatically look up and use the BNA hostname. The BNA hostname (or a configured hostname alias) is required when setting up the Machine in the Enterprise Manager. The BNA hostname is displayed when the SYSTEM user is logged on to the MARC Main Menu screen. At the bottom of the window, there is a string with the following syntax: Window MARC/```<window number>``` at ```<hostname>```. Make note of the hostname for use in the Enterprise Manager if you are not supplying a hostname alias.
    * Max number concurrent jobs: This value determines the maximum number of jobs the LSAM is allowed to process concurrently. The maximum allowed value is 500.