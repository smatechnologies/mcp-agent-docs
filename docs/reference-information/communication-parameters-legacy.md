---
title: Communication Parameters (Legacy)
description: "A reference table of legacy TCP/IP communication configuration fields for the MCP Agent and SMANetCom."
tags:
  - Reference
  - System Administrator
  - Agents
---

# Communication Parameters (Legacy)

:::caution Superseded

This page documents the legacy \*SMA/CONFIG configuration format. Use [Communication Parameters (COMM)](../configuration/communication-parameters) for current configuration guidance using SMA/MANAGER.

:::

| Field | Default | Valid Values | Description |
| ----- | ------- | ------------ | ----------- |
| OpCon port | 03100 | 0 – 65535 | This field specifies the TCP/IP port number that will be used for communication between the agent and SMANetCom. |
| Secure? | N | N | This field specifies whether communications with the SAM-SS are to be secured using TLS. |
| Key | SMALSAM | Any valid sockets key | This configuration variable must correspond to a Sockets Key defined in the Trusted Keys store of MCP Cryptographic Services. A valid certificate is also required. <br></br><br></br> - Use MCP Cryptographic Services to create a Sockets Key, associate it with the usercode under which you will run the MCP Agent, and generate a certificate request. Once a signed certificate has been received, install it for this key. <br></br> - The same key may be used for multiple instances of the MCP Agent. |
| Allow self-signed certificates? | N | - Y <br></br> - N | This field specifies whether to allow the use of self-signed certificates in the scheduling and View Job Output (JORS) TLS protocols. |
| Idle timer | 030 | 1 – 300 | This field defines the number of seconds the agent processes wait before checking for incoming messages from SMANetCom or other agent processes. <br></br><br></br> - A low idle timer value results in faster response(s) by agent processes and more prompt delivery of job status messages and external events to SAM-SS. <br></br> - A high idle time value results in lower CPU utilization since less processing is necessary. <br></br><br></br> **Note**: When messages accumulate, \*SMA/DISPLAY/HANDLER retrieves display messages more frequently (than the configured time); however, when the number of messages lessens, the idle timer resets to the configured value. | 
| Hostname alias | ```<None>``` | Any valid hostname | This field allows you to specify an alias for the agent. <br></br><br></br> - If no alias is entered, the BNA hostname must be entered for the Machine in the Enterprise Manager. <br></br> - If multiple agent instances are in use, additional instances require an alias. <br></br> - If an alias is entered, the same alias must be entered for the Machine in the Enterprise Manager and in the Hosts file on the OpCon application server. <br></br> - The alias (or BNA hostname) must be followed with a period (.) when defining a Machine in Administration of the Enterprise Manager. <br></br> - The alias (or BNA hostname) must also be followed with a period (.) when defining a Machine in the Hosts file of the OpCon application server. <br></br><br></br> The alias must not be followed by a period when defined in the \*SMA/CONFIG/xxx program. |
| Accept messages from IP addresses | ALL | - ALL <br></br> - Any valid dotted decimal IP address | This field allows you to specify up to five different TCP/IP addresses as machines from which the agent accepts messages. |