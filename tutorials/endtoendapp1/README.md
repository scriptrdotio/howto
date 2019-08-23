# About this tutorial

This is a short tutorial on how to implement a very simple end-to-end IoT application with scriptr.io, as means to start familiarizing yourself with scriptr.io.

We will consider the following use case: we need to display in a very simple dashboard, the current and historical values of measurements (speed, temperature and number of passengers) made by a device that sends these data to our scriptr.io account through http POST requests. Value changes will be reflected in real-time in the dashboard.

# The IoT application

## Application parts

Our application will be composed of two parts:
- A data ingestion script used by the device to send measurments. The script saves the data in our scriptr.io's NoSQL data store and publishes updates to the dahsboard
- A dahsboard script that receives published data and displays it.

To keep it simple, we will simulate the device by resorting to [Postman](https://www.getpostman.com/products), a well known http client. We will manually send data from Postman to our data ingestion script. 

## Required functionality

Our application requires the following to be implemented:

1. Extract payload sent by the device 
2. Store the extracted payload (measurments) into the NoSQL data store
3. Query the data store for the last 20 historical values of each measurement
4. Publish the latest and the historical values to the dashboard
5. Display the values in the dashboard

# Implementation

In the following, we will assume that the device sends us the following JSON payload via an HTTP POST request:
```
{
  "speed": <some_value>, // e.g. 45
  "temperature": <some_value_in_celsius>, // e.g. 25
  "num_passengers": <some_value> // e.g. 12
}
```

## Extract payload sent by the device

In scriptr.io, any script you implement is automatically turned into a web service, remotely accessible via different protocols and notably http. So let's go ahead and create our ingestion script:
- From the [workspace](https://www.scrptr.io/workspace), click on the +New Script option in the bottom-left corner of the screen
- Enter a name (ingestion)
- In the editor area, type "return" and save the script by clicking "Save" in the menu bar.

![create_script](./ingestion_script_1.png)

You now have a remotely accessible API available at the following endpoint: https://api.scriptrapps.io/ingest.

You might be wondering what will happen if all readers of this tutorial name their script "ingestion", wouldn't there be collisions? Actually, scriptr.io turned your script into a **secure** web service (you might have noticed the small red lock on the right), which means that devices can only invoke the script by providing credentials that are generated from your own scriptr.io account. Since credentials are account specific, there is no risk of collision! We'll get back to credentials later on.









