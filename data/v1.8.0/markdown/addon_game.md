# Game

Attempts to spawn a tsunami epicentered at the target transform, only one tsunami/whirlpool can be active at a time; stronger events will override weaker ones. Magnitude ranges from 0-1.

```lua
is_success = server.spawnTsunami(transform_matrix, magnitude)
```

Attempts to spawn a whirlpool near to the target transform, can fail based on ocean depth, only one tsunami/whirlpool can be active at a time; stronger events will override weaker ones. Magnitude ranges from 0-1.

```lua
is_success = server.spawnWhirlpool(transform_matrix, magnitude)
```

Cancels the active ocean gerstner wave event (tsunami or whirlpool).

```lua
server.cancelGerstner()
```

Spawns a tornado at the target transform.

```lua
is_success = server.spawnTornado(transform_matrix)
```

Spawns a meteor to land at the target transform. Magnitude ranges from 0-1 and scales the main meteor up to 20x default size.

```lua
is_success = server.spawnMeteor(transform_matrix, magnitude, is_spawn_tsunami)
```

Spawns a meteor to land at the target location, preceded by several smaller meteors. Magnitude ranges from 0-1 and scales the main meteor up to 20x default size, this magnitude also increases the number of secondary meteors spawned.

```lua
is_success = server.spawnMeteorShower(transform_matrix, magnitude, is_spawn_tsunami)
```

Activates the closest volcano if the volcano tile is in simulation range.

```lua
is_success = server.spawnVolcano(transform_matrix)
```

Get a list of volcano data.

```lua
VOLCANOS = server.getVolcanos()
```

```lua

	VOLCANOS = {
		x = volcano world x
		y = volcano world y
		z = volcano world z
		tile_x = tile grid x
		tile_y = tile grid z
	}

```

Gets the blended oil amount at the target location.

```lua
oil_amount = server.getOilSpill(transform_matrix)
```

Sets the oil spill amount at the target location, this amount is blended across nearby tiles.

```lua
server.setOilSpill(transform_matrix, amount)
```

[Requires Search and Destroy DLC to be enabled] Spawn an explosion at the specified world position matrix.

```lua
server.spawnExplosion(transform_matrix, magnitude)
```

Set a game setting.

```lua
server.setGameSetting(GAME_SETTING, value)
```

Returns a table of the game settings indexed by the GAME_SETTING string, this can be accessed inline eg. server.getGameSettings().third_person

```lua
{[GAME_SETTING] = value} = server.getGameSettings()
```

```lua

	GAME_SETTING |
	"third_person",
	"third_person_vehicle",
	"vehicle_damage",
	"player_damage",
	"npc_damage",
	"sharks",
	"fast_travel",
	"teleport_vehicle",
	"rogue_mode",
	"auto_refuel",
	"megalodon",
	"map_show_players",
	"map_show_vehicles",
	"show_3d_waypoints",
	"show_name_plates",
	"day_night_length", -- currently cannot be written to
	"sunrise", -- currently cannot be written to
	"sunset", -- currently cannot be written to
	"infinite_money",
	"settings_menu",
	"unlock_all_islands",
	"infinite_batteries",
	"infinite_fuel",
	"engine_overheating",
	"no_clip",
	"map_teleport",
	"cleanup_vehicle",
	"clear_fow", -- clear fog of war
	"vehicle_spawning",
	"photo_mode",
	"respawning",
	"settings_menu_lock",
	"despawn_on_leave", -- despawn player characters when they leave a server
	"unlock_all_components",
	"override_weather",
	
```

Set game money and research points.

```lua
server.setCurrency(money, research_points)
```

Get game money.

```lua
amount = server.getCurrency()
```

Get game research points.

```lua
amount = server.getResearchPoints()
```

Get number of days since game start.

```lua
days_survived = server.getDateValue()
```

Get the current game date.

```lua
d, m, y = server.getDate()
```

Get the current game time.

```lua
CLOCK = server.getTime()
	CLOCK = {
		["hour"] = hour (24),
		["minute"] = minute (60),
		["daylight_factor"] = midday factor (0-1),
		["percent"] = day_cycle_percent (0-1),
	}

```

Get the current game weather at a location.

```lua
WEATHER = server.getWeather(transform_matrix)
	WEATHER = {
		["fog"] = fog factor (0-1),
		["rain"] = rain factor (0-1),
		["snow"] = snow factor (0-1),
		["wind"] = wind factor (0-1),
		["temp"] = temp factor (0-1),
	}

```

Sets the custom weather override values (0-1).

```lua
server.setWeather(fog, rain, wind)
```

Sets the target audio mood. Mood naturally decreases over time. -1 for all peers.

```lua
server.setAudioMood(peer_id, AUDIO_MOOD)
	AUDIO_MOOD |
		0 = none, (Cannot be set)
		1 = main_menu, (Cannot be set)
		2 = mood_normal,
		3 = mood_mission_mid,
		4 = mood_mission_high,

```

Returns the world position of a random ocean tile within the selected search range.

```lua
transform_matrix, is_success = server.getOceanTransform(transform_matrix, min_search_range, max_search_range)
```

Returns the generated ocean floor height offset of a tile. This is not terrain height and does not include mesh height. It is advised to only use this for ocean tiles. Example return value: -375

```lua
height = server.getOceanFloor(transform_matrix)
```

Returns the world position of a random tile of type tile_name closest to the supplied location. Optional search radius defaults to 50000.

```lua
transform_matrix, is_success = server.getTileTransform(transform_matrix, tile_name, [search_radius])
```

Returns the data for the tile at the specified location.

```lua
TILE_DATA, is_success = server.getTile(transform)
```

```lua

	TILE_DATA = {
		["name"] = tile_name, 
		["sea_floor"] = sea_floor_height, 
		["cost"] = purchase_cost, 
		["purchased"] = is_purchased, 
	}

```

Returns the data for the tile selected as the start tile in the game settings.

```lua
TILE_DATA = server.getStartTile()
```

```lua

	TILE_DATA = {
		["name"] = tile_name, 
		["x"] = tile_x, 
		["y"] = tile_y, 
		["z"] = tile_z, 
	}

```

Returns whether the tile at the given world coordinates is player owned.

```lua
is_purchased = server.getTilePurchased(transform_matrix)
```

Returns the current inventory amounts for the tile resource depot.

```lua
coal, uranium, diesel, jet_fuel = server.getTileInventory(transform_matrix)
```

Sets the inventory amounts for the tile resource depot.

```lua
server.setTileInventory(transform_matrix, coal, uranium, diesel, jet_fuel)
```

Returns whether matrix_object is within zone_size of matrix_zone.

```lua
is_in_area = server.isInTransformArea(matrix_object, matrix_zone, zone_size_x, zone_size_y, zone_size_z)
```

Returns a table of waypoints that form a path from start to end, matching the required tags, tags should be separated by commas with no spaces.

```lua
{ [i] = {x = world_x, z = world_z} } = server.pathfind(matrix_start, matrix_end, required_tags, avoided_tags)
```

Returns a table of waypoints tagged with ocean_path, that form a path from start to end. This function is the same as passing 'ocean_path' to the function above.

```lua
{ [i] = {x = world_x, z = world_z} } = server.pathfindOcean(matrix_start, matrix_end)
```

Returns a table of underground oil deposit positions.

```lua
{ [i] = {x = world_x, y = world_y, z = world_z, r = radius, oil = current_oil} } = server.getOilDeposits()
```
