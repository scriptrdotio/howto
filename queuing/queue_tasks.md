# How to create queued jobs?

Queued jobs are scripts that are put in a queue and that execute sequentially and asynchronously. There are many situations where an application needs to create queued jobs, such as:

- When a remote client requests the execution of a lengthy operation and cannot wait for the answer
- When a script needs more time to execute than the maximum time allocated by scriptr
- When a script has to absorbe a sudden spike of requests issued by remote clients (e.g. devices)
- More generally, when batching makes more sense than a transactional behavior
- ...

Scriptr allows you to create queued jobs very easily, using the **queue** module. To create a queued job, apply the following steps:

- Create a channel that will be used as a queue
- Create the job (a script of which instances are put in the queue)
- Create the manager script (the script that puts jobs in the queue)

## Create a channel

**Reminder**: this step is optional if you already have channels and wish to reuse them

A channel is a generic publish/subscribe mecanism. Scripts or remote clients can publish or subscribe to it using any of the supported messaging protocols (websockets, mqtt, amqp). Any published messages is automatically broadcast to all subscribers.
To create a channel:

- In the [workspace](https://www.scriptr.io/workspace), click on your username on the top-right corner of the screen and select **Settings**
- Click on the **Channels** tab then click "+Add Channel"
- Enter a name for your channel. Do not check the boxes if you do not want to authorize non authenticated (anonymous) subscriptions or publications

![A Channel](../publish_subscribe/images/create_secure_channel_2.png)

*Image 1*

## Create the job

A job could be any script. 

As an illustration for this tutorial, we will use a script that sends weather data to a weather forecast web site API, then saves the returned answer into a document. Observe that the script receives data through the native **request** object. Assume this script is saved as "tutorials/howto/queuing/job". 

```
var document = require("document");
var metclient = require("../metclient");
try {
    var metClient = new metclient.MetOffice(); 
    var resp = metClient.sendObservation(request.parameters);
    document.save(resp);
}catch(exception){
    return exception;
}
```

## Create the manager script

This script requires the **queue** module and creates an instance of a queue client by invoking the **getInstance()** function, passing the name of a **channel**. The scripts pushes a new job into the queue by invoking the **queue()** function of the queue client, specifying the absolute path of the corresponding script, and providing the data to be processed.

```
var queue = require("queue");
var queueClient = queue.getInstance("internal_topic"); 
queueClient.queue("tutorials/howto/queuing/job", request.parameters); 
```

This is a typical scenario where you would use queuing. Indeed, hundreds of devices might be sending data to the above script and not expecting any reply, therefore, resorting to a queue would shorten their request cycle.

# More

- Read more about the queue module in our [documentation](https://www.scriptr.io/documentation#documentation-queuemodulequeueModule)
- Check our blog post about [queuing jobs with scriptr](https://blog.scriptr.io/queuing-tasks-with-scriptr-io/)
