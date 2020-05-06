# How to dynamically generate a file from within a script

**This is an advanced feature**

Sometimes you will find it convenient to dynamically generate files or even scripts (application logic) in your account.
This is very simple to do with scriptr, as illustrated in the below example where we generate a script. Same logic applies for any type of file to generate.

- The content variable will contain the logic we need to save into a script (if you wish to generate another type of file, add any content)
- The **fileContent** variable is the file content envelop. It must specify:
  - the execute, read and write authorizations (ACL). In our example, only the owner ("nobody") of the account has privileges on the script.
As a good practice, you should always keep read/write to "nobody" and possibly set the "execute" privilege to a user or a group.
  - the content-type: in the case of a script, it must be "application/vnd.scriptr-javascript
  - the content of the script
- Next step is to invoke the setContent() function of the file module, passing the file envelop and specifying if you are updating an existing file or creating a new one (update set to true or false).

'''
var content = "const MAX = 25;\nfunction isTemperatureTooHigh(temperature){return temperature > MAX;}";
var fileContent = {
    "ACL":
        {
            "execute":"nobody",
            "read":"nobody",
            "write":"nobody"
        },
    "contentType":"application/vnd.scriptr-javascript",
    "content": content
};
var file = require("file");
var update = false;

return file.setContent("tests/dynamicscript",JSON.stringify(fileContent), update) ;
'''
