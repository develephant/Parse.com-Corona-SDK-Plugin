# Parse.com - Corona SDK Plugin

## Sessions [parse.Session]

### .me

Get the logged in Session.

> The User must be logged in.

```lua
parse.request( parse.Session.me )
:response(cb)
```

### .get

Get an Session by `objectId`.

*Parameters:*

* __objectId__

```lua
parse.request( parse.Session.get, "1234abcd" )
:response(cb)
```

### .query

Get Session(s) by Query. To fetch all, pass empty table to the `:where` method.

```lua
parse.request( parse.Session.query )
:where( { color = "Red" } )
:response(cb)
```

### .update

Update a Session by `objectId`.

```lua
parse.request( parse.Session.update, "1234abcd" )
:data( { color = "Yellow" } )
:response(cb)
```

### .delete

Delete a Session by `objectId`.

```lua
parse.request( parse.Session.delete, "1234abcd" )
:response(cb)
```

### .logout

Alias to `User` logout.

```lua
parse.request( parse.Session.logout )
:response(cb)
```
