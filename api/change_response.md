# How to change the standard response structure of my API?

By default, scriptr.io wraps anything you return from a script into a predefined structure divided into two sections: 
- a metadata section, containing a status code and, in the case or the occurence of an error, an error code and an the error deails that 
- a result section, which contains whatever your script returned (in case no error was thrown)

Sample script response, no error
```
{
	"metadata": {
		"requestId": "f59d7b0a-50bb-4307-a4a4-6c3e2865d95d",
		"status": "success",
		"statusCode": "200"
	},
	"result": "hello"
}
```
Sample script response, error occurred
```
{
	"metadata": {
		"status": "failure",
		"statusCode": 400,
		"errorCode": "DUPLICATE_CHANNEL",
		"errorDetail": "The channel [internal_topic] already exists."
	}
}
```
However, there are cases where you would like to take control of the returned structure and provide your own customized response.
The way to do that is by leveraging the native **response** object from within your API.

## The reponse object

The **response** object allows you to specify your own http response headers (**response.setHeader()**) and to write (**response.write()**) into the response stream:
```
if (!request.parameters.temperature) { // send a custom error message if an expected parameter is not found in the request
    
    response.setHeader("status", "400");
    response.setHeader("Content-Type", "text/javascript");
    response.write(JSON.stringify({"msg":"Missing_Parameter - temperature"}));
    response.flush();
    response.close();
    return;
}

// Send custom response message otherwise
response.setHeader("status", "200");
response.write("ok");
response.flush();
response.close();
```

## CORS settings

Scriptr handles the setting of the CORS configuration in the defaut response. If you need to override the default response and send your own custom one as in the above example, you should also consider sending the CORS configuration in the geader of your response.
In the below example, we're specifying that our settings accept requests from any domain:

```
// ... some code here
response.setHeader("Content-Type", "text/javascript");
response.setHeader("Access-Control-Allow-Origin", "*");
response.write("write_something");
response.flush();
response.close();
```
