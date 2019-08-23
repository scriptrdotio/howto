# About this tutorial

This is a short tutorial on how to implement a very simple end-to-end IoT application with scriptr.io, as means to start familiarizing yourself with scriptr.io.

We will consider the following use case: we need to display in a very simple dashboard, the current and historical values of measurments (speed, temperature and number of passengers) made by a device that sends these data to our scriptr.io account through http POST requests. Value changes will be reflected in real-time in the dashboard.

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
3. Query the data store for the last 20 historical values of each measument
4. Publish the latest and the historical values to the dashboard
5. Display the values in the dashboard

# Implementation




