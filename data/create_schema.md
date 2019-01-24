# How to create validation rules (schemas) on my data?

- Scriptr provides you with a NoSQL database that allows you to save data into key/value structures called "documents"
- You can create (XML) schemas to define **document types**, i.e. constraints on the data (mandatory fields, multiplicity, data types, etc.)
- Scriptr **automatically** validates any schema-related document upon creation or update

## Create a schema using the visual environment

From the scriptr [workspace](https://www.scriptr.io/workspace) click on **Tools** in the toolbar then select **Data Explorer**

![Open Data Explorer](./images/open_data_explorer.png)

*Image 1*

Click on Schema then New to open the schema editor.

![Open Schema Editor](./images/new_schema.png)

*Image 2*

A schema has two main sections: **aclGroups** and **fields**

### aclGroups 

ACL groups allow you to define read/write permissions on the fields of your document. You should define at least one ACL group but you can have more than one ACL group. 

Scriptr creates three ACL groups by defaults: 
- &lt;aclGroup name='aclgroupName'&gt; (the name is just a dummy value, you should replace it with somethings meaningful), 
- &lt;defaultAcl&gt; is the default ACL. You can remove this element if you wish
- &lt;schemaAcl&gt; defines permissions on the schema itself. **You usually won't modify it**

An ACL group specifies read/write permissions on the document fields it contains (&lt;fields&gt;)
Permissions are specified via the **&lt;read&gt;** and **&lt;write&gt;** elements, which respectively define who has read and/or write permissions on the fields.

In the below example we created an ACL group called "smart_building_can_write" within which we specified that members of the "smart_building" **group** and the "building_admin" **user** have write privilege on the "temperature" and "humidity" fields of documents to which this schema is applied. Read permissions are granted to the "authenticated" **predefined role**, which includes any authenticated entity in the current scriptr account. Owners of the write privilege also have the permission to read.
([learn how to create users, devices and groups](../acl/create_devices_groups.md))

```
<schema>
	<aclGroups>
		<aclGroup name='smart_building_can_write'>
			<read>authenticated</read>
			<write>group:smart_building;building_admin</write>
			<fields>
				<field>temperature</field>
				<field>humidity</field>
			</fields>
		</aclGroup>
		<schemaAcl>
			<read>nobody</read>
			<write>nobody</write>
			<delete>nobody</delete>
		</schemaAcl>
	</aclGroups>
	<fields>
		<field name='temperature' type='numeric'/>
		<field name='humidity' type='numeric'/>
	</fields>
</schema>
```

### Fields

The **&lt;fields&gt;** element allows you to define (1) the type of the fields of your documents (2) validation constraints, (3) if a field is unique, (4) if a field is searchable.

- Available types are: numeric, string, text, data, File and geospatial
- Validation constraints are: 
  - cardinality: min, max values allowed for this field. If min = 1 and max = 1, the filed is mandatory. If min = 0 and max = 1, the field is optional (default case), if min = 1 and max = 10, you can store up to 10 values in this field (array - limited to a max of 50)
  - range: specifies the min and max value of a numeric field
  - length: specifies the min nand max length of a string field
  - regex: specifies a regular expression that must be matched by the value of a string field
- Unicity: when the "unique" attribute is set to true, it indicates that the value of the corresponding field is unique across documents sharing the same schema
- Searchable: when the "searchable"field is set to true, it forces the indexing of this field (only possible if the store is created as searchable)

**Example**
```
<schema>
	<aclGroups>
		<aclGroup name='smart_building_can_write'>
			<read>authenticated</read>
			<write>group:smart_building;admin</write>
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
		        <cardinality min='1' max='1'></cardinality>
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

# More

- Read our [documentation](https://www.scriptr.io/documentation#documentation-schemamoduleschemaModule) to Learn how to manipulate schemas from the code in your scripts
- [How to apply automatic validation (schemas) on my data](./create_schemabased_docs.md)
