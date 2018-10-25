# How do I restrict access to my data?

Scriptr.io Access Control Lists (ACL) allows you to define fine grain permissions, on your APIs and on your data.

- The first filter to your data is the permissions you set on your APIs that receive client requests. You can read more about [how to restrict access on your APIs](./restrict_access_to_api.md) if needed
- The second filter is to create a [document schema](../data/create_schema.md), in which you map read/write permissions on document fields, to devices, users, groups or roles
- However, once a request has passed the first filter and successfully triggered an API, **the script executes by default with the account owner credentials** therefore, your code can access any document, despite the schema 
- If this is not what you want, **you can enforce accessing documents using the credentials of the device/user that triggered the request**

## How do I access data using the request initiator credentials?

Simple,

In your code, just insert invocation to the document module's operation into a function passed to the native **runAs()** function.
- Example 1 below shows code that runs using the default privileges (account owner)
- Example 2 shows how to use **runAs()** to use the caller's (request initiator) privileges to run the same code

**Example 1: using default privileges** 
```
// we query all documents that are bound to the "smart_building" schema
var document = require("document");
var queryExpression = {

    query: 'schema="smart_building"',
    fields: '*'
};

// default privileges (account owner)
return document.query(queryExpression);
```

**Example 2: using caller's privileges**
```
var document = require("document");
var queryExpression = {

    query: 'schema="smart_building"',
    fields: '*'
};

// Retrive user (caller) id from the request
var userId = request.user.id;

// use caller's privileges
return runAs(
    function(){
        return document.query(queryExpression);
    }, "fitbit");
```

## The schema used in the above examples

- Open the [Data Explorer](https://www.scriptr.io/dataexplorer), click on "Schemas" in the left-side menu, then click on "New" to create a new schema
- In the editing area, paste the below schema definition and save it as "smart_building".
```
<schema>
	<aclGroups>
		<aclGroup name='smart_building_policy'>
			<read>group:smart_building</read>
			<write>group:smart_building/write>
			<fields>
				<field>temperature</field>
				<field>humidity</field>
				<field>timestamp</field>
				<field>deviceid</field>
			</fields>
		</aclGroup>
		<schemaAcl>
			<read>nobody</read>
			<write>nobody</write>
			<delete>nobody</delete>
		</schemaAcl>
	</aclGroups>
	<fields>
		<field name='temperature' type='numeric'>
		    <validation>
		        <cardinality min='1'></cardinality>
		    </validation>
		</field>
		<field name='humidity' type='numeric'>
		    <validation>
		        <range min='0' max='100'></range>
		    </validation>
		</field>
		<field name='timestamp' unique='true' type="numeric"></field>
		<field name='deviceid' type='string'>
		    <validation>
		        <regex>dev[0-9]{9}</regex>
		    </validation>
		</field>
	</fields>
</schema>
```
Looking closer at &lt;aclGroup&gt; element, you can observe that **the schema grants read and write permissions on all the document fields to the devices and users that are members of the "smart_building" group** (read more on [how to create groups](./create_devices_groups.md))

Assume you already have created two documents bound to the above schema:

- The execution of Example 1 would return something similar to the following
- You can observe that the temperature, umidity and timestamp field are returned

```
{
	"result": {
		"documents": [
			{
				"key": "6D73404F88A6A12363CB1FC404A76C85",
				"versionNumber": "1.0",
				"deviceid": "dev012345678",
				"temperature": "22.5",
				"humidity": "52.0",
				"timestamp": "1.53996309E12",
				"creator": "scriptr",
				"lastModifiedDate": "2018-10-19T15:40:35+0000",
				"lastModifiedBy": "scriptr",
				"creationDate": "2018-10-19T15:37:14+0000",
				"schema": "smart_building",
				"latest": "1.0"
			},
			{
				"key": "D92B256B64773A86AB89C2253735725E",
				"versionNumber": "1.0",
				"deviceid": "dev012345678",
				"temperature": "55.0",
				"humidity": "22.0",
				"timestamp": "1.23456794E9",
				"creator": "S22A80F766",
				"lastModifiedDate": "2018-10-19T14:58:55+0000",
				"lastModifiedBy": "S22A80F766",
				"creationDate": "2018-10-19T14:57:48+0000",
				"schema": "smart_building",
				"latest": "1.0"
			}
		]
	},
	"metadata": {
		"status": "success"
	}
}
```
- On the opposite, running the code in Example 2 returns what follows
- You can see the effect or using runAs(): we only obtained document metadata, but not the temperature, humidity and timestamp fields

```
 {
	"result": {
		"documents": [
			{
				"key": "6D73404F88A6A12363CB1FC404A76C85",
				"versionNumber": "1.0",
				"creator": "scriptr",
				"lastModifiedDate": "2018-10-19T15:40:35+0000",
				"lastModifiedBy": "scriptr",
				"creationDate": "2018-10-19T15:37:14+0000",
				"schema": "smart_building",
				"latest": "1.0"
			},
			{
				"key": "D92B256B64773A86AB89C2253735725E",
				"versionNumber": "1.0",
				"creator": "S22A80F766",
				"lastModifiedDate": "2018-10-19T14:58:55+0000",
				"lastModifiedBy": "S22A80F766",
				"creationDate": "2018-10-19T14:57:48+0000",
				"schema": "smart_building",
				"latest": "1.0"
			}
		]
	},
	"metadata": {
		"status": "success"
	}
```
