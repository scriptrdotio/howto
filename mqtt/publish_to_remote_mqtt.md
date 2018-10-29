# How to publish a message to a remote mqtt broker from a script?

Very simple. This is what you need to do:

- Require the **mqtt** module
- Use the module to get an instance of the mqtt client for a given **endpoint configuration** (the remote mqtt broker you are targeting)
- Invoke the **publish()** method of the mqtt client, passing the topic and the message

For the sake of the example, we will use a [free online mqtt test broker](https://test.mosquitto.org/). You can replace it with any other mqtt broker you have access to.

## Publish using mqtt 

```
var mqtt = require("mqtt");
var options = {username:"blah", password:"blah"}; // no credentials are actually required for the remote test broker we're using in this example
var mqttClient = mqtt.getInstance("test.mosquitto.org", options); 
if (mqttClient.metadata) {
    return mqttClient;  // failure message
}

return mqttClient.publish("io.scriptr.mqtt", JSON.stringify({"fan":"on"}));
```

**Note**: the message you send should be a string, plain text or stringified JSON

## Publish using mqtts

- When using mqtts, you might have to provide a client certificate, a root CA or both. These are passed along with the **options** parameter of **mqtt.getInstance()** 
- The free online broker we are using in these example expects root CA when connecting on port 8883 
- We will assume that our 

