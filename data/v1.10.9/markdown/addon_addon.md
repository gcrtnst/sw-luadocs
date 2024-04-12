# Addon

Get the internal index of this addon

```lua
addon_index, is_success = server.getAddonIndex()
```

Get the internal index of an active addon by its name (useful if you want to spawn components from another active addon)

```lua
addon_index, is_success = server.getAddonIndex(name)
```

Get the internal index of a location in the specified addon by its name (this index is local to the addon)

```lua
location_index, is_success = server.getLocationIndex(addon_index, name)
```

Directly spawn a location by name from the current addon, optional world transform parameter - otherwise spawns at first tile of the location type.

```lua
is_success = server.spawnNamedAddonLocation(name, (transform_matrix))
```

Spawn the specified mission location from the specified mission addon at  the specified world coordinates. A transform_matrix with x,y,z = 0,0,0 will spawn the location at a random location of the tile's type (useful for spawning missions on specific tiles)

```lua
out_transform_matrix, is_success = server.spawnAddonLocation(transform_matrix, addon_index, location_index)
```

Get the filepath of an addon, is_rom will only be true for DEV addons stored in the rom folder

```lua
path, is_success = server.getAddonPath(addon_name, is_rom)
```

Get a table of all active ENV MOD zones.

```lua
ZONE_LIST = server.getZones()
```

```lua

	ZONE_LIST = { 
		[zone_index] = { 
			["tags_full"] = tags, 
			["tags"] = { [i] = tag },
			["name"] = name, 
			["transform"] = transform_matrix, 
			["size"] = {x, y, z}, 
			["radius"] = radius, 
			["type"] = ZONE_TYPE,
			["parent_vehicle_id"] = parent_vehicle_id,
			["parent_relative_transform"] = relative_matrix
		}
	}

	ZONE_TYPE |
	0 = box,
	1 = sphere,
	2 = radius,

```

Get a table of all active ENV MOD zones that match the specified tag(s)

```lua
ZONE_LIST = server.getZones(tag(s))
```

Returns whether the specified world transform is within any ENV MOD zone that matches the display name. For specific zones, using isInTransformArea may be preferred.

```lua
is_in_zone, is_success = server.isInZone(transform_matrix, zone_display_name)
```

Get number of active addons.

```lua
count = server.getAddonCount()
```

Get table of addon data for the specified addon_index. Returns nil if the addon cannot be found.

```lua
ADDON_DATA = server.getAddonData(addon_index)
```

```lua

	ADDON_DATA = {
		["name"] = name, 
		["path_id"] = folder_path, 
		["file_store"] = is_app_data, 
		["location_count"] = location_count 
	}

```

Get table of location data for the specified location at the specified addon_index. Returns nil if the location cannot be found.

```lua
LOCATION_DATA, is_success = server.getLocationData(addon_index, location_index)
```

```lua

	LOCATION_DATA = {
		["name"] = name,
		["tile"] = tile_filename, 
		["env_spawn_count"] = spawn_count, 
		["env_mod"] = is_env_mod, 
		["component_count"] = component_count 
	}

```

Get table of component(object/vehicle) data for the specified component at the specified location at the specified addon_index. Returns nil if the component cannot be found.

```lua
COMPONENT_DATA, is_success = server.getLocationComponentData(addon_index, location_index, component_index)
```

```lua

	COMPONENT_DATA = {
		["tags_full"] = tags,
		["tags"] = { [i] = tag },
		["display_name"] = display_name, 
		["type"] = TYPE_STRING,
		["id"] = component_id,
		["dynamic_object_type"] = OBJECT_TYPE,
		["transform"] = transform_matrix, 
		["vehicle_parent_component_id"] = vehicle parent component id ,
		["character_outfit_type"] = OUTFIT_TYPE 
	}

```

Spawn the component(object/vehicle) at the specified component index at the specified location at the specified addon_index. Optional parent_vehicle_id param for fire and zone components.

```lua
COMPONENT, is_success = server.spawnAddonComponent(transform_matrix, addon_index, location_index, component_index, [parent_vehicle_id])
```

```lua

	COMPONENT = {
		["tags_full"] = tags, 
		["tags"] = { [i] = tag }, 
		["display_name"] = display_name, 
		["type"] = TYPE_STRING, 
		["transform"] = transform_matrix, 
		["id"] = object_id/main_vehicle_id 
		["object_id"] = object_id/main_vehicle_id 
        ["group_id"] = object_id/vehicle_id 
        ["vehicle_ids"] = { [i] = vehicle_id }
	}

```
