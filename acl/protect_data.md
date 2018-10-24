# How do I restrict access to my data?

Scriptr.io Access Control Lists (ACL) allows you to define fine grain permissions, on your APIs and on your data.

- The first filter to your data is the permissions you set on your APIs that receive client requests. You can read more about [how to restrict access on your APIs](./restrict_access_to_api.md) if needed
- The second filter is to create a [document schema](../data/create_schema.md), in which you map read/write permissions on document fields, to devices, users, groups or roles
- However, once a request has passed the first filter and successfully triggered an API, **the script executes by default with the account owner credentials** therefore, your code can access any document 
- Since this might not be what you want, **you can enforce accessing documents using the credentials of the device/user that triggered the request**

## How do I access data using the request initiator credentials?

Simple,

In your code, just insert invocation to the document module's operation into a function passed to the native **runAs()** function.
- Example 1 below shows code that runs using the default privileges (account owner)
- Example 2 shows how to use **runAs()** to use the caller's (request initiator) credentials to run the same code

**Example 1** 
```
// we quert 
var document = require("document");
var queryExpression = {

    query: 'schema="smart_building"',
    fields: '*'
};

// default privileges (account owner)
return document.query(queryExpression);
