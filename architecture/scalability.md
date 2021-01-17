# Scalability

Scalability is always a concern in most enterprise-grade applications. While it is definitely possible to increase capacity, solution architects will evaluate design alternatives that maximize the available resources, before considering any capacity increase. On that end, this document goes through a few options that can be assessed when implementing an application.

In this document, we use the word *application* to refet to business logic deployed and executed on scriptr.io. We also use the words *request*, *message* and *event* interchangeably, to refer to any demand sent by a client application to the scriptr.io application.

## Asynchronous processing
It often appears that sychronous, request-reply and/or transactional processing are not necessary to tackle a given use cases, but they are actually used out of habit, leading sometimes to bloating the application by reserving a large part of the available resources.

### Queued jobs

### Long running jobs

## Data processing

### Shards

### Incremental data aggregation

### Use the right data store type

## Increase capacity
