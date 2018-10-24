# How do I restrict access to my data?

Scriptr.io Access Control Lists (ACL) allows you to define fine grain permissions, on your APIs and on your data.

- The first filter to your data is the permissions you set on your APIs that receive client requests. You can read more about [how to restrict access on your APIs](./restrict_access_to_api.md) if needed
- The second filter is to create a [document schema](../data/create_schema.md), in which you map read/write permissions on document fields, to devices, users, groups or roles
- However, once a request triggered an API, the script executes with the **account owner credentials**, and therefore, your code can access any document. Since this might not be what you want, you can enforce accessing documents using the credentials of the device/user that triggered the request
- 
