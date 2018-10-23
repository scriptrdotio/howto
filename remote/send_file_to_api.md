# How to send a file to a remote REST API?

- It is very simple to invoke third party REST APIs from within a script, using scriptr.io's http module and its request() function
- Read more about [how to invoke remote REST APIs from a script](https://github.com/scriptrdotio/howto/blob/master/remote/invoke_rest_api.md)

## Retrieving a file stored in a document

(Read more on [how to persist files sent to my API via http?](../data/upload_files.md))

Assume we have persisted a file into a document (the file is "attached" to the document):
- If the document is not bound to a schema, the field name of the file is **attachments**
- If the document is bound to a schema, the field name is whatever is specified in the latter

Let's agree that in our example, our the file is attached to a document under the "camera_snapshot" field and assume that the identifier (the key) of our document is "AAFE8C24CC9B7D5E275143DADF228CD5".

The get a file that is attached to a document, we just need to require the **document** module and invoke the **getAttachment()** function, specifying the key of the targetted document.

```

```

## Sending a file to a remote REST API


