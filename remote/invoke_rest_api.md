# How to invoke a remote REST API from a script?

It is very simple to invoke third party REST APIs from within a script, using scriptr.io's **http** module and its **request()** function.

```
var http = require("http");
var requestParams = {}; // details in the below sections
var resp = http.request(requestParams);
```
The **request()** function needs you to provide some parameters to configure the http request to issue, such as: **url, params, method, headers, bodyString, etc.**

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

The below sections provides cover different scenarios through code examples. In the latter, we will be using public online test APIs.

## How to issue a GET request

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In this example, we invoke an API operation that lists books (returns an array of books). The API requires us to specify the encoding we accept on our end. We will instruct it to send us data in the JSON format
- Notice that we are specifying the url, method and headers properties

```
var http = require("http");
var requestParams = {
  "url": "https://fakerestapi.azurewebsites.net/api/Books",
  "method": "get",
  "headers": {
    "Accept": "application/json"
  }

}; 

var resp = http.request(requestParams);
if (resp.status == "200") {

  // let's parse the body of the response
  var bookList = JSON.parse(resp.body);
  return bookList;
}
// ... more code

```

## How to issue a GET request with parameters

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In this example we invoke send an id parameter to an API operation that returns the book that matches the provided ID
- Notice that we are specifying the url, method and headers properties

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

    // let's parse the body of the response
    var book = JSON.parse(resp.body);
    return book;
}
// ... more code

```

## How to issue a POST request with application/json content

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In this example we invoke an API operation to create a new book (the API responds with the data about the book it created). The new book's data is sent as a JSON object 
- Observe that in that case we are sending a **stringifed JSON** in the **bodyString** property
- Also note that we are sending the content-type in the headers property

```
var http = require("http");
var newBookData = {

  "ID": 1000,
  "Title": "Mastering scriptr.io",
  "Description": "Become an expert in scriptr.io",
  "PageCount": 100,
  "Excerpt": "string",
  "PublishDate": "2018-10-23T08:02:26.482Z"
};

var requestParams = {
    "url": "https://fakerestapi.azurewebsites.net/api/Books",
    "method": "post",
    "headers": {
        "Accept": "application/json",
        "Content-Type": "application/json"
    },
    "bodyString": JSON.stringify(newBookData)
}; 

var resp = http.request(requestParams);
if (resp.status == "200") {

    // lets parse the body of the response
    var createdBook = JSON.parse(resp.body);
    return createdBook;
}
```

## How to issue a POST request with application/x-www-form-urlencoded or multipat/form-data content

- Open your [workspace](https://www.scriptr.io/workspace) and create a new script
- In that case, you can pass the content as key/value pairs using the **params** property

```
var http = require("http");
var requestParams = {
    "url": "https://jsonplaceholder.typicode.com/posts",
    "method": "post",
    "headers": {
        "Content-Type": "application/x-www-form-urlencoded"
    },
    "params": { // when posting with content-type "application/x-www-form-urlencoded" or "multipart/form-data", use params
        "topic": "scriptr.io",
        "subject": "posting data"
    }
}; 

var resp = http.request(requestParams);
if (resp.status == "201") {

    // lets parse the body of the response
    var post = JSON.parse(resp.body);
    return post;
}
```
# More

Read more about the http module in our [documentation](https://www.scriptr.io/documentation#documentation-httphttpModule)
