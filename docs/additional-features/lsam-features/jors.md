---
title: Job Output Retrieval System (JORS)
description: "Configure JORS to allow users to view MCP job output directly from the OpCon interface."
tags:
  - Conceptual
  - System Administrator
  - Operations Staff
  - Agents
---

# Job Output Retrieval System (JORS)

## What is it?

JORS (Job Output Retrieval System) allows users to view job output from MCP jobs directly within the OpCon interface. When JORS is configured, job output is accessible without requiring direct access to the MCP system.

- Use JORS to retrieve and review MCP job print output from the OpCon interface after a job completes.
- JORS requires configuration in both the MCP Agent and the OpCon machine definition before it can be used.

The Job Output Retrieval System (JORS) allows users to view job output from Enterprise Manager or Solution Manager. To activate JORS, configure both the MCP Agent and the OpCon machine definition.

## Configure JORS in the Agent Configuration

If JORS was not activated during the installation, update the configuration file.
 
Modify the following fields under [Optional Modules (OPT)](../../operations-and-components/sma-manager/optional-modules):

a. JORS

b. JORS: Port

c. JORS: Prefix

d. JORS: Family

## Configure the JORS Port Number

For Enterprise Manager or Solution Manager to connect to the MCP Agent for job output, configure the JORS Port Number to match the JORS Port configured through the agent. The default JORS port number is **3110**. For more information on setting the JORS Port Number for the machine, refer to [Configuring Advanced Machine Parameters and Properties](https://help.smatechnologies.com/opcon/core/Files/UI/Enterprise-Manager/Configuring-Advanced-Machine-Properties) in the Enterprise Manager online help.

## View Job Output

For more information on viewing MCP job output, refer to [Viewing Job Output](https://help.smatechnologies.com/opcon/core/Files/UI/Enterprise-Manager/Performing-Job-Procedures-List#viewing-job-output) in the Enterprise Manager online help.

## FAQs

**What must be configured before JORS will work?**
JORS requires configuration in two places: the agent configuration file (JORS, JORS Port, JORS Prefix, and JORS Family fields under Optional Modules) and the OpCon machine definition in Enterprise Manager or Solution Manager (the JORS Port Number under Advanced Machine Settings must match the port configured in the agent).

**What happens if the JORS Port Number in Enterprise Manager or Solution Manager does not match the agent?**
Enterprise Manager or Solution Manager will be unable to connect to the MCP Agent for job output retrieval. The View Job Output feature will return an error or no output.

**Does JORS require direct access to the MCP system to view output?**
No. Once JORS is configured, users can view MCP job print output directly from Enterprise Manager or Solution Manager without requiring direct access to the MCP system.

## Glossary

**JORS (Job Output Retrieval System)**: The MCP Agent component that makes job print output accessible from Enterprise Manager or Solution Manager after a job completes.

**JORS Port**: The TCP port number on which the JORS process listens for connections from Enterprise Manager or Solution Manager. Must match the JORS Port Number configured in the machine's Advanced Machine Settings.

**JORS Prefix / JORS Family**: Agent configuration parameters that control where JORS looks for job output files on the MCP platform.