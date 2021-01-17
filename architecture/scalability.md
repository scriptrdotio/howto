# Scalability

Scalability is always a concern in most enterprise-grade applications. While it is definitely possible to increase capacity, solution architects will evaluate design alternatives that maximize the available resources, before considering any capacity increase. In addition, increasing the capacity is not always the optimal solution to a performance problem due to a perfectible architecture. On that end, this document goes through a few options that can be assessed when implementing an application.

*Note:* In this document, we use the word *application* to refer to business logic deployed and executed on scriptr.io. We also use the words *request*, *message* and *event* interchangeably, to refer to any demand sent by a client application to the scriptr.io application.

## Asynchronous processing

It often appears that sychronous, request-reply and/or transactional processing are not necessary to tackle a given use cases, but they are actually used out of habit, leading sometimes to bloating the application by reserving a large part of the available resources. Therefore when designing an application, it is important to answer the following questions:
- Is there a large number of messages to process, whose emitters do not need an response immediately, but can be provided later with the outcome of their request?
- Is the execution time of the logic triggered by a request higher than a few seconds? Can it reach minutes or hours? 

If at least one of the answers to those questions is "yes", then asynchronous processing should definitely be considered.

### Queued jobs
The [Broker](./broker.md) and [Mediator](./mediator.md) architecture patterns can be used to handle the asynchronous execution of event-driven logic, by decoupling the message producers (e.g. client applications) from the message processors. More specifically, using job queues allow the latter to handle a very large number of messages, whose processing time is measured in seconds, at a more convenient pace.

### Long running jobs
When the processing of a message takes more than a few seconds and can span over minutes or even hours, then this type of message must be handled by **long running jobs**. Note that this is a paid feature that is not available by default on scriptr.io's environments.

## Data processing

Persisting and querying data can often become the bottleneck of an application. There is a few techniques however, that can postpone the fateful time at which an increase of capacity is necessary: 

### Shards
When the data store grows to hundreds of thousands or millions of documents, the execution time of queries increases, which has a direct incidence on the latency of the application. A well known potential solution to this problem is sharding (contraction of shared-nothing), which consists in horizontally or vertically splitting a data set into multiple **disjoint** data sets, to reduce the time needed to scan the data. 

By creating multiple data stores in a scriptr.io application, it is possible to create "shards" and distribute the data over the different stores. Note however that there is currently no built-in sharding mechanism in scriptr.io, which means that the logic to determine which data store to use to write/read data must be done at the level of the application. While this can increase the complexity of the latter, it can also dramatically improve its performance.

### Incremental data aggregation
Many scenarios, such as generating dashboard content and/or analytics, require performing data aggregations. When the type of aggregates is known in advance (e.g. generate reports hourly, daily, weekly, monthly, etc.), a good option is to perform the aggregation at ingestion time, via queued or long running jobs for example, or at regular intervals via scheduled jobs. Pre-processing the data will thus result in significant performance gain when generating dashboards and reports.

### Use the right data store type
Scrpitr.io provides general-purpose NoSQL data stores. While these are convenient to store application data, they might not fit all use cases, which can have a direct incidence on performance. For example, scriptr.io's NoSQL data store is not optimized for handling time-series nor for efficiently dealing with relational data. In similar cases, it might be wiser to persist the data into more specialized data stores, such as InfluxDB or MySQL for example, for which scriptr.io provides connectors that can be leveraged from within the code. 

## Increase capacity

It is always possible to ask for increasing the capacity of a dedicated environment. However, depending on the architecture of the solution, it might be more intersting to ask for the creation of multiple small dedicated environments, rather than increasing the capacity of the existing one. For example, if the solution is leveraging [Microservices](./microservices.md), then it might make sense to deploy each Microservice (or sub-sets of Microservics) on a small dedicated environment. This will result in distributing the load of the solution on the different environments and provide improved scalability.

# Solution Architecture Booklet ToC
- [Environment configuations](./environment_configurations.md) you can have on scriptr.io
- [Development life-cycle](./development_life_cycle.md)
- [Architecture patterns](./architecture_patterns.md)
- [Scalability](./scalability.md)
- [Security](./security)
