# Inquire Display Msg Backlog (MSGCOUNT)

Use this screen to inquire as to the backlog waiting to be processed by the Display Handler. A high number of messages awaiting processing may cause a delay in actions associated with a given message. If a large number of messages are consistently backlogged, it is prudent to analyze the display message definitions (\*SMA/DISPLAYS and \*SMA/DISPLAYS/SYSMSG) to determine if the defined tokens are fairly unique. Using a common message token, such as "ENTER" or "DATE" to select messages will cause a large number of messages to be selected for analysis.

###### SMA Configuration and Operations Manager: SMAMSGCOUNT

![SMAMSGCOUNT](/img/smamsgcount.png)

