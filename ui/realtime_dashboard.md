# How to update my dashboard in real time?

You have devices pushing data to one of your API and you need to reflect the data in real time on a dasboard. 
Well, that is doable in four steps.

- Create a channel
- Update you API (or create a new API) to receive the data pushed by the devices
- Create a dashboard with the dashboard builder and add some widgets to reflect the values
- Bind your widgets to the channel

## Create a channel



## Create a dashboard with the dashboard builder and add some widgets to reflect the values

- Open your [workspace](https://www.scriptr.io/workspace), then click on the arrow near "New Script" in the bottom left corner of the screen
- Select **Dashboard** to open the dashboard builder (The dashboard builder is a visual environment that allows your to build dashboards without coding)

![Open Dashboard Builder](./images/open_dashboard.png)

*Image 1*

Let's assume you need to reflect temperature variations in real time in a gauge:

- Click on the gauge icon in the toolbar. A new Gauge is automatically added to the dashboard

![New gauge](./images/add_gauge.png)

*Image 2*

## Update a gauge in real time



# More

- [How to create a secure and scalable API?](../api/create_api.md)
- [How to retrieve the parameters sent to my API via http?](../api/read_http_request_parameters.md)
- [How to publish an mqtt message to a script (API)?](https://github.com/scriptrdotio/howto/blob/master/api/publish_mqtt_msgs_to_script.md)
- [How to read the messages sent to my API through mqtt?](https://github.com/scriptrdotio/howto/blob/master/api/read_mqtt_messages.md)
- [How to display simple values in a dashboard?](../ui/create_dashboard.md)
- [How to display historical data in a dashboard?](../ui/create_dashboard_historical.md)
