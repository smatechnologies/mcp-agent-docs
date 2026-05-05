---
title: User-defined Restart/Recovery Checkpoints
description: "Explains how to configure the MCP Agent to periodically back up job array and tracking information to minimize data loss during a restart or recovery."
tags:
  - Conceptual
  - System Administrator
  - Agents
---

# User-defined Restart/Recovery Checkpoints

## What is it?

User-defined Restart/Recovery Checkpoints allow the MCP Agent to periodically back up job array and tracking information at configurable intervals — per minute, per job array update, or never — and at normal shutdown, so the agent can recover to the latest checkpoint after a restart. Administrators must balance checkpoint frequency against processing performance, as more frequent checkpoints improve data recovery but may slow processing.

- Configure checkpoint frequency and interval to protect job tracking data in environments prone to instability or unexpected shutdowns.
- Tune checkpoint frequency to improve processing performance in stable environments where data loss risk is low.

To minimize possible data loss, the MCP Agent backs up job array and tracking information at user-specified intervals and at a normal shutdown. These periodic backups are called checkpoints. During a restart/recovery, the agent automatically falls back to the data in the latest checkpoint.
 
User-defined checkpoint frequencies are per minute, per job array update, or never. The interval (in minutes or updates) between these checkpoints can also be defined. To update these configuration values, refer to the procedure in the related topic.
 
With this feature, consider the risk of data loss versus processing performance. More checkpoints may burden and slow processing, but improve data recovery. Fewer checkpoints may improve processing performance, but diminish data recovery. Try to balance the costs and benefits of checkpoints. If the computing environment is unstable and prone to crashes, faster processing may be traded for greater data protection. If the environment is more stable, fewer checkpoints may be desired to achieve better processing performance.

## Update the Configuration File

If User-defined Checkpoints were not defined during the installation, update the configuration file.
 
Modify the following fields under [Optional Modules (OPT)](../../operations-and-components/sma-manager/optional-modules):

a. Freq

b. Interval