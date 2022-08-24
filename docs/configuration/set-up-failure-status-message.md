# Set Up Failure and Status Message Logic

An MCP job's status in Enterprise Manager Operation relies on several configuration settings: Fail Immediately on Fail Code, Send Fail/Reset Message, Task-Failure Checking, and Task-Completion Message. (Refer to the configuration file tables starting in [Processing Variables (VAR)](/configuration/processing-variables).) If a job is not failed immediately, the internal JOB TO BE FAILED flag also plays an important role.

## Job to be Failed Flag

The JOB TO BE FAILED flag, set per job, ultimately determines the final status of MCP jobs run through the LSAM. The LSAM checks this flag when the job terminates. If the flag is set to the default "N", the LSAM reports the job as successful. If the flag is set to "Y", the LSAM reports a job's failure, even if the operating system reports a job's success.

During the processing of a job or a task, a match between the console display and the words entered in the Fail Code or Fail Reset fields determines the JOB TO BE FAILED flag's setting. A Fail Code match sets the flag to "Y" and a Fail Reset match sets the flag back to "N". Refer to [Failure Criteria](https://help.smatechnologies.com/opcon/core/job-types/mcp#failure-criteria) in the Concepts online help. Regardless of the actual outcome of the job or tasks, the final value of the JOB TO BE FAILED flag decides the success or failure in Enterprise Manager Operation.

## Fail Code and Fail Reset Logic

Use of Fail Codes is an alternative solution to programming a WFL to ABORT if a program IS NOT COMPLETED OK. Use of Fail Resets provides greater flexibility in assigning job statuses. For example, a critical application's success can reset the JOB TO BE FAILED flag despite the failure of other non-critical tasks. Refer to [Failure Criteria](https://help.smatechnologies.com/opcon/core/job-types/mcp#failure-criteria) in the Concepts online help.

The next table shows all the factors involved in using the Fail Code/Fail Reset feature. Use the table to configure the LSAM's behavior upon a Fail Code or Fail Reset match.

### Fail Code/Fail Reset Conditions

| Console Match | Fail Immediately on Fail Code | Job to be Failed | Send Fail/Reset Message | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ------------- | ----------------------------- | ---------------- | ----------------------- | -------------------------------------- |
| Fail Code | Y | N/A | N/A | JJJJJ/TTTTTFAIL MSG |
| Fail Code | N | Set to Y | A, F | JJJJJ/TTTTTFAILCODE |
| Fail Code | N | Set to Y | R, N | ```<NONE>``` |
| Fail Reset | N | Set to N | A, R | JJJJJ/TTTTTRESETCODE |
| Fail Reset | N | Set to N | F, N | ```<NONE>``` |

## Task-Level Checking

Task-level checking enables the LSAM to report a job as failed to Enterprise Manager Operation when a job's subordinate task fails. Display messages issued by the job do not determine the job completion status; job completion status is determined solely by the completion status of the subordinate task(s). With task-level checking enabled, the failure of any single task in a WFL marks the job as failed or sets the JOB TO BE FAILED flag to Y. 

If defined, Fail Codes and/or Fail Resets are applied to tasks regardless of the task-level checking setting. For more information on configuration settings, refer to [Processing Variables (VAR)](/configuration/processing-variables). When the LSAM is configured to report at the task level (A or F), the Enterprise Manager's job history includes the completion status of each task. 

The next table shows all the factors involved in task-level checking. Use the table to configure the LSAM's behavior upon a task's failure or success.

### Task-Level Checking Conditions

| Task | Task-Level Checking | Job to be Failed	| Task-Completion Message | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ---- | ------------------- | ---------------- | ----------------------- | -------------- |
| FAIL | I | N/A | N/A | JJJJJ/TTTTTTASK FAIL | 
| FAIL | T | Set to Y | A, F | JJJJJ/TTTTTTASK FAIL |
| FAIL | T | Set to Y | N | ```<NONE>``` |
| FAIL | T | Set to N | F, N | ```<NONE>``` |
| OK | I,T | N/A | A | JJJJJ/TTTTTCOMP OK |
| OK | I,T | N/A | F, N | ```<NONE>``` |\

## Final Status

If a job is not failed immediately, the JOB TO BE FAILED flag determines the success or failure of a job in Enterprise Manager Operation. If the flag is set to Y for multiple reasons, Enterprise Manager Operation takes the last job or task status. If the flag is N, then the job's final status is JJJJJCOMPLETED.

### Job To Be Failed Flag Effects


| Job to be Failed | Final Status | Status Message <br></br> JJJJJ = Job Mix Number <br></br> TTTTT = Task Mix Number |
| ---------------- | ------------ | --------------------------------------------------------------------------------- |
| Set to Y | FAILED | JJJJJ/TTTTTFAIL MSG |
| Set to Y | FAILED | JJJJJ/TTTTTTASK FAIL |
| Set to N | FINISHED OK | JJJJJCOMPLETED |

