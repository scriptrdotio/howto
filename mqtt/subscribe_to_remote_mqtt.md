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



