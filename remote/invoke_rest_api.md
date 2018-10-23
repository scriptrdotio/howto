# How to invoke a remote REST API from a script?

It is very simple to invoke third party REST APIs from within a script, using scriptr.io's **http** module and its **request()** function.

```
var http = require("http");
var requestParams = {}; // details in the below sections
var resp = http.request(requestParams);
```
The **request()** function needs you to provide some parameters to configure the http request to issue: url, params, method, headers, bodyString, etc.

The response returned by the invocation of **request()** has the following structure:
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

## How to issue a GET request

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In this example, we invoke an API operation that lists books (returns an array of books). The API requires us to specify the encoding we accept on our end. We will instruct it to send us data in the JSON format

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

return bookList;
```

## How to issue a GET request with parameters

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In this example we invoke send an id parameter to an API operation that returns the book that matches the provided ID

```
var http = require("http");
var requestParams = {
    "url": "https://fakerestapi.azurewebsites.net/api/Books",
    "headers": {
        "Accept": "application/json"
    },
    "params": { // we use the "params" field to pass parameters
        "id":4
    }

}; 

var resp = http.request(requestParams);
if (resp.status == "200") {

    // lets parse the body of the response
    var book = JSON.parse(resp.body);
}

return book;
```

## How to issue a POST request with application/json content


