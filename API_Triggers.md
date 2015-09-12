# Parse.com - Corona SDK Plugin

## Triggers [parse.Trigger]

### .get

Get a Trigger from Parse.

*Parameters:*

* __triggerName__

```lua
parse.request( parse.Trigger.get, "triggerName" )
:response(cb)
```

### .getAll

Get all Triggers.

```lua
parse.request( parse.Trigger.getAll )
:response(cb)
```

### .create

Create a new Trigger.

```lua
parse.request( parse.Trigger.create )
:response(cb)
```

### .update

Update a Trigger.

*Parameters:*

* __triggerName__

```lua
parse.request( parse.Trigger.update, "triggerName" )
:response(cb)
```

### .delete

Deletes a Trigger.

*Parameters:*

* __triggerName__

```lua
parse.request( parse.Trigger.delete, "triggerName" )
:response(cb)
```
