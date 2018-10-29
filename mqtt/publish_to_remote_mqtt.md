# How to publish a message to a remote mqtt broker from a script?

Very simple. This is what you need to do:

- Require the **mqtt** module
- Use the module to get an instance of the mqtt client for a given **endpoint configuration** (the remote mqtt broker you are targeting)
- Invoke the **publish()** method of the mqtt client, passing the topic and the message

For the sake of the example, we will use a [free online mqtt test broker](https://test.mosquitto.org/). You can replace it with any other mqtt broker you have access to.

```
var mqtt = require("mqtt");
var options = {username:"blah", password:"blah"}; // no credentials are required for the remote test broker we're using in the example
var mqttClient = mqtt.getInstance("test.mosquitto.org", options); 
if (mqttClient.metadata) {
    return mqttClient;  // failure message
}

return mqttClient.publish("io.scriptr.mqtt", JSON.stringify({"fan":"on"}));
```

- **Note 1**: the message you send should be a string, plain text or stringified JSON
- **Note 2**: in the above example, we're using mqtt. Resorting to mqtts requires passing a root CA  
