# Parse.com - Corona SDK Plugin

## Apps [parse.App]

### .get

Get a App from Parse.

*Parameters:*

* __applicationId__

```lua
parse.request( parse.App.get, "applicationId" )
:response(cb)
```

### .getAll

Get all Apps.

```lua
parse.request( parse.App.getAll )
:response(cb)
```

### .create

Create a new App.

```lua
parse.request( parse.App.create )
:response(cb)
```

### .update

Update a App.

*Parameters:*

* __applicationId__

```lua
parse.request( parse.App.update, "applicationId" )
:response(cb)
```

### .delete

Deletes a App.

*Parameters:*

* __applicationId__

```lua
parse.request( parse.App.delete, "applicationId" )
:response(cb)
```
