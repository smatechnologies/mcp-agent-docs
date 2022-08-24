# SMA/Manager Overview

## Overview

The SMA/MANAGER program provides a single interface for performing configuration and operations tasks related to the MCP LSAM. It replaces the \*SMA/CONFIG program, and reduces the MCP-specific knowledge required to perform routine operational tasks. Upon accessing \*SMA/MANAGER, the user is presented with a main menu. All activities are performed by navigating successive screen Choices until the final screen is reached. In most cases, the user need only make a selection from the Main Menu to arrive at the final screen.

## Using SMA/MANAGER

To access the Manager program, from any MCP window type ?ON SMAMGRxxx where xxx represents the unique LSAM identifier, if used. If you are not presented the Main Menu, simply transmit a space and the Main Menu will appear.

There are three fields on the Main Menu: screen name, Action, and Choice. The screen name is a protected field and cannot be changed, but is presented so that the SMA/MANAGER program can identify the function to be performed, and to facilitate a point of reference for the user when accessing documentation. Each screen has the possibility of displaying informational and error messages. For a list of these messages and their meaning, refer to [Error and Informational Messages](/operations-and-components/sma-manager/error-and-informational-messages). These messages appear on the last line of the screen. If the message refers to an error in a field, the cursor will be placed in the field in error, a bell will sound, and the message will be in red or reverse video, depending on the terminal emulator in use.

For LSAM configuration fields, the allowed values are indicated on the screen adjacent to the field name. If no value is indicated, the field is not edited. In the upper left corner of each screen you will see the name of the screen. The name of this LSAM instance is notated in the heading. If this instance is not named, the word BASE will appear. The last line of the screen is reserved for error or informational messages. For more information regarding informational and error messages, please refer to [Error and Informational Messages](/operations-and-components/sma-manager/error-and-informational-messages).

Be advised that LSAM configuration changes (Main Menu options COMM, GEN, OPT, and VAR) will be implemented only after 1) notifying the LSAM by submitting the LOADCFG choice via the Manager program, or 2) starting the LSAM if the LSAM was not running when the configuration changes were made. Saved changes to the File, Message, and System Resource definitions files will be implemented only after the appropriate LSAM components have been notified of the changes. Please refer to the appropriate section for each definition file.

## Main Menu

It is from the Main Menu that the user exits the SMA/MANAGER program. To exit, type BYE in the Action field. To select an activity to perform, enter the mnemonic for the function in the Choice field.

![SMAMAINMENU](/img/smamainmenu.png)



