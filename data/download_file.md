# How to download a file from scriptr via http?

If you have attached files to documents persisted in your data storage, it is possible to download them from an http client.
For that, you need the following:

- Retrieve the file object from the persisted document
- Retrieve the content of the file object
- Override the standard response to send the file

In the below example, we assume that the name of the document is "mosquitto_ca",  the file name is "mosquitto.org.ct"  and that the file is attached to the "attachments" field of the document (if the document has no schema, "attachments" is a mandatory name).

```
// retrieve the file object from the persisted document
var document = require("document");
var file = document.getAttachment("mosquitto_ca", "mosquitto.org.crt", {"fieldName":"attachments"});

// Override the standard response to send the file
response.setHeader("content-disposition", "attachment;filename=" + file.fileName);
response.write(file);
response.close();
```

**Note** you can't run this example directly from the [workspace](https://www.scriptr.io/workspace) but rather from a web browser.

# More

- [How to persist files sent to my API via http?](./upload_files.md)
- [How to change the standard response structure of my API?](../api/change_response.md)
