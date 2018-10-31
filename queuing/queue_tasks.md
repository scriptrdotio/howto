# How to create queued jobs?

Some lengthy operations cannot be completed in a time that is acceptable for a remote client. 
In that case, it makes no sense to keep the client waiting for the answer and resorting to an asychronous communication is a better alternative.
In addition, the execution time of a script is throttled, meaning that scriptr will automatically stops any script that requires an execution time that is greater that the maximum.
