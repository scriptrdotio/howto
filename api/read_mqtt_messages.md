# How to read the messages sent to my API through mqtt?

- Any script you write in scriptr.io is by default turned into a secure and scalable API that is invokable via http (in addition to webockets, mqtt and amqp).
- The important thing to remember is that any script can retrieve the parameters it receives using the native request object that allows you to retrieve information about the request, including the conveyed parameters.

## Expected mqtt messages structure

When you **directly invoke** a script via mqtt, you need to adopt a predefined message structure in JSON:
```
{
"method":"path/to/script",
"params":key/value pairs
}
```
The **method** fied contains the path to the script and the **params** field contains a key/value pairs payload (no nested objects allowed). Example:
```
{
"method":"tutorials/howto/api/mqtt_receive_json",
"params":{"temperature":22, "humidity":52}
}
```
In the target script, the message payload is automatically delivered to in the native **request.parameters** object.
```
var payload = request.parameters; // using the above message example, 'payload' will contain: {"temperature":22, "humidity":52}
```

# More
- [How to publish an mqtt message directly to one of my APIs]()
- More on [using scriptr.io as an mqtt broker]()
