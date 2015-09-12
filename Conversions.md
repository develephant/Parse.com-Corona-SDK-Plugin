# Corona SDK Parse Plugin

## Conversions

In the Parse.com API guide you will see lots of usage examples. You need to do table conversions on the `data` you will send from Lua. In the examples, the `data` property is the __-d__ flag, followed by some JSON data.

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
