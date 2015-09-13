# Corona SDK Parse Plugin

## JSON to Lua Rules

JSON "objects" and Lua tables have a similar looking structure, but differ in the following ways:

#### General

Lua uses an equal sign `=` as its setter. JSON uses a colon `:` as its setter. Both use curly braces as "objects":

```lua
--Lua
local tbl_obj = { username = "Jim", age = 23 }
```

```javascript
//JSON (javascript)
var json_obj = { "username": "Jim", "age": 23 }
```

JSON uses quoted strings as key names. This is optional for Lua in most cases (see Unique Keys).

#### Arrays

Arrays in JSON are enclosed in brackets:

```javascript
//JSON (javascript)
var json_arr = [ 'green', 'blue', 'red' ]
```
In __Lua__, use a table array instead:

```lua
--Lua
local tbl_arr = { 'green', 'blue', 'red' }
```

#### Unique Keys

If you have a key with uncommon chars, spaces, etc., you must wrap it with brackets and quotes so that it will be converted to JSON properly from Lua.

```lua
--== Nope, even though $gt is a valid Parse key.
local data_tbl = { $gt = 200 }

--== Yes! Wrap the value in brackets and quotes.
local data_tbl = { ["$gt"] = 200 }
```

```lua
--== Nope.
local data_tbl = { my awesome color = "Green" }

--== Yes!
local data_tbl = { ["my awesome color"] = "Green" }
```

__This is not needed for common keys:__

```lua
--== Using common keys
local data_tbl = { color = "Green", dogs = 3 }

--== Mixing common and unique
local data_tbl = { score = { ["$gt"] = 200 } }
```

## Conversions

In the [__Parse REST API guide__](https://www.parse.com/docs/rest/guide) you will see lots of usage examples. You need to do table conversions on the `data` you will send from Lua. In the examples, the `data` property is the __-d__ flag, followed by some JSON data.

```bash
# Parse.com example code
 curl -X POST \
  ...
  -d '{"score":1337,"playerName":"Sean Plott","cheatMode":false}' \
  https://api.parse.com/1/classes/GameScore
```
This particular data structure (__-d__) is a simple conversion to __Lua__:

```lua
local data = { score = 1337, playerName = "Sean Plott", cheatMode = false }
```
__The following ACL structure is a bit more work:__

```bash
# Parse.com example code
curl -X POST \
  ...
  -d '{
        "name": "Moderators",
        "ACL": {
          "*": {
            "read": true
          }
        }
      }' \
  https://api.parse.com/1/roles
```
Again, from the __-d__ key above, a conversion to __Lua__ land:

```lua
local data = {
  name = "Moderators",
  ACL = {
    ["*"] = {
      read = true
    }
  }
}
```
__Query data require the same conversion:__

```bash
curl -X GET \
  ...
  --data-urlencode 'where={"score":{"$gte":1000,"$lte":3000}}' \
  https://api.parse.com/1/classes/GameScore
```

From __-data-urlencode__ flag to __Lua__:

```lua
local query = { score = { ["$gte"] = 1000, ["$lte"] = 3000 } }
```

> You might notice that the `where=` is not part of the query. This parameter is added during request processing.
