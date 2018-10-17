# How to read the messages sent to my API through mqtt?

- Any script you write in scriptr.io is by default turned into a secure and scalable API that is invokable via http (in addition to webockets, mqtt and amqp).
- The important thing to remember is that any script can retrieve the parameters it receives using the native request object that allows you to retrieve information about the request, including the conveyed parameters.

## Supported MQTT messages

- Key/value pairs JSON objects (if you have many nested objects you will have to stringify them, e.g. {"msg": "{\"temperature\":22,\"humidity\":52,\"device\":{\"id\":123456,\"location\":\"40.7775,-73.971\"}}"})
- Text
- XML



go ahead an create a script in your scriptr.io [workspace](https://www.scriptr.io/workspace)
