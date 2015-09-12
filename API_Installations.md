# Parse.com - Corona SDK Plugin

## Installations [parse.Installation]

### .get

Get an Installation from Parse.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Installation.get, "1234abcd" )
:response(cb)
```

### .query

Perform an Installation Query.

```lua
parse.request( parse.Installation.query )
:where( { color = "Brown" } )
:response(cb)
```

### .create

Create a new Installation.

```lua
parse.request( parse.Installation.create )
:data( { color = "Red", name = "Jingles" } )
:response(cb)
```

### .update

Update an Installation by `objectId`.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Installation.update, "Ex4UOSca" )
:set("color", "Blue")
:response(cb)
```

### .delete

Deletes an Installation by `objectId`.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Installation.delete, "Ex4UOSca" )
:response(cb)
```
