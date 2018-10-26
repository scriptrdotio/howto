# How to subscribe one or may scripts to a remote mqtt topic?

Assume some devices are publishing data to a third party mqtt topic and that you need to broadcast these messages to one or many of your scripts.
The following steps tell you how to easily do that in scriptr:

- Create an mqtt endpoint
- Create a channel
- Create a bridge between the endpoint and the channel
- Subscribe the script(s)

For the sake of the example, we will use a free [online mqtt test broker](https://test.mosquitto.org/). 
You can replace it with any other mqtt broker you have access to.


