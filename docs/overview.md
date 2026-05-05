---
sidebar_label: 'Overview'
title: OpCon MCP Agent overview
description: "An overview of the OpCon MCP Agent (MCP LSAM), including its purpose, abbreviations used throughout the documentation, and key concepts."
tags:
  - Conceptual
  - System Administrator
  - Automation Engineer
  - Agents
---

# OpCon MCP Agent overview

## What is it?

The MCP Agent, Version 21.06.00, is an OpCon agent that allows OpCon to schedule MCP jobs within an MCP environment. The agent communicates with the OpCon server to receive job instructions, run them on the MCP platform, and report results back to OpCon.

- Use the MCP Agent when you need to automate and schedule jobs that run on Unisys MCP (Master Control Program) systems.
- The agent supports a full suite of features including file monitoring, file transfer, automated responses, and job output retrieval (JORS).
- Multiple agent instances can be installed on a single MCP machine, allowing you to support different environments or configurations simultaneously.

## MCP abbreviations

Throughout this documentation, several abbreviations are used for common MCP items.

| Abbreviation | Meaning |
| ----------- | ------- |
| MARC | Menu-Assisted Resource Control |
| WFL | Workflow Language |
| MCS | Message Control System |
| IDC | Interactive Datacomm Configurator |
| LIBS | System Libraries |
| SSL | Set System Library |
| SL | System Library |
| COMS | Transaction Server for MCP |
| /xxx | This indicates a forward slash followed by the unique agent instance identifier used when a site has multiple agent instances installed on a single MCP machine |
| xxx  | This indicates the unique agent instance identifier used when a site has multiple agent instances installed on a single MCP machine |

## FAQs

**What MCP versions does the agent support?**
The MCP Agent 21.06.00 is compiled on MCP 60.1. Earlier versions 19.00.00 and 19.01.00 are also available compiled on MCP 60.1.

**Can I run multiple agent instances on one MCP machine?**
Yes. You can install multiple agent instances on a single MCP machine. Each instance uses a unique agent instance identifier (referred to as `xxx` in the documentation) to distinguish it from other instances.

**What communication protocol does the agent use?**
The MCP Agent communicates with OpCon using TCP/IP. TLS encryption is supported for both scheduling (SMANetcom) and JORS communications.

**Does the agent support SMA File Transfer?**
Yes. SMA File Transfer (SMAFT) is supported, though TLS is not currently available for SMAFT communications.

## Glossary

**LSAM (Legacy Schedule Activity Monitor)** — The agent software installed on MCP machines that communicates with OpCon. In user-facing documentation, this is referred to as the "agent." The term "LSAM" is retained here because it appears in MCP-specific installer and program names.

**WFL (Workflow Language)** — The MCP native scripting language used to define job workflows. OpCon submits and monitors WFL jobs on the MCP platform.

**JORS (Job Output Retrieval System)** — The component that retrieves job output from the MCP platform and makes it viewable in OpCon.

**SMA/MANAGER** — The MCP-based user interface used to configure the agent, manage operational tasks, and maintain definition files without requiring direct access to the OpCon server.

**COMS (Transaction Server for MCP)** — The MCP transaction server component used for communication between agent modules.
