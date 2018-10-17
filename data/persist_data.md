# How do I persist data?

- Scriptr.io provides you with a NoSQL database that allows you to save data into key/value structures called "documents" 
- To persist data into document from within a script, you need to require the native "document" module

```
var document =  require(document);
```
## Create a document

From the scriptr.io [workspace](https://www.scriptr.io/workspace)

```
var obj = {
  temperature: 22,
  humidity: 52,
  time: "2018-10-10"
};

var resp = document.create(obj);
```

- The object returned by **create()** contains a metadata section and a result section
- If successful, metadata.status will be set to "success" and result.key will contains the document key (identifier)
- If **save()** fails, metadata.statust will be set to "failure" and no result is returned

```
// successful create

```

#More
Read more about the document module in our [documentation](https://www.scriptr.io/documentation#documentation-documentdocumentModule).
