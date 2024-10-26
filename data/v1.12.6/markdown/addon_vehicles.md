# Vehicles

Spawns a vehicle component from a specific addon. See getLocationComponentData() for info on how to get component_id. group_vehicles is a table listing all vehicle ids in this group.

```lua
vehicle_id, is_success, group_vehicles = server.spawnAddonVehicle(transform_matrix, addon_index, component_id)
```

Spawns a vehicle from local appdata using its file name. group_vehicles is a table listing all vehicle ids in this group.

```lua
vehicle_id, is_success, group_vehicles = server.spawnVehicle(transform_matrix, save_name)
```

Sets a vehicle to despawn when out of a player's range. If is_instant the vehicle will instantly despawn no matter the player's proximity.

```lua
is_success = server.despawnVehicle(vehicle_id, is_instant)
```

Sets a all vehicles in a vehicle group to despawn when out of a player's range. If is_instant the vehicles will instantly despawn no matter the player's proximity.

```lua
is_success = server.despawnVehicleGroup(group_id, is_instant)
```

Gets the world position of the center of a vehicle's main body. Optionally passing a voxel position will return the world position of the specified voxel on the vehicle.

```lua
transform_matrix, is_success = server.getVehiclePos(vehicle_id, [voxel_x, voxel_y, voxel_z])
```

Converts a world transform to an astronomy transform. Used for navigating in Space.

```lua
astronomy_transform_matrix = server.getAstroPos(transform_matrix)
```

Teleports the specified vehicle to the target world position. The vehicle is unloaded and reloaded.

```lua
is_success = server.setVehiclePos(vehicle_id, transform_matrix)
```

Teleports the specified vehicle to the target world position. The vehicle is unloaded and reloaded. The vehicle is displaced by other vehicles at the arrival point.

```lua
is_success, result_matrix = server.setVehiclePosSafe(vehicle_id, transform_matrix)
```

Teleports all vehicles in the group to the target world position. The vehicle is unloaded and reloaded.

```lua
is_success = server.setGroupPos(group_id, transform_matrix)
```

Teleports all vehicles in the group to the target world position. The vehicle is unloaded and reloaded. The vehicle is displaced by other vehicles that are not in the group at the arrival point.

```lua
is_success, result_matrix = server.setGroupPosSafe(group_id, transform_matrix)
```

Moves the specified vehicle to the target world position.

```lua
is_success = server.moveVehicle(vehicle_id, transform_matrix)
```

Moves the specified vehicle to the target world position. The vehicle is displaced by other vehicles at the arrival point.

```lua
is_success, result_matrix = server.moveVehicleSafe(vehicle_id, transform_matrix)
```

Moves all vehicles in the group to the target world position.

```lua
is_success = server.moveGroup(group_id, transform_matrix)
```

Moves all vehicles in the group to the target world position. The vehicle is displaced by other vehicles that are not in the group at the arrival point.

```lua
is_success, result_matrix = server.moveGroupSafe(group_id, transform_matrix)
```

Checks if a zone of size xyz is clear of vehicles at the provided transform.

```lua
is_success = server.isLocationClear(transform_matrix, x, y, z)
```

Reloads the vehicle as if spawning from a workbench, refreshing damage and inventories etc.

```lua
is_success = server.resetVehicleState(vehicle_id)
```

Cleans up all player spawned vehicles.

```lua
server.cleanVehicles()
```

Cleans up all fallout zones.

```lua
server.clearRadiation()
```

Returns a table of vehicle ids in the vehicle group.

```lua
{ [i] = vehicle_id }, is_success = server.getVehicleGroup(group_id)
```

Returns a table of vehicle ids that match the name set by a map-icon-block.

```lua
{ [i] = vehicle_id }, is_success = server.getVehiclesByName(name)
```

Gets general data for a vehicle.

