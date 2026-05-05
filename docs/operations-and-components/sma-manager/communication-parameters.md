---
title: Communication Parameters (COMM)
description: "Configure the network and security settings the MCP Agent uses to exchange scheduling messages with the OpCon server."
tags:
  - Reference
  - System Administrator
  - Agents
  - System Configuration
---

# Communication Parameters (COMM)

## What is it?

The Communication Parameters screen configures the TCP/IP port, TLS security options, hostname alias, and accepted IP addresses that the MCP Agent uses to communicate with the OpCon server. Changes are saved by placing an X in the submit field and take effect when the Agent reloads its configuration.

- Set the OpCon TCP/IP port number and optionally enable TLS with a certificate key to secure scheduling traffic.
- Restrict inbound connection requests to up to five specific IP addresses, or allow connections from any address using the ALL value.

The Communication Parameters screen configures the information needed to communicate scheduling messages between the agent and the OpCon Server.

### SMA Configuration and Operations Manager: SMACOMM

![SMACOMM](../../../static/img/smacomm.png)

### MCP Agent Configuration Settings: Communication Parameters

The following table describes each field on the SMACOMM screen.

| Field | Description |
| ----- | ----------- |
| OpCon TCP/IP port number | This field defines the port number that should be used to communicate with SMANetCom. It must match the port number defined for this machine in the database. |
| Secure using TLS? | This field defines whether to use TLS for secure communication. If you want to use TLS to secure communications, enter a Y in this field, install a certificate using Security Center, and enter the key in the "TLS Key" field. |
| TLS Key | This field is the key associated with the certificate used to secure scheduling communications with TLS. The certificate is stored using the Unisys Security Center. |
| Allow self-signed certificates? | This field defines whether to allow self-signed certificates. If the TLS certificate is self-signed, enter a Y in this field. |
| Idle Timer | This field sets how often the agent checks for messages between agent components and how often it checks for messages to send to SMANetCom. The value is in seconds. A low value means faster throughput during idle periods but increases processor usage. A high value uses fewer resources but can result in slower throughput during idle periods. Job start requests are not affected by this timer; however, job status updates can be affected when there is little activity initiated by SMANetCom. |
| Hostname alias | This field defines the value that corresponds to the machine name defined via the Enterprise Manager. If left blank, the system hostname will be used. When providing a value for this field, do not include an ending period (.); however, when defining the machine name in the Enterprise Manager, the trailing period (.) must be used in the Machine definition. |
| Accept messages from IP addresses | These five fields specify from which IP addresses the agent will accept a request to connect. Enter a maximum of five unique IP addresses. Alternatively, enter the value "ALL" for the first IP address to instruct the agent to accept a connection request from any IP address. |
| Place an 'X' here to submit this screen and return to the Main Menu | To save changes, place an 'X' in this field. To discard changes or if you accessed this screen only to view the current values, leave this field blank and transmit the screen to return to the main menu. |