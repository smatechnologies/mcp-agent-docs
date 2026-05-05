---
title: General LSAM Configuration (GEN)
description: "Configure the WFL startup parameters for the MCP Agent and Resource Monitor, including usercodes, disk families, and OpCon external event credentials."
tags:
  - Reference
  - System Administrator
  - Agents
  - System Configuration
---

# General LSAM Configuration (GEN)

## What is it?

The General LSAM Configuration screen defines the MCP queue, usercode, accesscode, and disk family settings used to build the WFL that starts the MCP Agent and optionally the Resource Monitor. It also stores the OpCon user ID and external token required for sending external events to the OpCon server.

- Configure separate WFL parameters for the MCP Agent and Resource Monitor when you want to stop the Agent independently while keeping the Resource Monitor running.
- Set the OpCon user and external token to establish default credentials for external events sent by the MCP Agent.

The General LSAM Configuration (GEN) screen configures the information needed to create a WFL that starts the agent and optionally the Resource Monitor. This WFL is not stored on your system; it is created from the configuration fields when you select the INITLSAM and/or INITRM screens. This screen also configures the userid and external token for external events when you want to set default values for these credentials.

SMA Configuration and Operations Manager: SMAGEN

![SMAGEN](../../../static/img/smagen.png)

*MCP General LSAM Configuration*

| Field | Description |
| ----- | ----------- |
| **LSAM WFL Parameters** | |	 
| MCP Queue for WFL that starts the LSAM | This field defines the MCP QUEUE used to start the agent (and Resource Monitor if it is to be initiated along with the agent). |
| Usercode to start the LSAM | This field defines the MCP usercode under which the agent starts. This should be the same usercode that was used to install or upgrade the agent. |
| Password for Usercode to start the LSAM | This field defines the password associated with the MCP usercode under which the agent starts. |
| Accesscode to start the LSAM | This field defines the ACCESSCODE under which the agent starts. |
| Password for the Accesscode used to start the LSAM | This field defines the password associated with the ACCESSCODE under which the agent starts. |
| FAMILY DISK =	| This field defines the primary family to be used by the MCP Agent. It should be the same as the primary family associated with the USERCODE above. |
| OTHERWISE | This field defines the secondary family to be used by the MCP Agent. If there is no secondary family, leave this field blank. | 
| Include Resource Monitor in same WFL? | This field specifies that a single WFL should be used to initiate both the agent and the SMA/RESOURCE/MONITOR. When you combine these, a single option (INITLSAM) starts both the agent and Resource Monitor. If you want to keep the Resource Monitor separate from the agent so that you can stop the agent while allowing the Resource Monitor to continue monitoring system entities, enter an "N" in this field and define values for the Resource Monitor WFL Parameters. |
| **Resource Monitor WFL Parameters (if not included with LSAM WFL)** | |
| MCP Queue for Resource Monitor WFL | This field defines the MCP QUEUE used to start the MCP Resource Monitor if it is not to be initiated along with the agent. |
| Usercode to start the Resource Monitor | This field defines the MCP usercode under which the MCP Resource Monitor starts. This should be the same usercode that was used to install or upgrade the agent. |
| Password for Usercode to start the Resource Monitor | This field defines the password associated with the MCP usercode under which the Resource Monitor should be started. |
| Accesscode to start the Resource Monitor | This field defines the ACCESSCODE under which the Resource Monitor should be started. |
| Password for the Accesscode used to start the Resource Monitor | This field defines the password associated with the ACCESSCODE under which the Resource Monitor should be started. |
| FAMILY DISK =	| This field defines the primary family to be used by the MCP Resource Monitor. It should be the same as the primary family associated with the USERCODE above. |
| OTHERWISE	| This field defines the secondary family to be used by the MCP Resource Monitor. If there is no secondary family, leave this field blank. |
| **Authentication in OpCon Server** | |
| OpCon user | This field defines the OpCon userid to be used with external events. It must also be defined within the OpCon database. |
| OpCon External Token | This field defines the external token associated with the OpCon User. |
| Place an 'X' here to submit this screen and return to the Main Menu | To save changes, place an 'X' in this field. To discard changes or if you accessed this screen only to view the current values, leave this field blank and transmit the screen to return to the main menu. |

:::info Note

All password fields on the SMAGEN screen are masked.

:::