# How to invoke a decision table from a script?

A decison table is automatically turned into an API, which is meant to be invoke by remote client through one of the supported communication protocols (http, mqtt, websockets, amqp). Nevertheless, it is possible for a script to invoke a decision table as if it was a module, using the native **scriptUtil** module.

```
// Require the scriptUtil module, notice the "/m"
var stdLibScript = require("m/scriptUtil");

// Specify the absolute path of the decision table script (do not start with "/")
var decisionTablePath = "tutorials/howto/decision_tables/simple_table"; // this is an example

// prepare the payload to send to the decision table
var data = {
  "payload": { // "payload" is a mandatory field
      "temperature": 26,
      "humidity": 61,
      "unit": "C"
   }
};

// invoke the decision table using the execute() function, passing the path and the stringified payload, then get the returned decision
var decision = stdLibScript.execute(decisionTablePath, {"payload": JSON.stringify(payload)});
```
