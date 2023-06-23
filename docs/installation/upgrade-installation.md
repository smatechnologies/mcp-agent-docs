# Upgrade Installation

If you wish to perform an upgrade installation of the MCP LSAM, then follow the procedures provided in this section.

## Complete Job and Event Processing

If performing an upgrade, complete the following procedure to allow all active jobs to complete and/or outstanding external events to be processed by the LSAM.

1. Under the Operation topic, double-click on Machine Status below the Navigation tab on the Enterprise Manager screen.

2. Confirm the number of Running Jobs is 0 for the MCP machine.

3. Wait approximately two minutes to allow any outstanding external events to be forwarded to the SAM and supporting services.

:::caution

Any external events which are generated after the machine is marked down and before the new version of the LSAM is up and running may be lost. This depends on the current version of the LSAM and depends on the changes in structure of the file in which these events are stored (prior to being forwarded to the SAM and supporting services).

:::

4. Right-click on the Machine name then click Stop Communication.

5. Check the current LSAM version:

    a. From the Home position of the LSAM window, type VERSION. Transmit the line -or-
    
    b. For LSAM version 18.00.00 and up, perform the STATUS inquiry form the Main Menu of the SMA/MANAGER program. The RELEASEID is displayed on the STATUS screen.
    
    c. Take note of the version for reference during the upgrade installation.

## Stop the LSAM and Resource Monitor

:::info Note 

Please allow up to five minutes for the components to shut themselves down.

:::

1. Access *SMA/MANAGER via ?ON SMAMGRxxx.

2. From the Main Menu, select STOPLSAM.

3. From the Main Menu, select STOPRM, if the Resource Monitor is active.

To view the previous procedure, refer to [Stop the LSAM and Resource Monitor](../reference-information/legacy#stop-the-lsam-and-resource-monitor) in the Legacy Information topic.

## Remove Checkpoint Files and Perform Upgrade

1. Remove ```*SMA/CP/MCS/= ON <diskpack>```.

2. Use the ```*SMA/INSTALL``` program to perform the upgrade.

## Configure the LSAM

If upgrading from a version earlier than 18.00.00 to version 18.00.00 or higher, you must complete the following steps:

1. Run ```*SMA/CONFIG/xxx``` and capture a screenshot or print the configuration values.

2. Next, remove the ```*SMA/CONFIG/FILE/xxx```.

:::info Note

 This is necessary due to the various configuration file formats that have existed over multiple releases.

:::

3. Run the SMA/MANAGER program to populate the configuration file with the values you captured, as well as the additional fields prior to starting the LSAM. You will need to access all four LSAM configuration screens. For new fields, refer to the discussion of the [SMAGEN (GEN option)](../configuration/general-lsam-configuration) in the MCP LSAM Configuration to configure and operate the LSAM.

:::info Note 

For versions prior to MCP LSAM 19.01.00, it is also necessary to exit the Manager program after updating the configuration fields to save the new values. Then, you may run the Manager program to perform all other functions.

:::