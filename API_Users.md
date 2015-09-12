# Parse.com - Corona SDK Plugin

## Users [parse.User]

### .login

Log in a User.

```lua
parse.request( parse.User.login )
:set("username", "Chris")
:set("password", "1234abcd")
:response(cb)
```

### .logout

Log out a User.

> If the User is not logged in, this action does nothing.

```lua
parse.request( parse.User.logout )
:response(cb)
```

### .me

Get the logged in User.

> The user must be logged in.

```lua
parse.request( parse.User.me )
:response(cb)
```

### .get

Get an User by `objectId`.

*Parameters:*

* __objectId__

```lua
parse.request( parse.User.get, "1234abcd" )
:response(cb)
```

### .query

Get User(s) by Query. To fetch all, pass empty table to the `:where` method.

```lua
parse.request( parse.User.query )
:where( { color = "Red" } )
:options( { limit = 1, order = "color" } )
:response(cb)
```

### .create

Create a new User.

```lua
parse.request( parse.User.create )
:data( { username = "Spock", password = "1234", email = "spock@enterprise.net" } )
:response(cb)
```

### .update

Update a User by `objectId`.

```lua
parse.request( parse.User.update, "1234abcd" )
:data( { phone = "233-230-2333", address = "Space" } )
:response(cb)
```

### .delete

Delete a User by `objectId`.

```lua
parse.request( parse.User.delete, "1234abcd" )
:response(cb)
```

### .requestPasswordReset

Queues up a password reset request based on `email`.

```lua
parse.request( parse.User.requestPasswordReset )
:options( { email = "spock@enterprise.net" } )
:response(cb)
```

### .link

Link a User by `objectId`.

```lua
parse.request( parse.User.link, "1234abcd" )
:response(cb)
```

### .unlink

Unlink a User by `objectId`.

```lua
parse.request( parse.User.unlink, "1234abcd" )
:response(cb)
```
