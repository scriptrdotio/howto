# How to invoke my API (scripts) using websockets?

By default, any script you write is automatically deployed as a secure and scalable API, which can be invoke through http, websockets, mqtt or amqp

A remote client that needs to invoke a script using websockets should connect to the following URL

```
wss://api.scriptrapps.io/<AN_AUTHENTICATION_TOKEN> 
```

Notice that the client should append an authentication token to the URL. Read this [howto](https://github.com/scriptrdotio/howto/blob/master/api/obtain_auth_token.md) if you don't know how to obtain authentication tokens.

The message to send is a JSON structure with the following format:

```
{
  "method":"absolute_path_to_script",
  "params":your_params_as_json_or_string
}
```

**Example**

```
{
  "method":"tutorials/howto/api/someAPi", // the absolute path does not start with '/'
  "params":{"temperature":22, "humidity":43}
}
```

## Example of a JavaScript websocket client

- You can run the below code in a browser.
- The value of the **params** field can be text or a simple key/value pairs JSON object (no nested objects). If you wish to send nested objects, check [how to publish data to scriptr using websockets?]()

```
// connect to scriptr
var connection = new WebSocket("wss://api.scriptrapps.io/YOUR_AUTH_TOKEN");

// When the connection is open, send some data to your API on scriptr
connection.onopen = function () {
  
  var msg  = {
  	"method":"tutorials/howto/api/websocket_receive_json", // replace with relative path to your script
    "params": {"temperature":22, "humidity":43} // replace with any payload
  };
  
  connection.send(JSON.stringify(msg)); // NOTICE THAT YOU NEED TO STRINGIFY THE MESSAGE
};

// Log errors
connection.onerror = function (error) {
  console.log('WebSocket Error ' + error);
};
```

## How to read the received message in the script?

On the scriptr side, your script will receive the **params** part of the message that was sent by the JavaScript client.
These parameters are obtained from the native **request.parameters** object:

```
var temperature = request.parameters.temperature;
var humidity = request.parameters.humidity;
// etc.
```
