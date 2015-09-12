# Parse.com - Corona SDK Plugin

## Analytics [parse.Analytics]

### .AppOpened

Send an "Application Opened" event to Parse.

```lua
parse.request( parse.Analytics.AppOpened )
:data({})
:response(cb)
```

### .event

Send a custom event to Parse.

```lua
parse.request( parse.Analytics.event )
:response(cb)
```
