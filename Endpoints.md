# Corona SDK Parse Plugin

## Parse API Endpoints

The endpoint meta objects are used to provide the url, parameters, etc. for a specific request. It is always the first argument in a `parse.request` call, for example:

```lua
local req = parse.request( parse.User.login )
```

### Objects [parse.Object]

`.get`

`.query`

`.create`

`.update`

`.delete`

### Users [parse.User]

`.login`

`.logout`

`.me`

`.get`

`.query`

`.create`

`.update`

`.delete`

`.link`

`.unlink`

`.requestPasswordReset`

### Sessions [parse.Session]

`.me`

`.get`

`.query`

`.update`

`.delete`

`.logout`

### Roles [parse.Role]

`.get`

`.create`

`.update`

`.delete`

### Files [parse.File]

`.link`

`.delete`

See also [Working with Files](Files)

### Analytics [parse.Analytics]

`.AppOpened`

`.event`

### Push [parse.Push]

`.send`

### Installations [parse.Installation]

`.get`

`.query`

`.create`

`.update`

`.delete`

### Config [parse.Config]

`.get`

### Cloud [parse.Cloud]

`.call`

`.job`

### Schemas [parse.Schema]

`.getAll`

`.get`

`.create`

`.update`

`.delete`

### Apps [parse.App]

`.getAll`

`.get`

`.create`

`.update`

### Hooks [parse.Hook]

`.getAll`

`.get`

`.create`

`.update`

`.delete`

### Triggers [parse.Trigger]

`.getAll`

`.get`

`.create`

`.update`

`.delete`
