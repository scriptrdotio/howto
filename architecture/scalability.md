# Scalability

Scalability is always a concern in most enterprise-grade applications. While it is definitely possible to increase capacity, solution architects will evaluate design alternatives that maximize the available resources, before considering any capacity increase. On that end, this document goes through a few options that can be assessed when implementing an application.

In this document, we use the word *application* to refet to business logic deployed and executed on scriptr.io. We also use the words *request*, *message* and *event* interchangeably, to refer to any demand sent by a client application to the scriptr.io application.

## Asynchronous processing

It often appears that sychronous, request-reply and/or transactional processing are not necessary to tackle a given use cases, but they are actually used out of habit, leading sometimes to bloating the application by reserving a large part of the available resources. Therefore when designing an application, it is important to answer the following questions:
- Is there a large number of messages to process, whose emitters do not need an response immediately, but can be provided later with the outcome of their request?
- Is the execution time of the logic triggered by a request higher than a few seconds? Can it span to minutes or hours? 

If at least one of the answers to those questions is "yes", the asynchronous processing should definitely be considered.

### Queued jobs
The [Broker](./broker.md) and [Mediator](./mediator.md) architecture patterns can be used to handle the asynchronous execution of event-driven logic, by decoupling the message producers (e.g. client applications) from the message processors. More specifically, using job queues allow the latter to handle a very large number of messages, whose processing time is measured in seconds, at a more convenient pace.

### Long running jobs
When the processing of a message takes more than a few seconds and can span over minutes or even hours, then this type of message must be handled by **long running jobs**. Note that this is a paid feature that is not available by default on scriptr.io's environments.

## Data processing


### Shards
When the data store grows to hundreds of thousands or millions of documents, the execution time of queries increases, which has a direct incidence of the latency of the application. A well known potential solution to this problem is sharding, which consists in horizontally or vertically splitting a data set into multiple data sets, to reduce the time needed to scan the data. By creating multiple data stores in a scriptr.io application, it is possible to create "shards" and distribute the data over the different stores. Note however that there is no built-in sharding mechanism in scriptr.io, which means that data distribution and 

### Incremental data aggregation

### Use the right data store type

## Increase capacity
