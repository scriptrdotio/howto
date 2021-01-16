# Mediator

Along with the Broker, the Mediator allows for the implementation of an event driven architecture. As opposed to the Broker that favors choreography, i.e. collaboration among software components, the Mediator relies on orchestration, ranging from the centralization of a few event/message routing rules to the full definition of a business process. The steps of the process are usually implemented by different software components that consume events sent by the mediator and optionally generate events in response. Events are used by the mediator to move forward in the process. The Mediator pattern is mainly used in SOA architectures, and commonly implemented as an Enterprise Service Bus (ESB).

The main constituants of the Mediator patterns are : (1) the event queue, which buffers incoming events that trigger orchestrations, (2) the mediator, in charge of orchestrating the execution by either forwarding the events to channels or generating new events, (3) the event channels and (4) the event processors that process the events and optionally generate other events into the mediator's queue. 

![mediator](./mediator.PNG)

*Figure 1 - The Mediator Pattern*

# Channels

Please refer to this section to see how to create channels and queues in scriptr.io.



