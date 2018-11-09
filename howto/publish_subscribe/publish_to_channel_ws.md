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

The value of the **params.message** field can be text or a JSON object (simple or nested). 

## Create a channel

A channel is a generic publish/subscribe mecanism. Scripts or remote clients can publish or subscribe to it using any of the supported messaging protocols (websockets, mqtt, amqp). Any published messages is automatically broadcast to all subscribers. To create a channel:

- In the [workspace](https://www.sriptr.io), click on your username in the top-right corner of the screen and select Settings
- Click on the **Channels** tab then click "+Add Channel"
- Enter a name for your channel. Do not check the boxes if you do not want to authorize non authenticated (anonymous) subscriptions or publications
