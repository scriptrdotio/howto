# How do I retrieve my persisted data?

- Scriptr.io provides you with a NoSQL database that allows you to save data into key/value structures called "documents"
- To manipulate documents from within a script, you need to require the native "document" module, which provides very straitghtforward and simple functions.

## Retrieve data by document key

The simplest way to retrieve persisted data is by using the identifier of the document into which these data were pesisted. For that, you just need to invoke the **get()** method of the document module, passing a document key.
From within a script opened in the scriptr.io [workspace](https://www.scriptr.io/workspace), you can type the following:

```
var document = require("document");
var resp = document.get("43C5AFC7BDC265828EC53056731512FB");
```
- The object returned by **get()** contains a metadata section and a result section
- If successful, metadata.status will be set to "success" and result will contain the document (all your persisted fields + metadata fields, such as key, creator, creationDate, versionNumber, "meta.types", etc.)
- If unsuccessful, metadata.status will be set to "failure".

```
// successful get (example)
{
		"result": {
			"key": "43C5AFC7BDC265828EC53056731512FB",
			"versionNumber": "1.0",
			"temperature": "22.0",
			"humidity": "52.0",
			"time": "2018-10-10T00:00:00+0000",
			"creator": "scriptr",
			"lastModifiedDate": "2018-10-17T07:24:49+0000",
			"lastModifiedBy": "scriptr",
			"creationDate": "2018-10-17T07:24:49+0000",
			"latest": "1.0",
			"meta.types": {
				"temperature": "numeric",
				"humidity": "numeric",
				"time": "date",
				"creator": "string",
				"lastModifiedDate": "date",
				"lastModifiedBy": "string",
				"creationDate": "date",
				"versionNumber": "numeric",
				"key": "string",
				"latest": "numeric"
			}
		},
		"metadata": {
			"status": "success"
		}
}

// unsuccessful get (example)
{
		"metadata": {
			"status": "failure",
			"statusCode": 404,
			"errorCode": "DOCUMENT_NOT_FOUND",
			"errorDetail": "The document key [43C5AFC7BDC265828EC53056731512FA] was not found."
		}
}
```

## Can I query my peristed data based on conditions?

Yes,
- Scriptr.io has a simple yet powerful queyring syntax that you can use to query your data, using the **query()** function of the document module.
- When invoking this method, there are two mandatory parameters to pass:
  - The "query" parameter, which contains the query expression
  - The "fields" parameter, which specifies the document fields to return

```
var document = require("document");
var queryExpression = "temperature<numeric> >= 20 and humidity<numeric> < 60";
var queryObj = {
    query: queryExpression,
    fields: "temperature, humidity" // use "*" to return all fields
};

return document.query(queryObj);
```
