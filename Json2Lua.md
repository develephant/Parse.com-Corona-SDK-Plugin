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

Be sure to check out the [__Parse REST API guide__](https://www.parse.com/docs/rest/guide) for more practice examples.
