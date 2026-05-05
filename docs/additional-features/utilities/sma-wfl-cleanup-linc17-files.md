---
title: "*SMA/WFL/CLEANUP/LINC17/FILES"
description: "A utility WFL that removes aged Acceptfiles from the *SMA/LINC17/FILES directory created by EAE/AB Suite MCP jobs."
tags:
  - Procedural
  - System Administrator
  - Agents
---

# *SMA/WFL/CLEANUP/LINC17/FILES

## What is it?

\*SMA/WFL/CLEANUP/LINC17/FILES removes Acceptfiles from the \*SMA/LINC17/FILES directory that are older than a specified number of days, keeping disk usage under control when EAE/AB Suite MCP jobs are run with an ACCEPTFILE parameter. The utility accepts two parameters: the number of days' worth of Acceptfiles to retain, and the family on which to search for the \*SMA/LINC17/FILES directory.

- Purge aged Acceptfiles left in \*SMA/LINC17/FILES after EAE/AB Suite jobs complete or fail
- Automate routine cleanup of the \*SMA/LINC17/FILES directory on a scheduled basis via OpCon


