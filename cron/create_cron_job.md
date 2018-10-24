# How to schedule the automatic execution of a script (cron job)?

Scriptr.io allows you to automatically execute your scripts are regular intervals. 
There are two ways to do this: 
- From the [workspace](https://www.scriptr.io/workspace]
- From the code of a script

** Note** scheduled scripts should have a return instruction (you cannot schedule the execution of modules)

## Schedule the automatic execution of a script from the workspace

From the [workspace](https://www.scriptr.io/workspace], select an existing script from the tree view on left-side, 
or create a new script (click on New Script) and type some instructions.

![Schedule a script](./images/schedule.png)

From the "Schedule script" dialog, define your scheduling rule:

- Specify if the script should execture regularly (**every**) or at at specified date/time (**on**)
- Specify the time range (hour, day, week, month or year)
- Specify the hour of execution
- Specify the minute of execution

In the below example, we schedule the script to run every data at 08:00 AM.

![Cron trigger](./images/create_trigger.png)

**Note** if you are familiar with [cron expressions](https://www.freeformatter.com/cron-expression-generator-quartz.html), you can directly write an expression by clicking on the Advanced link.






