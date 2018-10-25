# How to display simple values in a dashbord?

- Open your [workspace](https://www.scriptr.io/workspace), then click on the arrow near "New Script" in the bottom left corner of the screen
- Select **Dashboard** to open the dashboard builder

![Open Dashboard Builder](./images/open_dashboard.png)

The dashboard builder is a visual environment that allows your to build dashboards without coding.

## Displaying single values

The dashboard builder offers several widgets that are dedicated to displaying single values, such as gauges, speedometer or odometer.

Let's say you need a gauge to display the current temperature measured by a sensor and persisted in a document. This is done in three steps:
- Add a gauge to the editing area and configure it 
- Create an API script to read the temperature from the document (we assume you already created the script to persist the temperature in a document)
- Connect the gauge to the script

### Add a gauge to the editing area and configure it 

- Click on the gauge icon in the toolbar. A new Gauge is automatically added to the dashboard

![New gauge](./images/add_gauge.png)

*Image 1*

- You can resize the gauge by dragging its bottom-right corner. You can also move the gauge by pressing on the gauge title bar then dragging and dropping it
- You can customize the look and feel of the gauge by clicking on the **gear icon** to open the settings

![Gauge settings](./images/gauge_settings.png)

Since we need to display temperature, we will configure the min and max values (in Celsius) and the corresponding colors: green from 0 to 22, orange from 22 to 28 and red from 28 to 40:

- From the setting, click on the Min/Max tab
- Set the min value to 0 and the max value to 40

![Gauge Min/Max](./images/gauge_minmax.png)

- From the setting, click on the Format tab
- Set the Symbol field to "Celsius"

![Gauge Min/Max](./images/gauge_unit.png)

