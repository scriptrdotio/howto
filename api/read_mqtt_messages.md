# How to read the messages sent to my API through mqtt?

- Any script you write in scriptr.io is by default turned into a secure and scalable API that is invokable via http (in addition to webockets, mqtt and amqp).
- The important thing to remember is that any script can retrieve the parameters it receives using the native request object that allows you to retrieve information about the request, including the conveyed parameters.

## Retrieving the message payload

TSimple: in the target script (your API), the message payload is automatically delivered to in the native **request.parameters** object.
```
var payload = request.parameters; 
```

# More
- [How to publish an mqtt message directly to a script?](./publish_mqtt_msgs_to_script.md)
- More on [using scriptr.io as an mqtt broker](https://www.scriptr.io/documentation#documentation-communicating-over-mqttScriptr.ioMQTTBroker)
