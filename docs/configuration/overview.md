---
title: Configuration Overview
description: "An overview of the MCP Agent configuration section, covering the configuration file, all parameter groups, and procedures for common configuration tasks."
sidebar_label: Overview
tags:
  - Conceptual
  - System Administrator
  - System Configuration
  - Agents
---

# Configuration Overview

## What is it?

The Configuration section documents all parameters that control MCP Agent behavior, organized by parameter group: General (GEN), Communication (COMM), Processing Variables (VAR), and Optional Modules (OPT). It also covers procedures for specific configuration tasks such as adjusting job concurrency limits and defining failure and status message logic.

- Use the MCP LSAM Configuration page for an introduction to the configuration file structure and how to access it through SMA/MANAGER.
- Use the parameter group reference pages to look up individual settings and their valid values.

The following table describes each page in this section.

## In this section

| Page | Description |
| ---- | ----------- |
| [MCP LSAM Configuration](mcp-lsam-configuration) | Introduction to the configuration file and the SMA/MANAGER-based workflow for viewing and editing configuration settings. |
| [Configuration Settings](configuration-settings) | Step-by-step procedure for accessing and modifying configuration settings through SMA/MANAGER. |
| [General LSAM Configuration (GEN)](general-lsam-configuration) | Reference for all General parameter group settings — agent instance identifier, port, timing, logging, and core behavior options. |
| [Communication Parameters (COMM)](communication-parameters) | Reference for all Communication parameter group settings — SMANetCom address, port, retry intervals, and TLS options. |
| [Processing Variables (VAR)](processing-variables) | Reference for all Processing Variable settings — job limits, prerun behavior, output handling, and MCP-specific options. |
| [Optional Modules (OPT)](optional-modules) | Reference for optional module settings — Automated Response, JORS, MSGIN, File Monitor, Resource Monitor, and SMA File Transfer. |
| [Update Max Concurrent Jobs](update-max-concurrent-jobs) | Procedure for changing the maximum number of jobs the MCP Agent runs concurrently. |
| [Set Up Failure and Status Message Logic](set-up-failure-status-message) | How to configure failure status message detection so the MCP Agent correctly reports job completion states to OpCon. |
