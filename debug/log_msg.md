# How to log messages to check the execution of my scripts?

There are actually two ways to do this:

## Write to the logs

- Open your [workspace]("https://www.scriptr.io/workspace") and click on "New Script".
- In the script, require the **log** module, then specify the **log level** you desire using **log.setLevel()**. There are four log levels: 
info, error, warn and debug (or "INFO", "ERROR", "WARN", "DEBUG")
- To write to the logs, use on of the available methods: **log.debug()**, **log.info()**, **log.warn()**, **log.error()**

```
var log = require("log");
log.setLevel("info");

log.debug("some debug data");
log.info("some info");
log.warn("some warning");
log.error("some error");
```
### Log levels

As in any othr log system, the log level defines the verbosity, i.e. what appears in the log and what doesn't. Hence:
- If the level is set to "debug", any call to log.debug(), log.info(), log.warn(), log.error() results in a log entry
- If the level is set to "info", any call to log.info(), log.warn(), log.error() results in a log entry, log.debug() is ignored
- If the level is set to "warn", any call to log.warn(), log.error() results in a log entry, log.debug(), log.info() are ignored
- If the level is set to "error", only calls to log.error() result in a log entry, log.debug(), log.info() and log.warn() are ignored

### How to see the logs

From the [workspace]("https://www.scriptr.io/workspace"), click on "Logs". This opens the logs file in a new tab. 


Logs are listed by script execution and sorted by date in descending order. Click on a row to see the log messages for the corresponding script execution.
