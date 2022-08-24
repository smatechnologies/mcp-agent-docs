# General LSAM Congfiguration (GEN)

The General LSAM Configuration screen allows the user to configure the information needed to create a WFL that will start the LSAM and optionally also the Resource Monitor. 

This WFL is not stored on the user's system but rather is created using the configuration fields when the user selects the INITLSAM and/or INITRM screens. 

This screen is also used to configure the userid and external token for external events, if the user wishes to set up default values for these credentials.

###### SMA Configuration and Operations Manager: SMAGEN

![SMAGEN](/img/smagen.png)

###### MCP General LSAM Configuration

| Field | Description |
| ----- | ----------- |
| LSAM WFL Parameters | MCP Queue for WFL that starts the LSAM	This field defines the MCP QUEUE that should be used to start the LSAM (and Resource Monitor if it is to be initiated along with the LSAM). |
| Usercode to start the LSAM | This field defines the MCP usercode under which the LSAM should be started. This should be the same usercode that was used to install/upgrade the LSAM. |
| Password for Usercode to start the LSAM | This field defines the password associated with the MCP usercode under which the LSAM should be started. |
| Accesscode to start the LSAM | This field defines the ACCESSCODE under which the LSAM should be started. |
| Password for the Accesscode used to start the LSAM | This field defines the password associated with the ACCESSCODE under which the LSAM should be started. | 
| FAMILY DISK = | This field defines the primary family to be used by the MCP LSAM. It should be the same as the primary family associated with the USERCODE above. |
| OTHERWISE	| This field defines the secondary family to be used by the MCP LSAM. If there is no secondary family, leave this field blank. |
| Include Resource Monitor in same WFL?	| This field is a flag that specifies that a single WFL should be used to initiate both the LSAM and the SMA/RESOURCE/MONITOR. The impact of combining these is that when the user wants to start the LSAM and Resource Monitor, a single option (INITLSAM) will accomplish this. However, if you want to keep the Resource Monitor separate from the LSAM so that you can stop the LSAM while allowing the Resource Monitor to continue to monitor the system entities, enter an "N" in this field and proceed to define values for the Resource Monitor WFL Parameters. | 
| Resource Monitor WFL Parameters (if not included with LSAM WFL) | |
| MCP Queue for Resource Monitor WFL | This field defines the MCP QUEUE that should be used to start the MCP Resource Monitor if it is not to be initiated along with the LSAM. |
| Usercode to start the Resource Monitor | This field defines the MCP usercode under which the MCP Resource Monitor should be started. This should be the same usercode that was used to install/upgrade the LSAM. |
| Password for Usercode to start the Resource Monitor | This field defines the password associated with the MCP usercode under which the Resource Monitor should be started. | 
| Accesscode to start the Resource Monitor | This field defines the ACCESSCODE under which the Resource Monitor should be started. |
| Password for the Accesscode used to start the Resource Monitor | This field defines the password associated with the ACCESSCODE under which the Resource Monitor should be started. |
| FAMILY DISK =	| This field defines the primary family to be used by the MCP Resource Monitor. It should be the same as the primary family associated with the USERCODE above. |
| OTHERWISE	| This field defines the secondary family to be used by the MCP Resource Monitor. If there is no secondary family, leave this field blank. |
| Authentication in OpCon Server | |
| OpCon user | This field defines the OpCon userid to be used with external events. It must also be defined within the OpCon database. |
| OpCon External Token | This field defines the external token associated with the OpCon User. |
Place an 'X' here to submit this screen and return to the Main Menu	| In order to save any changes you have made to this screen, you must place an 'X' in this field. If you do not want to save changes, or you had accessed this screen simply to inquire as to the current values, leave this field blank and transmit the screen to be returned to the main menu. | 

:::info Note

All password fields on the SMAGEN screen are masked.

:::