# How to retrieve my persisted data?

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

## Can I query my persisted data based on criteria?

Yes,
- Scriptr.io has a simple yet powerful queyring syntax that you can use to query your data, using the **query()** function of the document module.
- When invoking this function, there are two mandatory parameters to pass:
  - The "query" parameter, which contains the query expression
  - The "fields" parameter, which specifies the document fields to return

```
var document = require("document");
var queryExpression = "temperature<numeric> >= 20 and humidity<numeric> < 60";
var queryObj = {
    query: queryExpression,
    fields: "temperature, humidity" // use "*" to return all fields
};

var resp = document.query(queryObj);
```

The output of the **query()** function is an object that contains a metadata and a result section 
- When query() is successful, metadata.status is set to "success" and result contains a "document" field that is an array of documents
- The "document" array can be empty if no document matching the query criteria was found
- By default, a maximum of 50 documents is returned 
- When query() is unsuccessful, metadata.status is set to "failure"

```
// successful query (example)
{
	"result": {
		"documents": [
			{
				"key": "43C5AFC7BDC265828EC53056731512FB",
				"versionNumber": "1.0",
				"temperature": "22.0",
				"humidity": "52.0"
			}
		]
	},
	"metadata": {
		"status": "success"
	}
}

// unsuccessful query (example)
{
	"metadata": {
		"status": "failure",
		"statusCode": 400,
		"errorCode": "INVALID_QUERY_REQUEST",
		"errorDetail": "The query request must contain either requested fields, a count, or an aggregate expression."
	}
}

```

### How do I count the number of documents matching given criteria?

Just pass the **count** field set to true in the query object. The result will contain the count field, in addition to the document field.

```
var document = require("document"); 
var queryExpression = "temperature<numeric> >= 20 and humidity<numeric> < 60";
var queryObj = {
    query: queryExpression,
    fields: "key", 
    count: true
};

var resp = document.query(queryObj);
```
Returns something similar to the following: 
```
{
	"result": {
		"count": "1",
		"documents": [
			{
				"key": "43C5AFC7BDC265828EC53056731512FB",
				"versionNumber": "1.0"
			}
		]
	},
	"metadata": {
		"status": "success"
	}
}
```

### What about query results pagination?

Scriptr.io paginates your requests automatically and returns a maximum of 50 documents per page. 
- You can control the max number of documents to return per page using the **resultsPerPage** parameter in your query (it is limited to a max of 50)
- You can specify the index of the page you need using the **pageNumber** parameter in your query

```
var document = require("document"); 
var queryExpression = "temperature<numeric> >= 10";
var queryObj = {
    query: queryExpression,
    fields: "temperature, humidity", 
    count: true,
    pageNumber: 2, // get the second page of results
    resultsPerPage: 10 // return a max of 10 documents per result page
};

var resp = document.query(queryObj);
```

### Can I use aggregation functions when querying my data?

Sure,
- Just pass one of **SUM($fieldName)**, **MAX($fieldName)**, **MIN($fieldName)**, **AVG($fieldName)** to the **aggregateExpression** parameter of your query 
- Specify the aggregation scope (all documents or page results) by setting one of **aggregateGlobal** or **aggregatePage** to "true" respectively
- Omit the **fields** parameter if you only need he aggregated value

```
// Assume we need the max recorded temperature 
var document = require("document"); 
var queryExpression = "temperature<numeric> >= 10";
var queryObj = {
    query: queryExpression,
    aggregateExpression: "MAX($temperature)",
    aggregateGlobal: true // aggregate on all matching documents
};

va resp = document.query(queryObj);
```
Returns a response similar to:
```
{
	"result": {
		"aggregate": {
			"pageScope": {
				"value": "25.0"
			},
			"globalScope": {
				"value": "25.0"
			}
		},
		"documents": []
	},
	"metadata": {
		"status": "success"
	}
}
```

# More
You can learn more about querying your data in our [documentation](https://www.scriptr.io/documentation#documentation-query-documentquery)
