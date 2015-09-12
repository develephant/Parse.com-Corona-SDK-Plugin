# Parse.com - Corona SDK Plugin

## Cloud [parse.Cloud]

### .call

Call a Cloud function.

*parameters:*

* functionName

```lua
parse.request( parse.Cloud.call, "functionName" )
:response(cb)
```

### .job

Start up a Cloud Job.

*parameters:*

* jobName

```lua
parse.request( parse.Cloud.job, "jobName" )
:response(cb)
```
