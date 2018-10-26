# How to transform an XML payload to JSON and vice-vesra?


## Transform an XML payload to JSON

Use the **xmlToJson()** native function!

Try it: 

- Open the [workspace](https://www.scriptr.io/workspace) and click on New Script in the bottom left corner of the screen 
to create a new script
- Paste the below code in the script. The code invokes a remote test API that returns data in XML upon request (accept header),  
it then converts the XML response JSON using **xmlToJson()** and returns the converted value

```
var http = require("http");
var requestConfig = {
    "url": "https://fakerestapi.azurewebsites.net/api/Authors",
    "headers": {
        "accept": "application/xml"
    }
};

var resp = http.request(requestConfig); 
if (resp.body){
    return xmlToJson(resp.body); 
}

return resp.body;
```

## Transform a JSON payload to XML

Use the **jsonToXml()** native function!

Try it: 

- Open the [workspace](https://www.scriptr.io/workspace) and click on New Script in the bottom left corner of the screen 
to create a new script
- Paste the below code in the script

```
var json = {
    "Author": [
        {
            "FirstName": "First Name 1",
            "ID": "1",
            "IDBook": "1",
            "LastName": "Last Name 1"
        },
        {
            "FirstName": "First Name 2",
            "ID": "2",
            "IDBook": "1",
            "LastName": "Last Name 2"
        }
    ]
};

return jsonToXml(json);
```
