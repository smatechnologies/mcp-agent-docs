# Job Output Retrieval System

The Job Output Retrieval System (JORS) allows users to view job output from the OpCon Enterprise Manager. To activate JORS, configure both the LSAM and the Enterprise Manager.

## Configure JORS in the LSAM Configuration

If JORS was not activated during the installation, the configuration file must be updated.
 
Modify the following fields under [Optional Modules (OPT)](/operations-and-components/sma-manager/optional-modules):

a. JORS

b. JORS: Port

c. JORS: Prefix

d. JORS: Family

## Configure the JORS Port in the EM

For the Enterprise Manager to connect to the LSAM for job output, configure the JORS Port Number to match the JORS Port configured through the LSAM. For more information on setting the JORS Port Number for the machine, refer to [Configuring Advanced Machine Parameters and Properties](https://help.smatechnologies.com/opcon/core/Files/UI/Enterprise-Manager/Configuring-Advanced-Machine-Properties) in the Enterprise Manager online help.

## View Job Output in the EM

For more information on viewing MCP job output from the OpCon Enterprise Manager, refer to [Viewing Job Output](https://help.smatechnologies.com/opcon/core/Files/UI/Enterprise-Manager/Performing-Job-Procedures-List#viewing-job-output) in the Enterprise Manager online help.