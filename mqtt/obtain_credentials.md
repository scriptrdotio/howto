# How to obtain credentials to publish mqtt messages to my scriptr.io account?

You can obtain these from the scriptr.io [workspace](https://www.scriptr.io/workspace). Click on the arrow near your username in the top-right corner, then select the **Messaging Protocols** option. In the resulting configuration form, do the following:

- Select MQTT from the Protocol drop-down
- Select a device from the Device drop-down in the Credentials section. A username and a password are automatically generated for that device. Your client application or physical device will use these when sending messages to your scriptr.io account
- Select a channel used by publishers to send messages and by subscribers to consume them. Selecting a channel displays two topics:
- The **/message** topic, to be used when **broadcasting an mqtt message to many subscribers** 
- The **/invoke** topic, to be used when **invoking a specific script via mqtt**

