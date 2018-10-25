# How to display historical data in a dashboard?

- Open your [workspace](https://www.scriptr.io/workspace), then click on the arrow near "New Script" in the bottom left corner of the screen
- Select **Dashboard** to open the dashboard builder

![Open Dashboard Builder](./images/open_dashboard.png)

*Image 1*

The dashboard builder is a visual environment that allows your to build dashboards without coding.

## Displaying Historical values

The dashboard builder offers several widgets that are dedicated to displaying historical values, such as line charts or bar charts.
Say you need a line chart to display the historical variations of temperature and humidity measured by a sensors and persisted in documents. 
This is done in four steps:
- Add a line chart to the editing area and configure it 
- Create an API script to query the data store for historical values of temperature and humidity (we assume these documents exist)
- Connect the line chart to the script
- Save your dashboard and view it

### Add a line chart to the editing area and configure it 

- Click on the line chart icon in the toolbar. A new lien chart is automatically added to the dashboard

![New linechart](./images/add_linechart.png)

*Image 2*

- You can resize the line chart by dragging its bottom-right corner. You can also move the line chart by pressing on the widget's title bar then dragging and dropping it
- You can customize the look and feel of the line chart by clicking on the **gear icon** to open the settings

![Line chart settings](./images/linechart_settings.png)

*Image 3*

Since we need to display historical temperature and humidity values, we should configure both X (date/time) and Y (temperature, humidity) values axes,

- From the setting, click on the **X** tab
- Set the value of the X-Key field to "date-time" or any other string you'd like

![Line chart X axis](./images/linechart_x_axis.png)

*Image 4*

- From the setting, click on the **Y** tab
- Set the value of the Y-Keys field to an array containing the names of the documents fields that hold temperature and humidity values (assume these are "temperature and "humidity")
- Set the value of the Labels field to an array of label, for each of the above field name respectively

![Line chart Y axis](./images/linehcart_y_axis.png)

*Image 5*

### Create an API script to query the data store for historical values of temperature and humidity 

In the [workspace](https://www.scriptr.io/workspace), click on "New Script" to create a new script and paste the below code in it, then save it 
```
var document = require("document");
var queryParams = {
    query: "temperature<numeric> is not null and humidity<numeric> is not null",
    fields: "temperature, humidity"
};

var resp = document.query(queryParams);
if (resp.metadata.status == "success") {
    return resp.result.documents;
}

return [];
```

### Connect the line chart to the script

- From the line chart, click on the **gear icon** to open the settings
- In the Data tab:
  - Set the **Transport** field to https
  - Set the **Api** field to the absolute path of your script (**do not start with /** !)
  - Click on Save

### Save your dashboard and view it

- Give a name to your your dashboard and save it by pressing Save in the workspace toolbar
- You now have a full fledge HTML dashboard that can be opened from any web browser 
- Try it by clicking on "View" in the workspace toolbar.

**ATTENTION** If you open your dashboard directly from a browser using it's URL (not from the workspace), do not forget to pass a valid script authentication token in the query string. Otherwise, the dahsboard will not be able to invoke the API that returns the temperate

```
// Example
https://iotdemos.scriptrapps.io/tutorials/howto/ui/linechart_dashboard?auth_token=UzByDTgkRjkk2NjpmaXRiaXQ6MjlBRURDOEZCMzlDOTR1QUE5MDIxQ0LyGjc7MkJ5MDU%6X
```