```lua
VEHICLE_DATA, is_success = server.getVehicleData(vehicle_id)
	VEHICLE_DATA = {
		["tags_full"] = tags, 
		["tags"] = { [i] = tag },
		["group_id"] = vehicle_group_id,
		["transform"] = transform_matrix, 
		["simulating"] = is_simulating, 
		["editable"] = is_editable, 
		["invulnerable"] = is_invulnerable, 
		["static"] = is_static,
		["name"] = map_icon_block_name,
		["authors"] = { [i] = { name = "name", steam_id = steam id } }

```

Gets advanced data for a LOADED vehicle. Including a list of attached character objects.

```lua
LOADED_VEHICLE_DATA, is_success = server.getVehicleComponents(vehicle_id)
	LOADED_VEHICLE_DATA = {
		["voxels"] = voxel count,
		["mass"] = mass, 
		["characters"] = { [i] = char_id },
		["components"] = { 
			["signs"] = { [i] = { SIGN_DATA } 
			["seats"] = { [i] = { SEAT_DATA }, 
			["buttons"] = { [i] = { BUTTON_DATA }, 
			["dials"] = { [i] = { DIAL_DATA } 
			["tanks"] = { [i] = { TANK_DATA } 
			["batteries"] = { [i] = { BATTERY_DATA } 
			["hoppers"] = { [i] = { HOPPER_DATA } 
			["guns"] = { [i] = { GUN_DATA } 
			["rope_hooks"] = { [i] = { ROPE_HOOK_DATA } 
		}
```

Each component contains the following data by default in addition to the type specific data detailed below in their specific get functions

```lua
VEHICLE_COMPONENT_DATA = { 
			["name"], 
			["pos"] = { 
				["x"] = voxel_x, 
				["y"] = voxel_y, 
				["z"] = voxel_z 
			} 
		}
	}
	

```

Returns the value of the first tank of the specified name or voxel position found on the specified vehicle. Stormworks uses Centi-Litres behind the scenes and as such values here will reflect that (10x Litres).

```lua
DATA, is_success = server.getVehicleTank(vehicle_id, tank_name)
```

```lua
DATA, is_success = server.getVehicleTank(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["value"] = current_held_total, 
		["values"] = { FLUID_TYPE = amount}, 
		["capacity"] = total_capacity, 
		["fluid_type"] = FLUID_TYPE (set in tank properties), 
	}

	FLUID_TYPE |
	0 = fresh water,
	1 = diesel,
	2 = jet fuel,
	3 = air,
	4 = exhaust,
	5 = oil,
	6 = sea water,
	7 = steam,
	8 = slurry,
	9 = saturated slurry,
	10 = oxygen,
	11 = nitrogen,
	12 = hydrogen,

```

Returns the data of the first seat of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleSeat(vehicle_id, seat_name)
```

```lua
DATA, is_success = server.getVehicleSeat(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["seated_id"] = seated_object_id (character or creature),
		["seated_peer_id"] = seated_peer_id (if character is a player), 
	}

```

Returns the state of the first button of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleButton(vehicle_id, button_name)
```

```lua
DATA, is_success = server.getVehicleButton(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		} 
		["on"] = is_on, 
	}

```

Returns the voxel position of the first sign of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleSign(vehicle_id, sign_name)
```

```lua
DATA, is_success = server.getVehicleSign(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		}
	}

```

Returns the value of the first dial of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleDial(vehicle_id, dial_name)
```

```lua
DATA, is_success = server.getVehicleDial(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["value"] = value_primary, 
		["value2"] = value_secondary, 
	}

```

Returns the resource data of the first hopper of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleHopper(vehicle_id, hopper_name)
```

```lua
DATA, is_success = server.getVehicleHopper(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["values"] = { RESOURCE_TYPE = amount}, 
		["capacity"] = total_capacity, 
	}

