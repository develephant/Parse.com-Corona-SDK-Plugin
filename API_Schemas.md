# Parse.com - Corona SDK Plugin

## Schemas [parse.Schema]

### .get

Get a Schema from Parse.

*Parameters:*

* __schemaName__

```lua
parse.request( parse.Schema.get, "schemaName" )
:response(cb)
```

### .getAll

Get all Schemas.

```lua
parse.request( parse.Schema.getAll )
:response(cb)
```

### .create

Create a new Schema.

*Parameters:*

* __schemaName__

```lua
parse.request( parse.Schema.create, "schemaName" )
:response(cb)
```

### .update

Update a Schema.

*Parameters:*

* __schemaName__

```lua
parse.request( parse.Schema.update, "schemaName" )
:response(cb)
```

### .delete

Deletes a Schema.

*Parameters:*

* __schemaName__

```lua
parse.request( parse.Object.delete, "schemaName" )
:response(cb)
```
