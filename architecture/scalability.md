# Scalability

Scalability is always a concern in most enterprise-grade applications. While it is definitely possible to increase capacity, solution architects will evaluate design alternatives that maximize the available resources, before considering any capacity increase. On that end, this document goes through a few options that can be assessed when implementing an application.

In this document, we use the word *application* to refet to business logic deployed and executed on scriptr.io. We also use the words *request*, *message* and *event* interchangeably, to refer to any demand sent by a client application to the scriptr.io application.

## Asynchronous processing

It often appears that sychronous, request-reply and/or transactional processing are not necessary to tackle a given use cases, but they are actually used out of habit, leading sometimes to bloating the application by reserving a large part of the available resources. Therefore when designing an application, it is important to answer the following questions:
- Must the emitter of the request receive an response immediately or can it be "contacted" later to be provided with the outcome of its request?
- Is the execution time of the logic triggered by a request higher than a few seconds? Can it span to minutes or hours? 

If at least one of the answers to those questions is "yes", the asynchronous processing should definitely be considered.

### Queued jobs

The [Broker](./broker.md) and [Mediator](./mediator.md) architecture patterns can be used to handle asynchronous event-driven business logic by decoupling the message producers (e.g. client applications) from the message processors, allowing the latter to processe the messages at a more convenient pace

### Long running jobs

## Data processing

### Shards

### Incremental data aggregation

### Use the right data store type

## Increase capacity
