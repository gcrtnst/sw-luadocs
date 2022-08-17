# Main Menu Properties

The following functions will add editable UI elements to the Addon script selector when starting a new game. These functions will return null unless the game was started through the new game screen, so it is recommended to use them in onCreate while is_world_create is true OR in g_savedata where the nil value will be overwritten with the saved value on subsequent loads of the game.

A simple boolean checkbox.

```lua
property.checkbox(text, default_value)
```

A slider that is limited between two numbers.

```lua
property.slider(text, min, max, increment, default_value)
```

# Http

Send a Http request.

```lua
server.httpGet(port, request)
```

# Admin

Ban a player.

```lua
server.banPlayer(peer_id)
```

Kick a player.

```lua
server.kickPlayer(peer_id)
```

Give a player Admin.

```lua
server.addAdmin(peer_id)
```

Remove Admin from a player.

```lua
server.removeAdmin(peer_id)
```

Give a player Auth.

```lua
server.addAuth(peer_id)
```

Remove Auth from a player.

```lua
server.removeAuth(peer_id)
```

Send a save command for dedicated server, with optional save name parameter.

```lua
server.save((save_name))
```

# Misc

Get system time in ms (Can be used for random seeding).

```lua
system_time = server.getTimeMillisec()
```

# Developer

Get whether the game considers the tutorial active (Default missions check this before they spawn).

```lua
tutorial_completed = server.getTutorial()
```

Sets whether the game considers the tutorial active (useful if you are making your own tutorial).

```lua
server.setTutorial()
```

Gets whether the player has acknowledged the video tutorials (useful if you are making your own tutorial) Returns true on a dedicated server.

```lua
video_tutorial_completed = server.getVideoTutorial()
```

Returns true if the host player is a developer of the game.

```lua
is_dev = server.isDev()
```

Returns true if the server has the weapons DLC active.

```lua
is_enabled = server.dlcWeapons()
```
