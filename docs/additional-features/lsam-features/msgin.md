# MSGIN

MSGIN functionality has been replaced by the External Event Interface Library that offers a dramatic increase in event throughput. Customers should use the External Event Interface Library or \*SMA/EVENTGEN/xxx. For information, refer to [External Event Interface Library](../../additional-features/lsam-features/external-event-interface-library). For backwards compatibility, MSGIN continues to be supported and is documented here.

## Update the Configuration File

If MSGIN was not activated during the installation, the configuration file must be updated.
 
Modify the following fields under [Optional Modules (OPT)](../../operations-and-components/sma-manager/optional-modules):

a. MSGIN: Freq

b. MSGIN: Family

## Define an External Event

1. Create a SEQDATA file named \*SMA/MSGIN/```<user defined name>```.

2. In the first record, enter a valid User Login ID and event external token.

3. In the second record, and subsequent records if desired, enter the syntax for an OpCon event. For a list of valid OpCon events, refer to [Introduction](https://help.smatechnologies.com/opcon/core/events/introduction) in the OpCon Events online help.

4. Save the file.

:::info Note

An external event definition, including User Login ID and event external token, cannot be longer than 738 characters.

:::

:::tip Example

In this use case, we have the need to dynamically supply different values as parameters to a job through an OpCon Event. One of these values contains a character that would cause a problem with the event. The solution for this problem is to define multiple properties instead, and place the problem character in the job definition. For this example, the problem character in question is a comma (,).
 
On the Job Definition, the first Parameter to the job must be a string of alpha characters (e.g., DAILY), and the second parameter must be a string of alpha characters with a comma in the middle (e.g., TEST,JOB).
 
The *incorrect* approach is:

1. In the Job Details for the platform, we use the following Tokens separated by commas:

```[[JI.PARAM1]],[[JI.PARAM2]]```

2. In the OpCon Event to add the job, we use this syntax:

```$JOB:ADD,$DATE,SCHEDULE,JOB,FREQCODE,PARAM1=DAILY;PARAM2=TEST,JOB```

#### Result

The job will fail because a comma is used by OpCon as a delimiter for events, and when the Tokens resolve, the value becomes "DAILY,TEST" instead of "DAILY,TEST,JOB".
 
The *correct* approach is:

1. In the Job Details for the platform, we use the following tokens separated by commas:

```[[JI.PARAM1]],[[JI.PARAM2]],[[JI.PARAM3]]```

2. In the OpCon Event to add the job, we use this syntax:

```$JOB:ADD,$DATE,SCHEDULE,JOB,FREQCODE,PARAM1=DAILY;PARAM2=TEST;PARAM3=JOB```

#### Result

When those tokens are resolved at job run time, they will become: DAILY,TEST,JOB

:::