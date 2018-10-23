# How to send a file to a remote REST API?

- It is very simple to invoke third party REST APIs from within a script, using scriptr.io's http module and its request() function
- Read more about [how to invoke remote REST APIs from a script](https://github.com/scriptrdotio/howto/blob/master/remote/invoke_rest_api.md)

## Retrieving a file stored in a document

Assume we have persisted a file into a document (Read more on [how to persist files sent to my API via http?](../data/upload_files.md))
:
- The document key is "AAFE8C24CC9B7D5E275143DADF228CD5" 
- The name of the document field storing the file is "camera_snapshot"
- The file name is "110916_server_512x512.png" 

The get a file that is attached to a document, you just need to require the **document** module and invoke the **getAttachment()** function, specifying the key of the targetted document, the file name and the name of the document field holding the file.

```
var document = require("document");
var file = document.getAttachment("AAFE8C24CC9B7D5E275143DADF228CD5", "110916_server_512x512.png", {"fieldName":"camera_snapshot"});
return file;
```

**ATTENTION** notice in the above example that the field name is always passed as a property of an object

## Sending a file to a remote REST API

To invoke a remote API, you need to use the **http** module and invoke its **request()** method, passing all the required parameters. Let's update the above code sample to incorporate the invocation of a remote API

```
var http = require("http");
var document = require("document");
var file = document.getAttachment("AAFE8C24CC9B7D5E275143DADF228CD5", "110916_server_512x512.png", {"fieldName":"camera_snapshot"});
var params = { // Prepare the parameters to pass the http.request()

    "files" :{ // use the predefined "files" parameter name to store a map of file objects
        "some_param_name": file // replace some_param_name with a name that is expected by the remote API
    },
    "method":"POST",
    "url":"https://api.scriptrapps.io/tutorials/howto/data/save_file", // replace with a remote endpoint
};

var response = http.request(params);
return response;
````

As you can seem in the example, you can use the predefined **files** property name to specify a map of file objects to send to the remote API.

# More

- Read more on attachments in our [documentation](https://www.scriptr.io/documentation#documentation-get-attachmentgetAttachment)
- Read more on the http module in our [documentation](https://www.scriptr.io/documentation#documentation-httphttpModule)
