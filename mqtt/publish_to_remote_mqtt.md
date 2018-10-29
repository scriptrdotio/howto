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

When using mqtts, you will probably have to provide a client certificate, a root CA or both. These parameters, along with other optional parameters (username, password, key) are provided to the mqtt client through the **options** parameter of **mqtt.getInstance()** 

The free online broker we are using in these examples expects a root CA when connecting on port 8883. We will assume that our root CA file is attached to a document, which we will retrieve and pass to the mqtt client.

```
var document = require("document");
var mqtt = require("mqtt");
// In our example, the root CA file is persisted as an attached file of a document 
var file = document.getAttachment("mosquitto_ca", "mosquitto.org.crt", {fieldName:"apsdb_attachments", "versionNumber": "1"});
var options = {
  rootCa: file  
};
var mqttClient = mqtt.getInstance("mqtts://test.mosquitto.org:8883", options); // You should add the mqtts:// when using TLS
return mqttClient.publish("iotdemos.scriptr.io", JSON.stringify({"fan":"on"}));
```
# More

- Read more about the [mqtt.getInstance() options](https://www.scriptr.io/documentation#documentation-mqtt-getInstance-endpointgetInstance)
- Read more about how to [get attached files from documents]()
