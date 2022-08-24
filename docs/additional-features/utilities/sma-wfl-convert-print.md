# *SMA/WFL/CONVERT/PRINT (MCP Print File Conversion)

The print conversion utility converts an MCP print file (kind=BACKUPPPRINTER) to an ASCII text file. Sites may find this utility helpful as a preliminary step to a SMA File Transfer job in distributing print files to users for viewing in an ASCII environment (Windows, UNIX, etc.).
 
The utility consists of two modules: \*SMA/WFL/CONVERT/PRINT and \*SMA/OBJ/CONVERT/PRINT. You will only reference the WFL, \*SMA/WFL/CONVERT/PRINT, which accepts two parameters. The first parameter is the title of the MCP print file to be converted; the second parameter is the title of the ASCII text file to be created. It is anticipated that you will then define a SMA File Transfer job to effect a text transfer of the ASCII file.

## Syntax

On the MCP Job Details screen, use the syntax specified in these next two subsections.

### File Title
\*SMA/WFL/CONVERT/PRINT/xxx

### Arguments

"```<MCP print file>```","```<ascii text file>```"
* ```<MCP print file>``` is the title of the MCP print file to be converted.
* ```<ASCII text file>``` is the title of the ASCII test file created as output.