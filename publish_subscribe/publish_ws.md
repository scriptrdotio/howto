# How to publish data to scriptr using websockets?

You can publish a message to a scriptr channel from a websocket client using the Publish API. All published messages will be automatically broadcast to any subscriber of the channel.

A remote client will connect using the following URL

```
wss://api.scriptrapps.io/<AN_AUTHENTICATION_TOKEN> 
```

Notice that the client should append an authentication token to the URL. Read this [howto](https://github.com/scriptrdotio/howto/blob/master/api/obtain_auth_token.md) if you don't know how to obtain authentication tokens.

The message to send is a JSON structure that adopts the following format:

```
{
  "method":"Publish",
  "params":{
      "channel":"your_channel_name",
      "message":the_payload_text_or_json
   }
}
```

Example

```
{
  "method":"Publish",
  "params":{
      "channel":"websocketdotorg",
      "message": {"temperature":22, "humidity":43}
   }
}
```

The value of the **params.message** field is text or a JSON object (simple or nested). 

## Create a channel

A channel is a generic publish/subscribe mecanism. Scripts or remote clients can publish or subscribe to it using any of the supported messaging protocols (websockets, mqtt, amqp). Any published messages is automatically broadcast to all subscribers. To create a channel:

- In the [workspace](https://www.sriptr.io), click on your username in the top-right corner of the screen and select Settings
- Click on the **Channels** tab then click "+Add Channel"
- Enter a name for your channel. Do not check the boxes if you do not want to authorize non authenticated (anonymous) subscriptions or publications

## Example of a JavaScript websocket client

- You can run the below code in a browser.
- Notice that in the value of the **params.message** field is text or a **stringified** JSON object (simple or nested)
- Notice that the sent msg has to be stringified

```
var connection = new WebSocket("wss://api.scriptrapps.io/YOUR_AUTH_TOKEN");
// When the connection is open, send some data to the server
connection.onopen = function () {
  
  var msg  = {
    
  	"method":"Publish",
    "params": {
      "channel":"websocketdotorg", // replace with your channel name
      "message":JSON.stringify({"temperature":22, "humidity":43}) // replace with any payload
    }
  };
  
  connection.send(JSON.stringify(msg)); // NOTICE THAT YOU NEED TO STRINGIFY THE MESSAGE
};

// Log errors
connection.onerror = function (error) {
  console.log('WebSocket Error ' + error);
};

// Log messages from the server
connection.onmessage = function (e) {
  console.log('Server: ' + e.data);
};

```

## How to consume the messages from my scripts?

To let your scripts consume the messages that will be published to this channel, you need to subscribe them to the latter, which can be done in two different ways:

- From the user interface
- From the code of another script

### Subcribe a script to a channel from the user interface

- In the [workspace](https://www.sriptr.io), select the script you wish to subscribe to the channel, from the tree view on the left side of the screen
- In the editor area, click on the Subscribe button
- Subscribe to a channel by switching on the corresponding toggle

![Subscribe to channel](../websockets/images/subscribe_to_channel.png)

### Subcribe a script to a channel from the code of anoher script

Simply use the native subscribe() function in the code, passing the channel name and the absolute path to the script (note: do not start with "/")

```
// the below subscribed the "tutorials/howto/websockets/subscriber" to the "websocketdotorg" channel
var resp = subscribe("websocketdotorg", "tutorials/howto/websockets/subscriber");
```

### Reading the payload

On scriptr's end, the payload (the content of the "message" field) is available in the native **request** object:
- If the payload that was sent is in text format, it can be retrieved from **request.rawBody**
- If the payload that was sent is in JSON format (even if stringified), it can be retrieved from **request.body**

```
// Based on the JavaScript example above
var temperature = request.body.temperature;
var humidity = request.body.humidity;
```
