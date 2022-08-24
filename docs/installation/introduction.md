# Introduction

The installation files for the MCP LSAM reside in MCP containers files encapsulated within a zip file. The zip file will be named, MCP_LSAM_nnnnnn_LEVELn; where nnnnnn is the MCP LSAM version number and LEVELn reflects the COMPILERTARGET level of the MCP machine upon which the LSAM will be installed. The zipped file must be transferred to a Windows machine, unzipped, and the resulting two container files transferred or copied to MCP. The estimated installation time is between 15 and 20 minutes.

## Multiple LSAM Installations

Subject to licensing restrictions, a site may install and concurrently run multiple copies of the MCP LSAM. Multiple LSAMs are useful in disaster recovery testing and implementation. Each LSAM must have a unique machine name and must use unique ports for scheduling SMANetcom, View Job Output (JORS), SMA File Transfer Server(s), and SMA File Transfer Agent.

When installing multiple LSAMs, identify each additional instance with a one- to three-character string to distinguish them. This string serves as the unique identifier for additional LSAMs. Keep in mind that any user-written WFLs that call LSAM utilities and any user programs that use the External Event library interface must use the unique LSAM identifier.

Throughout this document, the notation xxx or /xxx is used to indicate the unique LSAM identifier, when applicable.

:::info Note

If a single LSAM is desired, it is not necessary to use an LSAM identifier.

:::

Use the same procedures to install each LSAM in a multiple LSAM environment as you would to install a single LSAM. For more information, refer to [New Installation](/installation/new-installation).

## Prerequisites

The Pre-installation Worksheet has fields of required information for a successful MCP LSAM installation as well as fields for optional features which aid in implementing all of the LSAM features. For more information, refer to [Pre-installation Worksheet](/installation/pre-installation-worksheet).

