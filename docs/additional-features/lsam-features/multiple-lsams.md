---
title: Multiple LSAMs
description: "Learn how to install and concurrently run multiple copies of the MCP LSAM for disaster recovery testing and implementation."
tags:
  - Conceptual
  - System Administrator
  - Agents
---

# Multiple LSAMs

Subject to licensing restrictions, a site may install and concurrently run multiple MCP Agent instances. Multiple MCP Agent instances are useful in disaster recovery testing and implementation. For additional information, refer to [Multiple LSAM Installations](../../installation/overview#multiple-agent-instances).

## Port Requirements

Each MCP Agent instance must use a unique set of TCP port numbers to avoid conflicts. The following table lists the default port for each component and the configuration location where each port is set:

| Component | Default Port | Configuration |
| --------- | ------------ | ------------- |
| OpCon scheduling (SMANetCom) | 3100 | Communication Parameters (COMM) — OpCon TCP/IP port number |
| JORS | 3110 | Optional Modules (OPT) — JORS Port Number |
| SMAFT Server (non-TLS) | 3120 | Optional Modules (OPT) — FTServer nonTLS Port |
| SMAFT Agent | 3130 | Optional Modules (OPT) — SMA Agent Port Number |

When configuring multiple instances, assign a unique value for each port across all instances. Also update the corresponding machine definition in Solution Manager to match each instance's port assignments.

