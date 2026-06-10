---
title: Communication Parameters (COMM)
description: "Configure the TCP/IP port, TLS settings, hostname alias, and accepted IP addresses on the SMACOMM screen to enable LSAM-to-OpCon communication."
tags:
  - Reference
  - System Administrator
  - System Configuration
  - Agents
---

# Communication Parameters (COMM)

## What is it?

This page documents each field on the SMACOMM screen within SMA/MANAGER, which controls the network port, TLS certificate settings, idle timer, hostname alias, and the list of IP addresses from which the MCP Agent will accept connections.

- Use this page when initially connecting the MCP Agent to an OpCon server to ensure the port number, hostname, and TLS settings match the corresponding values defined in the Enterprise Manager or Solution Manager machine record.
- Use this page to restrict inbound connection requests to specific IP addresses or to configure TLS-secured scheduling communications with an appropriate certificate and key.

The Communication Parameters screen allows you to configure the information needed to communicate scheduling messages between the MCP Agent and the OpCon Server.

**SMA Configuration and Operations Manager: SMACOMM**

![SMACOMM](../../static/img/smacomm.png)

**MCP LSAM Configuration Settings: Communication Parameters**

The following table describes each field on the SMACOMM screen.

| Field | Description |
| ----- | ----------- |
| OpCon TCP/IP port number | This field defines the port number that should be used to communicate with SMANetCom. It must match the port number defined for this machine in the database. The default value is **3100**. |
| Secure using TLS? | This field defines whether to use TLS for secure communication. If you want to use TLS to secure communications, enter a Y in this field, install a certificate using Security Center, and enter the key in the "TLS Key" field. | 
| TLS Key | This field is the key associated with the certificate used to secure scheduling communications with TLS. The certificate is stored using the Unisys Security Center. |
| Allow self-signed certificates? | This field defines whether to allow self-signed certificates. If the TLS certificate is self-signed, enter a Y in this field. |
| Idle Timer | This field is a timer that instructs the MCP Agent on how often to inquire for messages between agent components and how often to see if there are messages to send to SMANetCom. The value is in seconds. The default value is **30** seconds; valid range is **1–300**. A low value means faster throughput during idle periods but increases processor usage. A high value uses less resources but can result in slower throughput during idle periods. Job start requests are not affected by this timer; however, job status updates can be affected when there is little activity initiated by SMANetCom. |
| Hostname alias | This field defines the value that corresponds to the machine name defined in Enterprise Manager or Solution Manager. If left blank, the system hostname will be used. When providing a value for this field, do not include an ending period (.); however, when defining the machine name in Enterprise Manager or Solution Manager, the trailing period (.) must be used in the Machine definition. | 
| Accept messages from IP addresses | These five fields allow you to specify from which IP addresses the MCP Agent will accept a request to connect. A maximum of five unique IP addresses may be entered. Alternatively, you may enter the value of "ALL" for the first IP address to instruct the agent to accept a connection request from any IP address. | 
| Place an 'X' here to submit this screen and return to the Main Menu | In order to save any changes you have made to this screen, you must place an 'X' in this field. If you do not want to save changes or you accessed this screen simply to inquire as to the current values, leave this field blank and transmit the screen to be returned to the main menu. |