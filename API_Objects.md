# Parse.com - Corona SDK Plugin

## Objects [parse.Object]

### .get

Get an Object from Parse.

*Parameters:*

* __class__
* __objectId__

```lua
parse.request( parse.Object.get, "Pets", "1234abcd" )
:response(cb)
```

### .query

Perform an Object Query.

*Parameters:*

* __class__

```lua
parse.request( parse.Object.query, "Pets" )
:where( { color = "Brown" } )
:response(cb)
```

### .create

Create a new Object.

*Parameters:*

* __class__

```lua
--== Creating an Object
--== Using `:set`
parse.request( parse.Object.create, "Pets" )
:set("color", "Red")
:set("name", "Jingles")
:response(cb)

--== OR
--== Using `:data`
parse.request( parse.Object.create, "Pets" )
:data( { color = "Red", name = "Jingles" } )
:response(cb)

--== OR
--== Using `:data` with JSON string
parse.request( parse.Object.create, "Pets" )
:data( [[{"color":"Red","name":"Jingles"}]] )
:response(cb)
```

### .update

Update an Object.

*Parameters:*

* __class__
* __objectId__

```lua
parse.request( parse.Object.update, "Pets", "Ex4UOSca" )
:set("color", "Blue")
:response(cb)
```
See `.create` above for other usages with Lua tables, and JSON strings.

### .delete

Deletes an Object.

*Parameters:*

* __class__
* __objectId__

```lua
parse.request( parse.Object.delete, "Pets", "Ex4UOSca" )
:response(cb)
```
