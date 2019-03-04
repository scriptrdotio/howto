# What is scriptr.io?

In a few words: 

- Scriptr.io is a cloud-based platform for developing and executing IoT solutions. It offers a set of tools, components and APIs to reduce the effort and time to market IoT applications
- Everything you code is automatically deployed in a secure and scalable cloud environment, releaving you from DevOps operations
- Scriptr.io is a managed service, so we take care of monitoring the health of your applications
- Scriptr.io runs on the cloud, and upon request: on premises (data centers) and even at the Edge
- Scriptr.io is an extremely flexible and efficient IoT Middleware and communication broker, enabling collaboration among heterogenous platforms and protocols.

![scriptr.io features at a glance](./scriptr.io-iot-middleware.png)

## How does it work?

- You can [sign-up for a free account](https://www.scriptr.io/register) to start exploring scriptr.io
- Once registered, [sign-in](https://www.scriptr.io/login) and you will land in the [workspace](https://www.scriptr.io/workspace)
- The workspace is a web IDE that offers everything you need to start developing a full fledged IoT application 

## What can I do with scriptr.io from the workspace?

- Create APIs that can be invoked by remote clients (such as devices) over http, websockets, mqtt or amqp
- Implement application and business logic into reusable modules
- Invoke remote http REST APIs
- Persist data and files in a NoSQL data store
- Publish mqtt messages to remote mqtt topics
- Subscribe to remote mqtt topic
- Send amqp messages to remote amqp exchanges/queues
- Subscribe to remote amqp queues
- Create scheduled (cron) jobs 
- Broadcast messages
- Queue the execution of tasks
- Integrate with Big Data platforms using connectors
- Integrate with networks services and device management platform using connectors
- Integrate with legacy systems using connectors
- Broker messages among different protocols in real-time
- Create HTML/JavaScript user interfaces
- Create HTML/JavaScript dashboards
- **... and much more**

## What language is used for coding?

- Scripts are the main constructs in script. Whenever you click on **+New Script** in the [workspace](https://www.scriptr.io/workspace), you create a new **server-side** script. Coding scripts is done in **JavaScript**
- From a server-side script, you have access to an extensive list of scriptr.io modules, native objects and functions that offer powerful features. Since scripts are running on the server-side, **you do not have access to the DOM**
- It is however possible to create client-side HTML pages and JavaScript scripts. You can read more about this in the howto

## How and where is my code deployed?

As soon as you save a script in the Web IDE, it is automatically deployed on the cloud run-time and ready to be used.

## How to integrate with third party systems?

There are many ways to do this:
- Leverage our **bridges** to subscribe to remote topics and queues (mqtt, amqp, websockets, Azure IoT hub, AWS)
- Leverage our [connectors](https://github.com/scriptrdotio?tab=repositories)

[Back to the how to list](https://github.com/scriptrdotio/howto/blob/master/README.md)
