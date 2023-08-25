# Default Game Commands

The following commands can be called at any time and are built into the game:


Autosaves the game and live-reloads all active scripts and mission locations to allow for live debugging and editing of missions

```lua
?reload_scripts
```

Kicks the associated player from the game.

```lua
?kick <peer_id>
```

Bans the associated player from the game.

```lua
?ban <peer_id>
```

Give a player admin status. Authorize a player to use commands and bypass custom menu lock.

```lua
?add_admin <peer_id>
```

Remove admin status from a player.

```lua
?remove_admin <peer_id>
```

Give a player auth status. Authorize a player to use workbenches.

```lua
?add_auth <peer_id>
```

Remove auth status from a player.

```lua
?remove_auth <peer_id>
```

Dedicated server only, lets you force the dedicated server to save. save_name parameter is optional and default uses save_name from server config (If config setting is left blank it will save to autosave_server.)

```lua
?save <save_name>
```

# Lua scripting overview

Lua scripting gives you the tools to create advanced missions and custom gamemodes. Stormworks provides a number of functions that allow your script to interface with the game.
This guide outlines the functions that are available but is not a comprehensive tutorial on using the Lua language



# API General Info

peer_id can be found on the left side of the player list, singleplayer games always use peer_id 0

The coordinate system uses Y as the vertical axis for matrices and vectors in world space

The functionalities of arguments in CAPS are detailed below the corresponding function

peer_id can be passed as -1 to send for all connected peers

Any variables saved to a lua table named g_savedata will be saved out and loaded from a per-save lua_data.xml, you can use this to make your scripts persistent

For code that you want to run once at the start of the save use onCreate(is_world_create) and check is_world_create is true

Using server.announce() in onCreate will usually cause the messages to be sent before your client is connected and they will not be received

Remember to avoid the table length operator # and iPairs unless dealing with contiguous tables that start at index 1 (If a table is unexpectedly showing as length 0 this probably means it is not contiguous, the following function can be used for non - standard tables)

```lua

function tableLength(T)
	local count = 0
	for _ in pairs(T) do count = count + 1 end
	return count
end

```

# LUA FUNCTIONS

The following global lua functions are available:

- pairs
- ipairs
- next
- tostring
- tonumber

and additional functions are available through the following lua libraries:

- math
- table
- string

For full documentation of the functions provided by these libraries, visit https://www.lua.org/manual/.

# META FROM THE DEVS

This scripting API is very powerful and as such there are some important reminders to take note of:

- Your script has a max execution time of 1000 milliseconds, however it is still possible to create scripts that significantly slow down the game. It is your responsibility to ensure your script runs efficiently.

- peer_id can be passed as -1 to send for all connected peers

- Any variables saved to a lua table named g_savedata will be saved out and loaded from a per-save lua_data.xml, you can use this to make your scripts persistent

- A number of safeguards are in place to sandbox your script, however it is still possible to write scripts that will potentially crash your game. If you crash your game with a script, it's likely that you're doing something (very) wrong. This is your own responsibility. If you suspect you have encountered a legitimate bug, please report it on the Stormworks issue tracker (accessible from the pause-menu).

- Malicious and harmful scripts will not be tolerated on the Stormworks Steam Workshop.

Finally, enjoy the almost limitless possibilities that these scripts provide. This short wiki aims to give a good overview of how scripting in Stormworks works, however if you have any questions that are not covered here, please feel free to join us on Discord (accessible from the pause-menu)!
