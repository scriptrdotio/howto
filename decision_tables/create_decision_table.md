# How to use decision tables?

Scriptr allows you to create advanced condition/action evaluation logic without coding, through [decision tables](https://en.wikipedia.org/wiki/Decision_table).

## Create a decision table

To create a decision table, click on the arrow near +New Script on the bottom left corner of the script, then select **Decision Tables**.

![New Decision Table](./images/create_decision_table.png)

*Image 1*

- The upper-left part of the decision table is where you set the criteria that you need to evaluate, and the columns specify the conditions you want to associate to these criteria. A rule is a combination of multiple conditions within a same conlumn
- The lower-left part of the decision table is where you specify the actions to execute whenever a rule is verified
- Each column of the decision table can hold a pair of rules/corresponding actions.

For example, assume you need to control the ambiant climate based on temperature and humidity values. You could define the following rules:

- If temperature < 18 turn and humidity < 60%  turn heater on
- If temperature < 18 turn and humidity >= 60% turn heater and dehumidifier on 
- If temperature > 25 turn and humidity < 60%  turn cooler on
- If temperature > 25 18 turn and humidity >= 60% turn heater and dehumidifier on 

![Ambiant climate control](./images/decision_table.png)

*Image 2*

## Where do criteria come from?

Criteria you use in defining conditions are fields of the payload that is sent to the decision table. This payload is a JSON object that has contains the mandatory "payload" field, which is a map of key/values.

Example of the payload to send for the ambiant climate control example:
```
{
  "payload": {
    "temperature":26,
    "humidity": 40
  }
}
```





