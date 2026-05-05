---
title: Interactive Agent Window
description: "Describes the interactive window provided by the MCP Agent for viewing version information and currently running or recently completed jobs."
tags:
  - Reference
  - Operations Staff
  - System Administrator
  - Agents
---

# Interactive LSAM Window

## What is it?

The Interactive Agent Window provides a terminal interface for querying the MCP Agent's active version and viewing jobs that are currently running or have recently completed. Commands such as VERSION and JOBS can be transmitted from the home position of the agent window and support lowercase input.

- Verify the active version of the MCP Agent running on a system.
- View a list of jobs currently running or recently completed that were initiated by the MCP Agent.

The MCP Agent provides the following interactive information and functions:

* Determination of the active version of the agent: Transmit VERSION (or VER) from the home position of the agent```<optional agent instance identifier>``` window.
* Viewing of all jobs currently running or recently completed that were initiated by the MCP Agent: Transmit JOBS from the home position of the agent```<optional agent instance identifier>``` window.
* If more than one page of information is available, retrieve subsequent pages by typing NEXT from the Home position then Transmit the line.

:::info Note

The Interactive Agent Window allows commands in lowercase letters.

:::