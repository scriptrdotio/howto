# How to unschedule the automatic execution of a script (cron job)?

There are two ways to do this:

- From the [workspace](https://www.scriptr.io/workspace)
- From the code of a script

## Unschedule a script from the workspace

- Open the [workspace](https://www.scriptr.io/workspace) and browser the tree view on the left to find the scheduled script. 
- Open the script in the editor
- Click on on the ⌚Schedule button in the script editor toolbar
- In the "Schedule Script" dialog, click on the trash can icon near the trigger you wish to remove

![Remove trigger](./images/delete_trigger.png)

## Unschedule a script from the code

Scripts can be unscheduled using the native **unschedule()** function. All you need is pass it the handle obtained when scheduling he script (read more on [how to schedule the automatic the execution of a script](./create_cron_job.md). 

In the example below, we assume that the handle was persisted in a document ("scheduled_script_handle") in the "handle" field.

```
var document = require("document");
var resp = document.get("scheduled_script_handle");
if (resp.metadata.status == "success") {  // if document is found
    
    var handle = resp.result.handle;
    return unschedule(handle); 
}

return null;
```
