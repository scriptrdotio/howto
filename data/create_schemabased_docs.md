# How to apply automatic validation (schemas) on my data

- Scriptr.io provides you with a NoSQL database that allows you to save data into key/value structures called "documents" 
- To persist data into document from within a script, you need to require the native "document" module
- To apply automatic validation, you need to specify a schema when creating a document

## Create a schema-based document

*Note: In the below, we are using the "smart_building" schema created in [this howto](create_schema.md)*

From the scriptr.io [workspace](https://www.scriptr.io/workspace)

```
var document =  require(document);
var obj = {
  temperature: 22,
  humidity: 52,
  timestamp: 1539963132423,
  deviceid: "dev012345678",
  "meta.schema": "smart_building"
};

var resp = document.create(obj);
```
Notice that you have to pass the "meta.schema" field to instruct scriptr.io that the new document should verify the validations and constraints defined in the "smart_building" schema.

- The object returned by **create()** contains a metadata section and a result section
- If successful, metadata.status will be set to "success" and result.document.key will contain the document key (identifier)
- If **save()** fails, metadata.statust will be set to "failure" and no result is returned

```
// successful create (example)
{
  "result": {
    "document": {
      "key": "6D73404F88A6A12363CB1FC404A76C85",
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

## Update a schema-based document

Simply use the **update()** function of the document module, passing a structure containing the document key and the fields to update.
**You do not need to specify the schema again**

```
var document =  require(document);
var obj = {
  key: "6D73404F88A6A12363CB1FC404A76C85",
  temperature: 22.5,
  humidity: 52,  
  time: "2018-10-10"
};

var resp = document.update(obj);
```
