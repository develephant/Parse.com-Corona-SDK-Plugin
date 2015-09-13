# Corona SDK Parse Plugin

## Usage - Chapter 2

To get started with a new app, you'll need to gather both your __Application ID__ and your __REST API Key__ from your Parse.com dashboard settings area.

## Setting the Config

The plugin Config module handles app level data. We need to add the __Application ID__ and __REST API Key__ to the Config.

On the main page, or near the start of your app, you should set your Config values:

```lua
local parse = require 'plugin.parse'

parse.config:applicationId("your-application-id")
parse.config:restApiKey("your-rest-api-key")

```

> Now the auth data is stored and can be used for requests.

### Debug Mode

When you're developing, it's nice to see the data that is flowing through the app. You can turn on the debug flag to get a print out of data in your terminal. This can be set in your Config:

```lua
parse.config:debugEnabled()
```

This mode will print out the `response` data, but nothing more. If you'd like to see all the response, and some request data, add verbose debugging:

```lua
parse.config:debugEnabled()
parse.config:debugVerbose(true)
```

## Parsing It Out

You'll spend most of your time learning how to use the plugin, and Parse, by reading the [__Parse REST API guide__](https://www.parse.com/docs/rest/guide). It offers examples, useful notes, and advice for every piece of functionality in the API.

The Parse Plugin can handle every situation, but you will need to learn a bit about "translating" the curl examples on Parse.com, because sadly, it's not displayed in Lua. :sad:

### Some Tips for The Road Ahead

Here are some things to look out for in the Parse.com curl examples:

* A __-d__ flag is short for 'data', this pairs with the `:data()` or `:set()` methods.
* A __-data-urlencode__ flag pairs with the `:options()` method.
* A __`where={...}`__ will usually pair with the `:where()` method.
* Ignore any __-H__ flags (header). These are handled by the plugin.
* Ignore the url path, you'll use the request object constants.

Be sure to read the [Parse to Lua](Parse2Lua) entry.

### Examples

__Logging in a User__

```bash
curl -X GET \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  -H "X-Parse-Revocable-Session: 1" \
  -G \
  --data-urlencode 'username=cooldude6' \
  --data-urlencode 'password=p_n7!-e8' \
  https://api.parse.com/1/login
```

In this login example from Parse.com, we can see the structure of a "GET" method. You should notice the two __--data--urlencode__ values. This gives us a clue that we should us the `:options()` method. Since this is the login method, we need to use the correct endpoint object (See [Endpoints](Endpoints)). In this case that would be `parse.User.login`. Let's see what it would look like in the client code:

```lua
--Lua
parse.request( parse.User.login )
:options( { username = "cooldude6", password = "p_n7!-e8" } )
:response(cb)
```

__Check Session / Current User__

> A User must be logged in for the following to work.

```bash
curl -X GET \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  -H "X-Parse-Session-Token: r:pnktnjyb996sj4p156gjtp4im" \
  https://api.parse.com/1/users/me
```

This one is super simple. There isn't anything we need to convert, except the endpoint, which in this case would be `parse.User.me`. We also check for a `209` code from Parse, which is 'invalid session token'.

```lua
--Lua
parse.request( parse.User.me )
:response(function( ok, res, info )
  if res.code == 209 then
    --session is gone
    --need a relogin
  end
end)
```

__Get an Object by ID__

```bash
curl -X GET \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  https://api.parse.com/1/classes/GameScore/Ed1nuqPvcm
```

Another simple one:

```lua
parse.request( parse.Object.get, "GameScore", "Ed1nuqPvcm" )
:response(cb)
```

__Create an Object with raw JSON__

```bash
curl -X POST \
-H "X-Parse-Application-Id: aOeTz9iwexrJOh7a9mE9ZzE2swBpQP3fwgp82cdV" \
-H "X-Parse-REST-API-Key: ZbtvAjlxJ5obTDTwkG44FWYeepdaXJvNnxAFIDKr" \
-H "Content-Type: application/json" \
-d '{"playerName":"develephant","cheatMode":false}' \
https://api.parse.com/1/classes/GameScore
```

Generally you would use Lua tables in the plugin, but in certain cases it may be easier just to use the straight JSON.

```lua
parse.request( parse.Object.create, "GameScore" )
:data([[{"playerName":"develephant","cheatMode":false}]])
:response(cb)
```

For *literal strings* in Lua, you must enclose the content with double brackets on each end of the text `[[some string content]]`. Remember that spaces will be preserved so you need to make sure you are keeping the brackets in tight.

__Query an Object with raw JSON__

```bash
curl -X GET \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  -G \
  --data-urlencode 'where={"playerName":"develephant","cheatMode":false}' \
  https://api.parse.com/1/classes/GameScore
```

Even though it's __--data--urlencode__, the __where=__ takes precedence, so you would use a `:where()` method. Now, the key to using raw JSON in a `:where()` method is making sure there are no spaces between the double brackets, or the call will fail.

```lua
parse:request( parse.Object.query, "GameScore" )
:where([[{"playerName":"develephant","cheatMode":false}]])
:response(cb)
```

___In most cases you should use Lua tables for data, it's better for conversion and error handling. Plus you have a table.___

---

__Creating an Installation__

```bash
curl -X POST \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  -H "Content-Type: application/json" \
  -d '{
        "deviceType": "ios",
        "deviceToken": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
        "channels": [
          ""
        ]
      }' \
  https://api.parse.com/1/installations
```

This is a little more of a challenge and may work best with raw JSON, but we'll convert to tables instead:

```lua
parse.request( parse.Installation.create )
:data({
  deviceType = "ios",
  deviceToken = "0123456789abcdef0123456789ab",
  channels = {
    ""
  }
})
:response(cb)
```

__Sign up and login with Twitter__

```bash
curl -X POST \
  -H "X-Parse-Application-Id: 9Ad8ugrxMiwTpgzH7IG7fjKsE07Xevroofy3fS1K" \
  -H "X-Parse-REST-API-Key: bgc8cqUdipxZDyPINvilTg5vacyivf8bJ1VQcH2I" \
  -H "X-Parse-Revocable-Session: 1" \
  -H "Content-Type: application/json" \
  -d '{
        "authData": {
          "twitter": {
            "id": "12345678",
            "screen_name": "ParseIt",
            "consumer_key": "SaMpLeId3X7eLjjLgWEw",
            "consumer_secret": "SaMpLew55QbMR0vTdtOACfPXa5UdO2THX1JrxZ9s3c",
            "auth_token": "12345678-SaMpLeTuo3m2avZxh5cjJmIrAfx4ZYyamdofM7IjU",
            "auth_token_secret": "SaMpLeEb13SpRzQ4DAIzutEkCE2LBIm2ZQDsP3WUU"
          }
        }
      }' \
  https://api.parse.com/1/users
```
  
In __Lua__...


```lua
local data_tbl =
{
  authData = {
    twitter = {
      id = "12345678",
      screen_name = "ParseIt",
      consumer_key = "SaMpLeId3X7eLjjLgWEw",
      consumer_secret = "SaMpLew55QbMR0vTdtOACfPXa5UdO2THX1JrxZ9s3c",
      auth_token = "12345678-SaMpLeTuo3m2avZxh5cjJmIrAfx4ZYyamdofM7IjU",
      auth_token_secret = "SaMpLeEb13SpRzQ4DAIzutEkCE2LBIm2ZQDsP3WUU"
    }
  }
}

parse.request( parse.User.create )
:data( data_tbl )
:response(cb)
```
