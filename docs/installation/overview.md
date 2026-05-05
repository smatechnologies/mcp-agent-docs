---
title: Installation Overview
description: "An overview of the MCP Agent installation section, including installation package structure, multiple-agent support, prerequisites, and links to installation procedures."
sidebar_label: Overview
tags:
  - Conceptual
  - System Administrator
  - Installation
  - Getting Started
---

# Installation Overview

## What is it?

The Installation section covers everything required to deploy the MCP Agent — from gathering prerequisites and copying installation files through completing a new installation or upgrading an existing one. Installation files are distributed as a zip archive containing MCP container files that must be transferred to the MCP platform before running the installation program. The estimated installation time is between 15 and 20 minutes.

- Use the pre-installation worksheet to gather all required configuration values before starting the installation.
- Follow the new installation or upgrade procedure depending on whether this is a first-time deployment or a version update.

## Installation Package

The installation files for the MCP Agent reside in MCP container files encapsulated within a zip file. The zip file is named `MCP_LSAM_nnnnnn_LEVELn`, where `nnnnnn` is the MCP Agent version number and `LEVELn` reflects the COMPILERTARGET level of the MCP machine on which the agent will be installed. Transfer the zipped file to a Windows machine, unzip it, and transfer or copy the resulting two container files to MCP.

## Multiple Agent Instances

Subject to licensing restrictions, a site may install and concurrently run multiple MCP Agent instances. Multiple MCP Agent instances are useful in disaster recovery testing and implementation. Each agent instance must have a unique machine name and must use unique ports for scheduling SMANetcom, View Job Output (JORS), SMA File Transfer Server(s), and SMA File Transfer Agent.

When installing multiple MCP Agent instances, identify each additional instance with a one- to three-character string to distinguish them. This string serves as the unique agent instance identifier. Any user-written WFLs that call agent utilities and any user programs that use the External Event library interface must use this unique agent instance identifier.

Throughout this document, the notation xxx or /xxx indicates the unique agent instance identifier, when applicable.

:::info Note

If a single agent instance is desired, it is not necessary to use an agent instance identifier.

:::

Use the same procedures to install each agent instance in a multiple-agent environment as you would to install a single agent. For more information, refer to [New Installation](new-installation).

## Prerequisites

The Pre-installation Worksheet contains fields for all required information for a successful MCP Agent installation, as well as fields for optional features that help implement all agent capabilities. For more information, refer to [Pre-installation Worksheet](pre-installation-worksheet).

## In this section

| Page | Description |
| ---- | ----------- |
| [Pre-Installation Worksheet](pre-installation-worksheet) | A checklist of values to collect before starting the installation — system name, port numbers, usercode, family names, and optional module settings. |
| [Copy Installation Files to MCP](copy-installation-files) | Steps for transferring the MCP Agent installation files from the distribution medium to the MCP platform. |
| [Automated Installation/Upgrade](automated-installation-upgrade) | How to use the automated installation and upgrade script to deploy or update the MCP Agent without stepping through manual prompts. |
| [New Installation](new-installation) | Step-by-step procedure for installing the MCP Agent on an MCP system for the first time. |
| [Upgrade Installation](upgrade-installation) | Step-by-step procedure for upgrading an existing MCP Agent installation to a newer version. |
