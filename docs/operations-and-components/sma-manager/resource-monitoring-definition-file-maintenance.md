# Resource Monitoring Definition File Maintenance

## Resource Monitoring Definition File Maintenance Main Menu (RESMENU)


Use this screen to select whether to create the initial resource monitoring definitions file, or to edit an existing resource monitoring definitions file.

The resource monitoring definitions file is used by the Resource Monitor to capture system metrics specified within this file. The Resource Monitor then performs the actions defined for that system metric and condition. 

Use "C" or "E" to indicate whether you want to Create or Edit the definitions file.

###### SMA Configuration and Operations Manager: SMARESMENU

![SMARESMENU](../../../static/img/smaresmenu.png)

## Resource Monitoring Definition File Maintenance (RELIST)

Use this screen to modify records within the resource monitoring definitions file.

###### SMA Configuration and Operations Manager: SMARESLIST

![SMARESLIST](../../../static/img/smareslist.png)

There are various navigation paths you can take from this screen, depending on the value in the Action field:

* HOme: This will take you directly to the Manager Main Menu without processing any of the changes you may have entered.
* NExt: This will process the changes you have made on this page and then display the next eight records in the definitions file.
* BAck: This will process the changes you have made on this page and then display the previous eight records in the definitions file.
* PArent: This will take you directly to the SAVERES screen where you will have the opportunity to elect to permanently save the changes you may have entered.
* REfresh: This will redisplay the original values from the previous presentation of this screen without processing any of the changes you may have entered. This Action is useful if you want to discard all changes you have made on this screen and want to start over.

Errors will be displayed in the status field at the bottom of the screen. If there are no errors, the changes will be temporarily saved.

## MCP LSAM Configuration Settings: Resource Monitoring Definition File Maintenance (RESLIST)

### D/E/I

This field is the action you want to perform on a given record.

* If D, delete the record at this sequence number in the file.
* If E, edit the record at this sequence number in the file.
* If I, insert a record at this sequence number in the file. You must also enter a sequence number that falls between the previous record and the next record in the file.

### D/M/S/%/*

This field is the record type.

* If D, the record type is the metric and condition for which to monitor.
* If M, the record type is an action that is to take place on the MCP platform.
* If S, the record type is the external event that is to be sent to the OpCon server for processing. All external events must begin with a dollar sign ($). Possible external OpCon events are documented in [External Events](https://help.smatechnologies.com/opcon/core/events/defining#external-events) in the OpCon Events online help.
* % and \* are used to denote that this is a comment. This is useful when you want to temporarily disable a definition or action, but do not want to permanently delete it from the file, or when you want to add an explanation.

### SEQ #

This is the sequence number associated with this record in the definitions file. To modify or delete an existing record, leave the sequence number field as is. To insert a new record in the definitions file, enter an 8-digit sequence number that falls between the previous record and the next record. If you are on the last page and want to add records to the end of the file, simply enter sequence numbers that are successively greater than the last existing record’s sequence number.

:::info Note

The long field below the action, type, and sequence line is used to define the file, condition, and optional start and end times for which to monitor or the action to take or to add a comment. Refer to the detailed description in the [Performance Monitor Data File](../../additional-features/lsam-features/resource-monitor#performance-monitor-data-file) section for more information about each record type and how to construct the data in this field.

:::

## Save Resource Monitor Definitions Changes (SAVERES)

Use this screen to permanently save the Resource Monitor definition changes. The definitions file will be re-sequenced as part of the save.

###### SMA Configuration and Operations Manager: SMASAVERES

![SMASAVERES](../../../static/img/smasaveres.png)