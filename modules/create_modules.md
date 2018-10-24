# How to create modules?

You can easily create reusable functions by placing them into modules. A module is simply a script that does not have a return instruction.

To create a module, login to your [workspace](https://www.scriptr.io/workspace) and click "New Script" and copy paste the below function, then save the script - assume we save it as "/lib/util".

```
function guid() {
    
    var id = "";
    for (var i = 0; i < 20; i++){
        id += String.fromCharCode(Math.round(Math.random() * 25 + 65));
    }
    
    return id;
}
```

To use the guid() function from another script, you need to **require** the "/lib/util" script:

```
var util = require("/lib/util");
var someId = util.guid();
```
