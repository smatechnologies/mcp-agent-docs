# Resource Utilization statistics

Selected job or task-level statistics can be returned with the OpCon job status update message and are visible in the Enterprise Manager.

## Update the Configuration File

By default, this feature is disabled. To enable resource utilization statistics reporting, the configuration file must be updated.
 
Modify the following fields under [Optional Modules (OPT)](/operations-and-components/sma-manager/optional-modules):

a. **Enable Statistics**: Set to a value of **Y**.

b. **Task completion message**: To receive task-level statistics for all resources listed in the Resource Utilization Statistics, except Wait time, set to a value of **A** or **F**:

* In order to receive statistics on all subordinate tasks, set to a value of **A**.
* In order to receive statistics on failed tasks only, set to value of **F**.

For more information on these configuration options, refer to [Processing Variables (VAR)](/operations-and-components/sma-manager/processing-variables).

:::info Note

Accumulated values include task-level statistics regardless of the value of the "Task Completion Messages" configuration variable.

:::

## Available Resource Utilization Statistics

| Resource | Description | When reported |
| -------- | ----------- | ------------- |
| Elapsed time | - This resource displays a process' elapsed time, as reported by the operating system. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of a process. |
| I/O time | - This resource displays a process' I/O time, as reported by the operating system. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of a process. |
| Number of print lines | - This resource displays the number of print lines produced by the process. <br></br> - Print lines produced by the job summary are not included in this value. | Upon completion of a process. |
| Processor time | - This resource displays a process' processor time, as reported by the operating system. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of a process. |
| ReadyQ time | - This resource displays a process' ReadyQ time, as reported by the operating system. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of a process. | 
| Wait time | - This resource displays a process' elapsed wait time, as reported by the operating system. <br></br> - The value extends to 1/10,000th of a second. | Upon a process being resumed following a Wait state. |
| Accumulated elapsed time | - This resource displays the accumulated elapsed time of the WFL compile and all subordinate tasks. <br></br> - The elapsed time of the job is not included in this value. | The value extends to 1/10,000th of a second. | Upon completion of the job. | 
| Accumulated I/O time | - This resource displays the accumulated I/O time of the WFL compile and all subordinate tasks. <br></br> - The I/O time of the job is not included in this value. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of the job. |
| Accumulated print lines | - This resource displays the accumulated print lines of the WFL compile and all subordinate tasks. <br></br> - Print lines produced by the job are not included in this value. | Upon completion of the job. |
| Accumulated processor time | - This resource displays the accumulated processor time of the WFL compile and all subordinate tasks. <br></br> - The processor time of the job is not included in this value. <br></br> - The value extends to 1/10,000th of a second. |Upon completion of the job. |
| Accumulated readyq time | - This resource displays the accumulated readyq time of the WFL compile and all subordinate tasks. <br></br> - The readyq time of the job is not included in this value. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of the job. |
| Accumulated wait time | - This resource displays the accumulated wait time of the WFL compile and all subordinate tasks. <br></br> - The wait time of the job is not included in this value. <br></br> - The value extends to 1/10,000th of a second. | Upon completion of the job. |
| Job/task mix number | - This resource displays the job or task mix number. | Upon completion of the job/task. |
| Process name | - This resource displays the task attributes USERCODE and NAME. | Upon completion of the process. |

