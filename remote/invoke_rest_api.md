# How to invoke a remote REST API from a script?

It is very simple to invoke third party REST APIs from within a script, using scriptr.io's **http** module and its **request()** function.

```
var http = require("http");
var requestParams = {}; // details in the below sections
var resp = http.request(requestParams);
```
The **request()** function needs you to provide some parameters to configure the http request to issue: url, params, method, headers, bodyString, etc.

The response return by the invocation of **request()** has the following structure:
```
{
  "status": "some_http_status", // status as returned by the remote API (200, 400, 404, 500, etc.)
  "headers": { // headers returned by the remote API
    
    ...
  },
  "body": "..."", // stringification of the data returned by the API 
  "timeout":"false" // indicates if the request timeout out or not
}
```

**IMPORTANT**: the body field always contained stringified data. You will have to parse it in your script.

The below sections provides cover different scenarios through code examples. In the latter, we will be using an online test API (https://fakerestapi.azurewebsites.net/api/Books).

## Issuing a Get request

In this example, we invoke an API operation that lists books (returns an array of books). The API requires us to specify the encoding we accept on our end. We will instruct it to send us data in the JSON format.

```
var http = require("http");
var requestParams = {
  "url": "https://fakerestapi.azurewebsites.net/api/Books",
  "headers": {
    "Accept": "application/json"
  }

}; 

var resp = http.request(requestParams);
if (resp.status == "200") {

  // lets parse the body of the response
  var bookList = JSON.parse(resp.body);
}
```



