# How to Create a Secure and Scalable API
Scripts are the main components of any scriptr.io application. By default, any script you write is automatically deployed as a secure and scalable API. All scripts are written in standard JavaScript, deployed and ran on the back-end.

## Create a script
- Open your scriptr.io [workspace](https://www.scriptr.io/workspace). In the bottom left corner, click on "New Script". 
- In the editor, simply type the below:
```
return "greetings"
```
![Save your script](./images/write_script.PNG)
- Give a name to your script then click on "Save" in the toolbar. You script is automatically deployed as a secure API, with it's own endpoint.
- The endpoint of the script is by default "https://api.scriptrapps.io/path_to_script/script_name", e.g. https://api.scriptapps.io/tutorials/howto/turn_a_script_into_secure_api/greeting
- To create a path, just type it before the script name.

## Try the new API from the workspace
- You can execute a script by clicking on "Run" in the toolbar. The output of the script's execution will be displayed in the console. 
- The output is a JSON object that contains a metadata section and a result section, containing anything returned by the script (in our case "hello")
- Notice that the console displays a cURL instruction to trigger the script from a remote http client
![Run your script](./images/run_script.png)
