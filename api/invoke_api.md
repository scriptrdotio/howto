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
  "method":"aboslute_path_to_script",
  "params":your_params_as_json_or_string
}
```

Example

```
{
  "method":"tutorials/howto/api/someAPi", // the absolute path does not start with '/'
  "params":{"temperature":22, "humidity":43}
}
```
