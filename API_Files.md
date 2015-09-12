# Parse.com - Corona SDK Plugin

## Files [parse.File]

See [Working with Files](Files) for __upload__ and __download__ methods.

### .link

Link a file.

*Parameters:*

* __class__

```lua
parse.request( parse.File.link, "Pets" )
:response(cb)
```

### .delete

Delete a File.

* Parse provided file uri.

```lua
parse.request( parse.File.delete, "http://path-to-file" )
:response(cb)
```
