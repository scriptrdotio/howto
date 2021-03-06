# Security

Security is of paramount importance in software systems and applications. Scriptr.io makes no exception and deals with security at three levels: 
- [Authentication](./security.md#authentication)
- [Authorizations](./security.md#authorizations)
- [Encryption](./security.md#ecryption)

## Authentication

### Account owner

The owner of a scriptr.io account signs into the workspace (web IDE) using his account user name and password, which should never be shared with anyone. Since it is possible to create more than one application for a same account, the account owner has a specific **account owner authentication token** that will identify him against the application (more on this in the next sections). Those tokens should never be shared as well, and never be used within applications.

### User and device directory
Each application of a scriptr.io account has its own user and device directory. Directories are not shared across applications, which means that a device or a user who is identified in an application is unknown to other applications of the same scriptr.io account.

### Suspended users/devices
Any suspended user or device looses its rights to access your application during the suspension period.

### Credentials
Adding a new a user or a device into the directory can be done from the workspace or using the corresponding APIs. It requires providing a user name (respectively a device name) and a password that will be used to generate an **authentication token**. If a token is lost or corrupted, a new token can be regenerated, which automatically invalidates the other one. It is also possible to modify the password, which leads to the automatic regeneration of an authentication token, and the invalidation of the former password and token respectively.

Users and devices (hereafter refered to as *client applications*) access your application by creating authenticated and secure connections with and/or issuing authenticated requests or message. The mechanism to adopt differs depending on the communication protcol that is used:

#### HTTP
 Client applications can access your application by issuing authenticated http requests to it's API. A request is authenticated by scriptr.io if it contains a valid **authentication token** pertaining to the directory of the targeted application. 

User interfaces served by your application can also leverage the [Login component](https://github.com/scriptrdotio/login), which allows users to sign-in by entering their user name and password in a login form. The login component will generate a session token, automatically redirecting users to the login form upon session expiration.

#### MQTT 
Client applications that invoke your application's API over mqtt(s) should authenticate using a **username and password generated by scriptr.io**, used when establishing the mqtt connection with scriptr.io. For more, please refer to [this document](https://www.scriptr.io/documentation#documentation-communicating-over-mqttScriptr.ioMQTTBroker).

#### AMQP
Similarly, client applications connecting to your application's API over amqp should authenticate by providing a **username and password generated by scriptr.io**, used when establishing the amqp connection. For more, please check this [document](https://www.scriptr.io/documentation#documentation-communicating-over-amqpScriptr.ioAMQPBroker).

#### WebSockets
Client applications interacting with your application's API via websockets authenticate with a valid **authentication token** when [establishing the connection](https://www.scriptr.io/documentation#documentation-realtimecommunicationReal-timeCommunication).

### Authenticating against third party systems
Your application will probably interact with third-party systems against which it should also authenticate. Authentication will strongly depend on the technique used by the third party. 

In addition to using traditional authentication means (bearer token, username/passwords, etc.) when issusing requests/messages to those third parties, you can leverage more advanced techniques that are natively available in scriptr.io and directly usable from within your scripts:

- OAuth
- Client SSL/TLS certificates
- JSON Web Tokens.

## Authorizations
Scriptr.io handles authorisations via **Access Control Lists** (ACL) at two levels:
- scripts: manage permissions on the execution of the logic in the scripts. For more on how to create ACLs for scripts please read [this](../acl/restrict_access_to_api.md)
- documents: manage permissions on your data, at the field level, either for reading and/or writing. For more on how to create ACLs for documents, please read [this](../acl/protect_data.md)

ACLs are lists of users, devices, groups and roles that are authorized on a given resource (script or data). Users, devices, groups and roles that are not part of the ACL of a given script, document or document field will get no access to the resource.

## Roles and Groups

### Roles
ACL can contain one of the predefined roles: 
- scriptr: refers to the owner of the application 
- authenticated-users: refers to all non suspended users and devices in the directory
- anonymous: means that no authentication is required to access the corresponding resource
- nobody: means that the corresponding resource is forbidden, even for the scriptr role.

### Groups
Groups can contain users, devices or other groups. It is a convenient ways of associating users and devices to the same resources. It is recommended to use groups as much as possible when creating ACLs.

### Authorization context
It is important to note that, by default, a request or message that has been authenticated an authorized to execute a script will run the latter **using the application's owner authorizations** (scriptr role), which means that any subsequent action, including data manipulation will take place within this authorization context. Therefore, if you want to make sure to execute the script (and subsequent actions) in the context of the user/device that issued the request/message, you must use **impersonation**, which is actually [very simple to do with script.io](../acl/protect_data.md#how-do-i-access-data-using-the-request-initiator-credentials).

## Encryption
In-flight data will be encrypted when sending requests/messages to your application over a TLS/SSL connection. Documents (data) are not encrypted by defaults, but you can leverage the provided encryption libraries to encrypt your data if needed. Note that scriptr.io will ask for TLS whenever an authentication token is passed over a non secure communication, and reject the request.

[Back to Solution Architect Booklet ToC](./solution_architect_booklet.md#toc)
