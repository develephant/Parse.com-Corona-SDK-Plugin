# Parse.com - Corona SDK Plugin

## Roles [parse.Role]

### .get

Get a Role.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Role.get, "1234abcd" )
:response(cb)
```

### .create

Create a new Role.

```lua
parse.request( parse.Role.create )
:data( { color = "Red", name = "Jingles" } )
:response(cb)
```

### .update

Update a Role.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Role.update, "Ex4UOSca" )
:response(cb)
```

### .delete

Deletes an Object.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Role.delete, "Ex4UOSca" )
:response(cb)
```
