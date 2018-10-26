# How to subscribe one or many scripts to a remote mqtt topic?

Assume some devices are publishing data to a third party mqtt topic and say that you need to broadcast these messages to one or many of your scripts. The following steps tell you how to easily do that in scriptr:

- Create an mqtt endpoint
- Create a channel
- Create a bridge between the endpoint and the channel
- Subscribe the script(s) to the channel
- Read the incoming messages

For the sake of the example, we will use a free [online mqtt test broker](https://test.mosquitto.org/). 
You can replace it with any other mqtt broker you have access to.

## Create an mqtt endpoint

- Open the [workspace](https://www.scriptr.io/workspace) and click on your username in the top right corner of the screen
- From the drop-down list, select **Settings** then click on the **External Endpoints** tab
- Click on +Add External Endpoint Configuration

![New Endpoint](./images/new_endpoint.png)

*Image 1*

- Select MQTT from the **Type** drop-down (or select MQTTS)
- Enter a name in the **Name** field that will be used to identify the endpoint
- In the **URL** field, enter the URL of the mqtt broker to use (e.g. test.mosquitto.org)
- You can leave the **Port** field empty if the target broker is used the default ports (1883 for mqtt or 8883 for mqtts)
- In the **Topic**, enter the name of a topic to subscribe to, on the remote broker (if you are using the aforementioned test broker, just type any name - try to make it unique to avoid collisions with others, e.g. "com.yourcomany.mqtt") 
- In the **Username** and **Password** fields, respectively enter your username and password provided by the remote broker (if you are using the test broker, you do not have to fill this fields)
- In the Client id field, enter a unique identifier (to avoid collisions with others)
- If you have selected MQTTS, you might have to fill the CA, Certificate and Private Key fields, depending on the mqtt broker you are using)

![MQTT Endpoint](./images/mqtt_endpoint.png)

*Image 2*

## Create a channel

A channel is a generic publish/subscribe mecanism. Scripts or remote clients can publish or subscribe to it using any of the supported messaging protocols (websockets, mqtt, amqp). Any published messages is automatically broadcast to all subscribers.

To create a channel:

- Open your workspace, then click on your username in the top-right corner of the screen and select Settings
- Select the Channels tab then click "+Add Channel"
- Enter a name for your channel. Do not check the boxes if you do not want to authorize non authenticated (anonymous) subscriptions or publications

![MQTT Channel](./images/new_channel.png)

*Image 3*


