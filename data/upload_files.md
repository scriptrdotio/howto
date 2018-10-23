# How to persist files sent to my API via http?

- Any script can retrieve the parameters it receives using the native **request** object that allows you to retrieve information about the request, including the conveyed parameters
- Upload files can be retrieved using the **files** property of the **request** object
- To persist data into document from within a script, you need to require the native "document" module

## Getting the uploaded files

**request.files** is an map of key/values where each key is the name of the parameter used to upload files and the value is an array of File objects
