# File Monitoring Definition File Maintenance

## File Monitoring Definition File Maintenance Main Menu (FILEMENU)

Use this screen to select whether to create the initial file monitoring definitions file or to edit an existing file monitoring definitions file.

The file monitoring definitions file is used by the Resource Monitor to capture file events for files specified within this file. The File Monitor then performs the actions defined for that file condition.

Use "C" or "E" to indicate whether you want to Create or Edit the definitions file.

###### SMA Configuration and Operations Manager: SMAFILEMENU

![SMAFILEMENU](../../../static/img/smafilemenu.png)

## File Monitoring Definition File Maintenance (FILELIST)

Use this screen to modify records within the file monitoring definitions file.

###### SMA Configuration and Operations Manager: SMAFILELIST

![SMAFILELIST](../../../static/img/smafilelist.png)

There are various navigation paths you can take from this screen, depending on the value in the Action field:

* HOme: This will take you directly to the Manager Main Menu without processing any of the changes you may have entered.
* NExt: This will process the changes you have made on this page and then display the next 8 records in the definitions file.
* BAck: This will process the changes you have made on this page and then display the previous 8 records in the definitions file.
* PArent: This will take you directly to the SAVEFILE screen where you will have the opportunity to elect to permanently save the changes you may have entered.
* REfresh: This will redisplay the original values from the previous presentation of this screen, without processing any of the changes you may have entered. This Action is useful if you want to discard all changes you have made on this screen and want to start over.

Errors will be displayed in the status field at the bottom of the screen. If there are no errors, the changes will be temporarily saved.

## MCP LSAM Configuration Settings: File Monitoring Definition File Maintenance (FILELIST)

### D/E/I

This field is the action you want to perform on a given record.

* If D, delete the record at this sequence number in the file.
* If E, edit the record at this sequence number in the file.
* If I, insert a record at this sequence number in the file. You must also enter a sequence number that falls between the previous record and the next record in the file.

### F/F2/F-/M/S/S-/%/*

This field is the record type.

* If F, the record type is the file title (with or without wildcards) that identifies the target file(s) and condition for which to monitor.
* If F-, the record type is used as a continuation of the F record, in the case where 70 characters is insufficient to fully define the file title and condition for which to monitor.
* If F2, the record type is used to define the start and end time during which to monitor for the file condition.
* If M, the record type is an action that is to take place on the MCP platform.
* If S, the record type is the external event that is to be sent to the OpCon server for processing. All external events must begin with a dollar sign ($).
* S- is used when the external event is longer than 70 characters.
    * Use S for the first part of the event (include $).
    * Use S- for the latter part of the event (no $).
    * Possible external OpCon events are documented in [External Events](https://help.smatechnologies.com/opcon/core/events/defining#external-events) in the OpCon Events online help.
* % and * are used to denote that this is a comment. This is useful when you want to temporarily disable a definition or action but do not want to permanently delete it from the file, or when you want to add an explanation.

### SEQ #

This is the sequence number associated with this record in the definitions file. To modify or delete an existing record, leave the sequence number field as is. To insert a new record in the definitions file, enter an 8-digit sequence number that falls between the previous record and the next record. If you are on the last page and want to add records to the end of the file, simply enter sequence numbers that are successively greater than the last existing record's sequence number.

:::info Note

The long field below the action, type, and sequence line is used to define the file, condition, and optional start and end times for which to monitor or the action to take or to add a comment. Refer to the detailed description in the [File Monitor Data](../../additional-features/lsam-features/file-monitor#file-monitor-data-file) File topic for more information about each record type and how to construct the data in this field.

:::

## Save File Monitoring Definition Changes (SAVEFILE)

Use this screen to permanently save the file monitoring definitions changes. The definitions file will be re-sequenced as part of the save.

###### SMA Configuration and Operations Manager: SMASAVEFILE

![SMASAVEFILE](../../../static/img/smasavefile.png)