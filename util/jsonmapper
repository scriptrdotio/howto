# How to map an incoming JSON payload to another JSON structure (JSON mapper)?

In many cases your IoT application will be receiving JSON data in different structures because they are stemming from different data sources. 
You will therefore need to normalize these data into a unique target data structure that your business logic will use.

One option to transform an incoming JSON structure into another one is to code the transformation yourself in one of your scriptrs. 
Another interesting option is to do this visually, using the JSON mapper tool.

# The JSON mapper

Click +New Script in the bottom left corner of the [workspace](https://www.scriptr.io/workspace) and select Json Mapper.

![Open the Json Mapper](./open_mapper.PNG])
*Figure 1 - Open the Json Mapper*

In the editor area, under the JSON tab, enter a sample of the expected incoming payload structure in the Input JSON area. 
In our example, we will use the below:
```
{
  "data": {
    "temp":22,
    "hum":56
  },
  "rssi": 324
}
```
Assume we need to normalize this struture into the following target structure:
```
{
  "temperature":33,
  "humidity":56,
  "rssi": 324
}
```
Just type the target data structure into the Output JSON area.
[Specifiy Input and Output payloads](./input_output_payloads.png)