RESOURCE_TYPE |
	0 = coal,
	1 = iron,
	2 = aluminium,
	3 = gold,
	4 = gold_dirt,
	5 = uranium,
	6 = ingot_iron,
	7 = ingot_steel,
	8 = ingot_aluminium,
	9 = ingot_gold_impure,
	10 = ingot_gold,
	11 = ingot_uranium,
	12 = solid_propellant,
	13 = anchovie,
	14 = anglerfish,
	15 = arctic_char,
	16 = ballan_lizardfish,
	17 = ballan_wrasse,
	18 = barreleye_fish,
	19 = black_bream,
	20 = black_dragonfish,
	21 = clown_fish,
	22 = cod,
	23 = dolphinfish,
	24 = gulper_eel,
	25 = haddock,
	26 = hake,
	27 = herring,
	28 = john_dory,
	29 = labrus,
	30 = lanternfish,
	31 = mackerel,
	32 = midshipman,
	33 = perch,
	34 = pike,
	35 = pinecone_fish,
	36 = pollock,
	37 = red_mullet,
	38 = rockfish,
	39 = sablefish,
	40 = salmon,
	41 = sardine,
	42 = scad,
	43 = sea_bream,
	44 = sea_halibut,
	45 = sea_piranha,
	46 = seabass,
	47 = slimehead,
	48 = snapper,
	49 = snapper_gold,
	50 = snook,
	51 = spadefish,
	52 = trout,
	53 = tubeshoulders_fish,
	54 = viperfish,
	55 = yellowfin_tuna,
	56 = blue crab,
	57 = brown_box_crab,
	58 = coconut_crab,
	59 = dungeness_crab,
	60 = furry_lobster,
	61 = homarus_americanus, (Atlantic Lobster)
	62 = homarus_gammarus, (Common Lobster)
	63 = horseshoe_crab,
	64 = jasus_edwardsii, (Red Rock Lobster)
	65 = jasus_lalandii, (Cape Rock Lobster)
	66 = jonah_crab,
	67 = king_crab,
	68 = mud_crab,
	69 = munida_lobster,
	70 = ornate_rock_lobster,
	71 = panulirus_interruptus,
	72 = red_king_crab,
	73 = reef_lobster,
	74 = slipper_lobster,
	75 = snow_crab,
	76 = southern_rock_lobster,
	77 = spider_crab,
	78 = spiny_lobster,
	79 = stone_crab

```

Returns the data of the first battery of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleBattery(vehicle_id, battery_name)
```

```lua
DATA, is_success = server.getVehicleBattery(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["charge"] = current_charge, 
	}

```

Returns the data of the first weapon component of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleWeapon(vehicle_id, name)
```

```lua
DATA, is_success = server.getVehicleWeapon(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		},
		["ammo"] = current_ammo, 
		["capacity"] = total_ammo_capacity, 
	}

```

Returns the data of the first rope anchor component of the specified name or voxel position found on the specified vehicle.

```lua
DATA, is_success = server.getVehicleRopeHook(vehicle_id, name)
```

```lua
DATA, is_success = server.getVehicleRopeHook(vehicle_id, voxel_x, voxel_y, voxel_z)
```

```lua
DATA = {
		["name"], 
		["pos"] = { 
			["x"] = voxel_x, 
			["y"] = voxel_y, 
			["z"] = voxel_z 
		}
	}

```

Applies a set fluid action to the first tank of the specified name or voxel position found on the specified vehicle. Fluid of the same state(gas or liquid) as the target type will be cleared when this function is triggered, therefore to fully clear a tank call this function twice, one for gases and one for liquids. Stormworks uses Centi-Litres behind the scenes and as such values here should reflect that (10x Litres).

```lua
server.setVehicleTank(vehicle_id, tank_name, amount, FLUID_TYPE)
server.setVehicleTank(vehicle_id, voxel_x, voxel_y, voxel_z, amount, FLUID_TYPE)

