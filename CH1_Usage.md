# Corona SDK Parse Plugin

## Usage - Chapter 1

The Parse plugin follows a simple pattern for making requests to the Parse REST API. The plugin facilitates the entire REST API. By reading through the [__Parse REST API Guide__](https://www.parse.com/docs/rest/guide) you will have a much easier time working with this plugin.

## Request

It all starts with a __request__ *to* Parse, and completes with a __response__ *from* Parse. What happens in-between that depends on the API call being used.  __All responses are returned in a Lua table.__

For exact details about each response, please see the Parse REST Guide mentioned earlier, or follow the direct Parse links off the [API pages](Home).

### parse.request

A `parse.request` requires one of the Parse REST API [endpoint objects](Endpoints) as the first parameter.

Example:

```lua
local req = parse.request( parse.User.me )
```

This will make a request to the Parse.com User endpoint, asking for the `me` resource.

> A `parse.User.me` request returns meta for the currently logged in user.

__Additional parameters may be required depending on the endpoint.__

Example:

```lua
local req = parse.request( parse.Object.update, "Pets", "1234abcd" )
```

> A `parse.Object.update` request requires a __class__ and __objectId__ parameter.

### Response

Every `parse.request` must have a `response` *listener* attached to it before it will fire. For example, in the previous example, the `request` is set up, but won't do anything until it has a `response` listener.

What follows is the bare minimum needed for a working `request`:

```lua
local req = parse.request( parse.User.me )
req:response()
```

To capture any incoming data, we need to provide a callback function to the `response` listener. The callback function receives three parameters; the success state (`ok`), the data, if any, as a table (`res`), and an (`info`) table that contains various information about the request and response that took place.

Example:

```lua
local req = parse.request( parse.User.me )
req:response(function( ok, res, info )
  if not ok then
    print( 'err', res )
  else
    print( res.username )
    print( info.status )
  end
end)
```

## Request Methods

The request methods are used in-between the request and response -- similar to middleware -- to perform certain functions depending upon the endpoint being used. The request methods are as follows, some are mutually exclusive for the request.

---

__:data( tbl_or_json )__

The __data object__ to send to Parse. Can be a Lua table or raw JSON string. See [Using Raw JSON](UsingJson). When viewing the Parse.com docs, the curl __-d__ flag shown in the examples indicates the usage of `:data()` or `:set()` in the Corona plugin request.

___Setting :data() at anytime will clear any previous data for the request, including data added with the :set() method.___ There can on be only one __data object__ per request.

---

__:set( name, value )__

Helper. Sets a value on the __data object__. If the __data object__ is a JSON string, no action is performed. `name` must be a string key.

---

__:where( query_tbl_or_json )__

When using `query` endpoints, you provide your query parameters using the `:where()` method.

Anytime you see the usage of `{where=...}` in the Parse.com docs, it's an indicator that the method will probably use `:where()` in the Corona plugin request.

---

__:options( { name1 = value1, name2 = value2 } )__

The `:options()` method is used to add values to the request query string. This can be used to add special Parse keys like `count`, `order`, `limit`, etc. The `:options()` method can be added to most requests that return bulk data sets.

When you see the usage of the __--data-urlencode__ curl flag in the Parse.com docs, then this indicates something that should be put in the `:options()` method. The method can accept a Lua table or a raw JSON string.

---

__:header( name, value )__

Helper. Adds a custom header to the request to be sent to Parse. Can be used multiple times.

In most cases you won't need to use this method, as the standard headers are already sent in the background. There are a few use cases for additional headers in the Parse.com docs. Use this method to add any.

---

__:progress( ok, bytesTrans, bytesEst )__

Used as a progress status *listener* for __upload__ and __download__ file events. See [Using Files](UsingFiles). The listener receives a status (`ok`), the bytes transferred (`bytesTrans`), and the estimated bytes to go (`bytesEst`). Use to follow file transfer progress.

### Coding Styles

You can use a variable, chain, or stack the various request methods, whatever fits your coding style best:

*Variable*

```lua
local req = parse.request( parse.Config.get )
req:response(function( ok, res )
  if not ok then
    print('err', res)
  else
    print(res.color, res.age)
  end
end)
```

*Chaining*

```lua
--Setup callback
local function cb( ok, res, info )
  print( ok, res, info )
end

parse.request( parse.User.me ):response(cb)

--OR

parse.request( parse.User.get, "1234abcd" ):options({keys='username'}):response(cb)
```

*Stacking*

```lua
parse.request( parse.Objects.query, "Pets" )
:where( { color = "Green", age = { ["$gt"] = 20 } )
:options( { limit = 20, order = "age" } )
:header("X-Secret-Msg", "some-value")
:response(function( ok, res, info )
  if not ok then
    print('err', res)
  else
    if info.status == 200 then
      print( res.color, res.age )
    end
  end
end)
```
