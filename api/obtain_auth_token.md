# How to obtain authentication tokens?

 Authentication tokens are used by remote clients that invoke your API (scripts) using http or websockets. They are also used internally to connect channels to bridges or to generate mqtt or amqp credentials for your remote clients.
 
 ## Account owner's authentication token
 
 When you registered to scriptr, an account was created for you on the platform and an authentication token was allocated to it. 
 To get your account token, open the [workspace](https://www.scriptr.io/workspace) the click on your username in the top right corner of the screen. In the drop-down list, click on **Account**.
 Select the **Info** tab (should be selected by default). Copy the value of the **token** field.
 
 ## User and Device authentication tokens

The account token token has a very high level of privileges and therefore, you should not distribute it and only use it for your own tests. To distribute tokens to remote clients, you should rather [create devices and users](https://github.com/scriptrdotio/howto/blob/master/acl/create_devices_users.md) and use the corresponding tokens.
