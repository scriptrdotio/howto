# How to persist data?

- Scriptr.io provides you with a NoSQL database that allows you to save data into key/value structures called "documents" 
- To persist data into document from within a script, you need to require the native "document" module

```
var document =  require("document");
```
## Create a document

From the scriptr.io [workspace](https://www.scriptr.io/workspace)

```
var document =  require("document");
var obj = {
  temperature: 22,
  humidity: 52,
  time: "2018-10-10"
};

var resp = document.create(obj);
```

- The object returned by **create()** contains a metadata section and a result section
- If successful, metadata.status will be set to "success" and result.document.key will contain the document key (identifier)
- If **save()** fails, metadata.statust will be set to "failure" and no result is returned

```
// successful create (example)
{
  "result": {
    "document": {
      "key": "361C349B24E8BF0DDFDA2AC8287B83DE",
      "versionNumber": "1.0"
    }
  },
  "metadata": {
    "status": "success"
  }
  
// unsuccessful create (example)
{
  "metadata": {
    "status": "failure",
    "statusCode": 400,
    "errorCode": "DUPLICATE_DOCUMENT_KEY",
    "errorDetail": "A request is sent to create a document with a key that already exists"
  }

```

## Update a document

Simply use the **update()** function of the document module, passing a structure containing the document key and the fields to update

```
var document =  require("document");
var obj = {
  key: "361C349B24E8BF0DDFDA2AC8287B83DE",
  temperature: 24,
  humidity: 52,  
  time: "2018-10-10"
};

var resp = document.update(obj);
```

## Specify the data types

By default, scriptr.io persists the values as strings. You can specify your data types using the "meta.types" field. The available data types are numeric, string (*default*), text, date (yyyy-mm-dd or yyyy-mm-ddThh:mm:ss+0000) and geospatial (lat:long, ex: 12.1234,12.1234)

```
var document =  require(document);
var obj = {
    temperature: 22,
    humidity: 52,
    time: "2018-10-10",
    location: "40.7775,-73.9710",
    "meta.types": {
        temperature: "numeric",
        humidity: "numeric",
        time: "date",
    	location: "geospatial"
    }
};

var resp = document.create(obj);
```

## Delete a document

Deleting a document is very easy. Simply pass the corresponding document key to the delete() function of the document module.
```
var document =  require(document);
var resp = document.delete("F12D44FF38DF5C30CE8D41E6EC20D498");
```

# More

Read more about the document module in our [documentation](https://www.scriptr.io/documentation#documentation-documentdocumentModule).
