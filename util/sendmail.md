# How to send an email from a script?

Easy. Just use the native **sendMail()** function, specifying the recipient email address, the sender, the subject and the email body.

**Example**

Open your [workspace](https://www.scriptr.io/workspace) and create a new script, then paste the below code in it 

```
var htmlContent = "<h1>Climate monitor</h1>Temperature: <strong>" + request.parameters.temperature + "</strong>";
var resp = sendMail("karim@scriptr.io", "iot demos", "Monitoring", htmlContent);
```