```

Override the inputs to the first seat of the specified name or voxel position found on the specified vehicle. A seated player will prevent overrides.

```lua
server.setVehicleSeat(vehicle_id, seat_name, axis_w, axis_d, axis_up, axis_right, button1, button2, button3, button4, button5, button6, trigger)
```

```lua
server.setVehicleSeat(vehicle_id, voxel_x, voxel_y, voxel_z, axis_w, axis_d, axis_up, axis_right, button1, button2, button3, button4, button5, button6, trigger)
```

Applies a press action to the first button of the specified name or voxel position found on the specified vehicle.

```lua
server.pressVehicleButton(vehicle_id, button_name)
```

```lua
server.pressVehicleButton(vehicle_id, voxel_x, voxel_y, voxel_z)
```

Applies a set number action to the first keypad of the specified name or voxel position found on the specified vehicle.

```lua
server.setVehicleKeypad(vehicle_id, keypad_name, value, (value2))
```

```lua
server.setVehicleKeypad(vehicle_id, voxel_x, voxel_y, voxel_z, value, (value2))
```

Sets the number of a specific type of resource object inside a hopper of the specified name or voxel position found on the specified vehicle.

```lua
server.setVehicleHopper(vehicle_id, hopper_name, amount, RESOURCE_TYPE))
```

```lua
server.setVehicleHopper(vehicle_id, voxel_x, voxel_y, voxel_z, amount, RESOURCE_TYPE)
```

Applies a set charge action to the first battery of the specified name or voxel position found on the specified vehicle. 0 to 1 range.

```lua
server.setVehicleBattery(vehicle_id, battery_name, amount)
```

```lua
server.setVehicleBattery(vehicle_id, voxel_x, voxel_y, voxel_z, amount)
```

Applies a set ammo action to the first weapon component of the specified name or voxel position found on the specified vehicle. 0 to 1 range.

```lua
server.setVehicleWeapon(vehicle_id, name, amount)
```

```lua
server.setVehicleWeapon(vehicle_id, voxel_x, voxel_y, voxel_z, amount)
```

Spawns a rope between two rope anchors on the specified vehicles at the provided rope hook component voxel positions. Length will be clamped to at least the distance between voxels. Length of 0 will spawn the rope at the clamped minimum. Currently does not fully support pulleys second rope slot.

```lua
server.spawnVehicleRope(vehicle_id_1, voxel_x_1, voxel_y_1, voxel_z_1, vehicle_id_2, voxel_x_2, voxel_y_2, voxel_z_2, length, ROPE_TYPE)
	ROPE_TYPE |
	0 = rope,
	1 = hose,
	2 = electric cable,
	3 = N/A
	4 = suspension cable,
	5 = N/A,
	6 = Fishing line,

```

Get the number of burning surfaces on a specified vehicle.

```lua
surface_count, is_success = server.getVehicleFireCount(vehicle_id)
```

Set the default block tooltip of a vehicle to display some text. Blocks with unique tooltips (e.g. buttons) will override this tooltip.

```lua
is_success = server.setVehicleTooltip(vehicle_id, text)
```

Applies impact damage to a vehicle at the specified voxel location. Damage maxiumum is 100. Radius is in meters. Negative damage values will instead repair the area.

```lua
is_success = server.addDamage(vehicle_id, damage, voxel_x, voxel_y, voxel_z, radius)
```

Returns whether the specified vehicle has finished loading and is simulating.

```lua
is_simulating, is_success = server.getVehicleSimulating(vehicle_id)
```

Returns whether the specified vehicle is loading, simulating or unloading.

```lua
is_local, is_success = server.getVehicleLocal(vehicle_id)
```

Sets a vehicle's global transponder to active. (All vehicles have a global transponder that can be active even if a vehicle is not loaded).

```lua
is_success = server.setVehicleTransponder(vehicle_id, is_active)
```

Sets a vehicle to be editable by players. If a vehicle is spawned by a script it will not have a parent workbench until edited by one (Edit vehicle in zone).

```lua
is_success = server.setVehicleEditable(vehicle_id, is_editable)
```

Sets a vehicle to be invulnerable to damage.

```lua
is_success = server.setVehicleInvulnerable(vehicle_id, is_invulnerable)
```

Sets a vehicle to show on the map.

```lua
is_success = server.setVehicleShowOnMap(vehicle_id, is_show_on_map)
```
