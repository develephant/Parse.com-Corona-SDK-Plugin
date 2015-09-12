# Corona SDK Parse Plugin

## Getting Started

Read through the [__Parse REST API guide__](ps://www.parse.com/docs/rest/guide) at Parse.com to learn how to use the API.

The Parse.com guide provides an example of all the methods available. Following a few rules, all JSON example data can be converted into a Lua table structure. You can also use raw JSON strings in certain methods, if preferable.

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
