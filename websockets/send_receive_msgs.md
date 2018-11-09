# How to communicate with a websocket endpoint?

Scriptr allows you to send messages to and receive messages from a websocket endpoint. It is important to note that sending and receiving cannot be done from th same script.
Therefore, you will usually use one or many scripts to send messages to the endpoint and you will subscribe one or many scripts to receive messages from the websocket endpoint.
If multiple scripts are subscribed to the same websocket endpoint, any message sent my the latter will be broadcast to all the subscribed scripts.

## Create a websocket endpoint

From the [workspace](https://www.scriptr.io/workspace), click on your username on the top right corner of the screen. Select **Settings** then click on the **External endpoints** tab.
Click on **+Add** to create a new websocket endpoint:

- In the **Type** field, select WS or WSS (depending on the endpoint)
- In the **Name** field, enter a name for your endpoint 
- In the **URL** field, enter the URL of the endpoint
- In the **Port** field, enter the port. This is optional, only enter a value if the endpoint is not using nominal websocket ports
- In the **Authorization**, enter optional credentials

![New WebSocket endpoint](./images/websocket_endpoint.png)

*Image 1*

Click on the orange checkbox on the right to create the endpoint. 

## Sending a message to a websocket endpoint

Sending messages is done using the **publish()
