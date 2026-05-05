---
title: MCP Known Issues
description: "Review documented MCP LSAM known issues and their workarounds, including FTAgent compatibility, startup errors caused by concurrent jobs changes, and JORS limitations."
tags:
  - Reference
  - System Administrator
  - Agents
  - System Configuration
---

# MCP Known Issues

## What is it?

This page documents known issues in the MCP Agent with their symptoms and workarounds, covering the SMA/FTAgent version compatibility error, the fatal startup errors that occur when the maximum concurrent jobs value is changed without removing checkpoint and tracking files, and current limitations of the Job Output Retrieval System (JORS).

- Use this page when encountering a startup failure with a SEG ARRAY ERR or ASSERTION FAILURE error to confirm the resolution requires removing checkpoint files before restarting the agent.
- Use this page to check JORS limitations before configuring job output retrieval, particularly for sites where the agent and print files reside on different families.

## SMA/FTAgent Error

The MCP SMA/FTAgent for releases prior to MCP Agent 16.0 will fail when used with OpCon 16.0.
 
**Workaround**: Upgrade to MCP Agent 16.02 or higher.

## Fatal Errors during Startup

### SMA/MCP/INTERFACE

```

SEG ARRAY ERR @178600

```

The above error occurs if the "Max number concurrent jobs" configuration value is changed and the agent was restarted before removing the agent's checkpoint files. For information on modifying the "Max number concurrent jobs" option, refer to [Update the "Max Number Concurrent Jobs" Field](../configuration/update-max-concurrent-jobs).

### SMA/COMM

```

ASSERTION FAILURE ON RANGE TEST @ (Expression out of range 91700)
 
```

The above error occurs if the "Max number concurrent jobs" configuration value is changed and the agent was restarted before removing the agent's tracking file. For information on modifying the "Max number concurrent jobs" option, refer to [Update the "Max Number Concurrent Jobs" Field](../configuration/update-max-concurrent-jobs).

## JORS Limitations

The Job Output Retrieval System (JORS) functionality is currently reserved for OpCon jobs initiated with the START command. Enabling this functionality for OpCon jobs initiated with the RUN command is under consideration for future implementation.
 
The Summary configuration variable is not operational at this time. The administrator cannot restrict users from viewing job summaries unless the JORS UC configuration variable is set to Y and the site's job summaries are non-usercoded.
 
For sites that do not run the agent on the same family as that on which the print files exist, it may not be possible for the GETSTATUS call (used by JORS to get the list of print files) to see the print files. The symptom is the "No Output Files" message in response to the View Job Output request from Operations in the Enterprise Manager.
 
**Workaround**: Confirm a print file exists for the requested job. If it does, then do not initiate JORS when the agent starts. Instead, create a separate WFL to initiate JORS. This WFL may reside as a non-usercoded file or under a usercode whose primary family is the same as the default print family.