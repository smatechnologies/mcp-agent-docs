# Restore Configuration and Definitions Files (RESTORE)

Each time the SMA/MANAGER program is initiated, it automatically backs up all configuration files used by the LSAM: the LSAM configuration file, global displays definitions file, system message definitions file, file monitor definitions file, and performance monitor definitions file. Files are named by appending the date and time of the backup to the file name, making it easy to identify when the file was backed up.

To restore a production configuration file from a recent backup, select the RESTORE option from the Manager Main Menu. Prior to presentation of the SMARESTORE screen, the Manager program will remove backup files in excess of 20 per type of file. Up to three files of each type are presented on the SMARESTORE screen. You may select only one file of each type; however, you may restore multiple types of files at one time. After you restore the file, you must notify the LSAM that the file has been restored. To do this, use the LOADCFG, LOADDISP, LOADFILE, and LOADPERF Main Menu choices as appropriate.

### SMA Configuration and Operations Manager: SMARESTORE

![SMARESTORE](/img/smarestore.png)