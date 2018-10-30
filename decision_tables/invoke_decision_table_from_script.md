# How to invoke a decision table from a script?

A decison table is automatically turned into an API, which is meant to be invoked by remote clients through one of the supported communication protocols (http, mqtt, websockets, amqp). Nevertheless, it is possible for a script to invoke a decision table as if it was a module, using the native **scriptUtil** module and it **execute(path_to_table, payload)** function, as described in the below example.

```
// Require the scriptUtil module, notice the "/m"
var stdLibScript = require("m/scriptUtil");

// Specify the absolute path of the decision table script (do not start with "/")
var decisionTablePath = "tutorials/howto/decision_tables/simple_table"; // this is an example

// prepare the payload to send to the decision table
var data = {
    // "payload" is a mandatory field
    "payload": JSON.stringify({  // notice that the payload content has to be stringified
        "temperature": 26,
        "humidity": 61,
        "unit": "C"
    })
};

// invoke the decision table using the execute() function, passing the path and the stringified payload, 
// then get the returned decision
var decision = stdLibScript.execute(decisionTablePath, data);
```
Try it,

Open your [workspace](https://www.scriptr.io/workspace) and create a new script using the below (first, create a decision table using the example given in [How to use decision tables?](./create_decision_table.md)
