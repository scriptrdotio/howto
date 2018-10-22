# How to create groups of devices and users ?

You can create groups of devices and users in two different ways:
- From the workspace, using the visual tools
- Dynamically from the code (scripts)

## Create groups from the workspace

Sign-in to your [workspace](https://www.scriptr.io/workspace), click on your username in the top-right corner of the screen, 
then  click on **Device Directory**

![Device Directory](./images/device_directory.png)

*Image 1*

- Click on the Group tab
- Click on +Add Group
- Enter a name for the group
- Click on the check sign

![Device Directory](./images/new_group.png)

*Image 2*

Scriptr.io automatically generates and authentication token for the newly created device. 
This token can be used to authenticate http requests and web socket messages sent to your APIs.

## Create devices dynamically from the code

From within a script in the [workspace](https://www.scriptr.io/workspace), you need to require the **device** module and invoke its **create()** method passing the necessary data. If you do not specify an "id", scriptr.io will create one automatically.

```
var device = require("device");
var deviceData = {
    
    name: "Multitech Conduit 001",
    password: "some_password",
    groups: "mydevices" // optional
};

var resp = device.create(deviceData);
return resp;
```
- The object returned by create() contains a metadata section and a result section
- If successful, metadata.status will be set to "success" and result.device.id will contain the device's identifier
- If create() fails, metadata.status will be set to "failure" and no result is returned
```
// successful create (example)
{
	"result": {
		"device": {
			"id": "T7256996A7"
		}
	},
	"metadata": {
		"status": "success"
	}
}

// unsuccessful create (example)
 {
	"metadata": {
		"status": "failure",
		"statusCode": 400,
		"errorCode": "INVALID_IDENTIFIER",
		"errorDetail": "The device [T7256996A7] is invalid."
	}
}
```
