# Player

Returns a table containing info on all connected players.

```lua
PLAYER_LIST = server.getPlayers()
```

```lua

	PLAYER_LIST |
	{ [peer_index] = { ["id"] = peer_id, ["name"] = name, ["admin"] = is_admin, ["auth"] = is_auth, ["steam_id"] = steam_id }}

```

Returns the player name of the specified peer as it appears to the server.

```lua
name, is_success = server.getPlayerName(peer_id)
```

Gets the world position of a specified peer as a matrix.

```lua
transform_matrix, is_success = server.getPlayerPos(peer_id)
```

Teleports the specified player to the target world position.

```lua
is_success = server.setPlayerPos(peer_id, transform_matrix)
```

Returns the forward vector of the specified player's camera

```lua
x, y, z, is_success = server.getPlayerLookDirection(peer_id)
```

# Objects

All dynamic objects in Stormworks have an object ID, Player characters have ownership of a dynamic object that can be manipulated with the following functions just like any NPC or physics object. Please note that peer_id and object_id are separate systems; the following function can convert from peer id to object id to allow manipulation of player characters.

Get a specified player's character object id.

```lua
object_id, is_success = server.getPlayerCharacterID(peer_id)
```

Spawn the specified object at the specified world position.

```lua
object_id, is_success = server.spawnObject(transform_matrix, OBJECT_TYPE)
```

```lua

	OBJECT_TYPE |
	0 = none,
	1 = character,
	2 = crate_small,
	3 = collectable, (Not spawnable)
	4 = basketball,
	5 = television,
	6 = barrel,
	7 = schematic,  (Not spawnable)
	8 = debris,  (Not spawnable)
	9 = chair,
	10 = trolley_food,
	11 = trolley_med,
	12 = clothing,  (Not spawnable)
	13 = office_chair,
	14 = book,
	15 = bottle,
	16 = fryingpan,
	17 = mug,
	18 = saucepan,
	19 = stool,
	20 = telescope,
	21 = log,
	22 = bin,
	23 = book_2,
	24 = loot,
	25 = blue_barrel,
	26 = buoyancy_ring,
	27 = container,
	28 = gas_canister,
	29 = pallet,
	30 = storage_bin,
	31 = fire_extinguisher,
	32 = trolley_tool,
	33 = cafetiere,
	34 = drawers_tools,
	35 = glass,
	36 = microwave,
	37 = plate,
	38 = box_closed,
	39 = box_open,
	40 = desk_lamp,
	41 = eraser_board,
	42 = folder,
	43 = funnel,
	44 = lamp,
	45 = microscope,
	46 = notebook,
	47 = pen_marker,
	48 = pencil,
	49 = scales,
	50 = science_beaker,
	51 = science_cylinder,
	52 = science_flask,
	53 = tub_1,
	54 = tub_2,
	55 = filestack,
	56 = barrel_toxic,
	57 = flare,
	58 = fire,
	59 = animal,
	60 = map_label,  (Not spawnable)
	61 = iceberg,  (Not spawnable)
	62 = gun_flare,
	63 = vehicle_flare,
	64 = ammo_shell,
	65 = binoculars,
	66 = C4,
	67 = grenade,
	68 = vehicle_flare,
	69 = coal,
	70 = meteorite,
	71 = glowstick,
	72 = creature,

```

Spawn a world fire at the specified world position matrix. parent_vehicle_id should be 0 if the fire should not move relative to a vehicle. Fires will slowly grow until they reach 1 magnitude.

```lua
object_id, is_success = server.spawnFire(transform_matrix, fire_size, fire_magnitude, is_lit, is_explosive, parent_vehicle_id, explosion_magnitude)
```

Spawn a character object with an optional outfit at the specified world postion.

```lua
object_id, is_success = server.spawnCharacter(transform_matrix, (OUTFIT_TYPE))
```

```lua

	OUTFIT_TYPE |
	0 = none,
	1 = worker,
	2 = fishing,
	3 = waiter,
	4 = swimsuit,
	5 = military,
	6 = office,
	7 = police,
	8 = science,
	9 = medical,
	10 = wetsuit,
	11 = civilian
```

Spawn a scenery animal at the specified world postion.

```lua
object_id, is_success = server.spawnAnimal(transform_matrix, ANIMAL_TYPE, size_multiplier)
```

```lua

	ANIMAL_TYPE |
	0 = shark,
	1 = whale,
	4 = kraken
```

[Requires Industrial Frontier DLC to be enabled] Spawn an animal/creature at the specified world postion.

```lua
object_id, is_success = server.spawnCreature(transform_matrix, CREATURE_TYPE, size_multiplier)
```

```lua

	CREATURE_TYPE |
	0 = badger_common,
	1 = bear_grizzly,
	2 = bear_black,
	3 = bear_polar,
	4 = chicken_barnevelder,
	5 = chicken_marans,
	6 = chicken_orpington_fowl,
	7 = chicken_sussex_fowl,
	8 = cow_angus,
	9 = cow_hereford,
	10 = cow_highland,
	11 = cow_holstein,
	12 = sasquatch,
	13 = yeti 
	14 = deer_red_f,
	15 = deer_red_m,
	16 = deer_sika_f,
	17 = deer_sika_m,
	18 = dog_beagle,
	19 = dog_border_collie,
	20 = dog_boxer,
	21 = dog_corgi,
	22 = dog_dachschund,
	23 = dog_dalmatian,
	24 = dog_dobermann,
	25 = dog_german_shepherd,
	26 = dog_greyhound,
	27 = dog_jack_russell,
	28 = dog_labrador,
	29 = dog_newfoundland,
	30 = dog_pug,
	31 = dog_shiba,
	32 = dog_siberian_husky,
	33 = dog_st_bernard,
	34 = dog_vizsla,
	35 = dog_yorkshire_terrier,
	36 = fox_red,
	37 = fox_arctic,
	38 = goat_alpine,
	39 = goat_bengal,
	40 = goat_oberhasli,
	41 = goat_saanen,
	42 = hare_arctic,
	43 = hare_irish,
	44 = hare_mountain,
	45 = horse_clydesdale,
	46 = horse_friesian,
	47 = horse_haflinger,
	48 = horse_welara,
	49 = muntjac_f,
	50 = muntjac_m,
	51 = penguin_gentoo,
	52 = pig_angeln_saddleback,
	53 = pig_old_spot,
	54 = pig_tamworth,
	55 = pig_yorkshire,
	56 = seal_polar,
	57 = sheep_black_nose,
	58 = sheep_highlander,
	59 = sheep_mule,
	60 = wildcat_scottish,
	61 = wolf_arctic,
	62 = wolf_costal,
	63 = wolf_plains,

	64 = zombie_male,
	65 = zombie_male_a,
	66 = zombie_male_b,
	67 = zombie_male_c,
	68 = zombie_male_d,
	69 = zombie_male_e,
	70 = zombie_male_f,
	71 = zombie_male_g,
	72 = zombie_male_nurse,
	73 = zombie_male_arctic,
	74 = zombie_male_firefighter,
	75 = zombie_male_pilot,
	76 = zombie_male_police,
	77 = zombie_male_ranger,
	78 = zombie_male_scuba,
	79 = zombie_male_tree_surgeon,
	80 = zombie_female,
	81 = zombie_female_a,
	82 = zombie_female_b,
	83 = zombie_female_c,
	84 = zombie_female_d,
	85 = zombie_female_e,
	86 = zombie_female_f,
	87 = zombie_female_arctic,
	88 = zombie_female_firefighter,
	89 = zombie_female_hazmat,
	90 = zombie_female_pilot,
	91 = zombie_female_pirate,
	92 = zombie_female_police,
	93 = zombie_female_safari,
	94 = zombie_female_sar,
	95 = zombie_female_scuba,
	96 = zombie_female_surgeon,
	97 = buffalo,
	98 = sheep_bighorn,
	99 = roadrunner,
	100 = lion_mountain,
    101 = crocodile,
    102 = coyote,

```

[Requires Industrial Frontier DLC to be enabled] Set the next target position for a creature to path towards.

```lua
is_success = server.setCreatureMoveTarget(object_id, transform_matrix)
```

Spawns an equipment item dynamic object.

```lua
object_id, is_success = server.spawnEquipment(transform_matrix, EQUIPMENT_ID, int, float)
```

```lua

	EQUIPMENT_ID |
Outfits
	0 = none,
	1 = diving,
	2 = firefighter,
	3 = scuba,
	4 = parachute, [int = {0 = deployed, 1 = ready}]
	5 = arctic,
	29 = hazmat,
	74 = bomb_disposal,
	75 = chest_rig,
	76 = black_hawk_vest
	77 = plate_vest,
	78 = armor_vest,
Items
	6 = binoculars,
	7 = cable,
	8 = compass,
	9 = defibrillator, [int = charges]
	10 = fire_extinguisher, [float = ammo]
	11 = first_aid, [int = charges]
	12 = flare, [int = charges]
	13 = flaregun, [int = ammo]
	14 = flaregun_ammo, [int = ammo]
	15 = flashlight, [float = battery]
	16 = hose, [int = {0 = hose off, 1 = hose on}]
	17 = night_vision_binoculars, [float = battery]
	18 = oxygen_mask, [float = oxygen]
	19 = radio, [int = channel] [float = battery]
	20 = radio_signal_locator, [float = battery]
	21 = remote_control, [int = channel] [float = battery]
	22 = rope, [int = {0 = default length, 1 = 1m, 2 = 2m, 3 = 4m, 4 = 8m, 5 = 16m}]
	23 = strobe_light, [int = {0 = off, 1 = on}] [float = battery]
	24 = strobe_light_infrared, [int = {0 = off, 1 = on}] [float = battery]
	25 = transponder, [int = {0 = off, 1 = on}] [float = battery]
	26 = underwater_welding_torch, [float = charge]
	27 = welding_torch, [float = charge]
	28 = coal,
	30 = radiation_detector, [float = battery]
	31 = c4, [int = ammo]
	32 = c4_detonator,
	33 = speargun, [int = ammo]
	34 = speargun_ammo,
	35 = pistol, [int = ammo]
	36 = pistol_ammo,
	37 = smg, [int = ammo]
	38 = smg_ammo,
	39 = rifle, [int = ammo]
	40 = rifle_ammo,
	41 = grenade, [int = ammo]
	42 = machine_gun_ammo_box_k,
	43 = machine_gun_ammo_box_he,
	44 = machine_gun_ammo_box_he_frag,
	45 = machine_gun_ammo_box_ap,
	46 = machine_gun_ammo_box_i,
	47 = light_auto_ammo_box_k,
	48 = light_auto_ammo_box_he,
	49 = light_auto_ammo_box_he_frag,
	50 = light_auto_ammo_box_ap,
	51 = light_auto_ammo_box_i,
	52 = rotary_auto_ammo_box_k,
	53 = rotary_auto_ammo_box_he,
	54 = rotary_auto_ammo_box_he_frag,
	55 = rotary_auto_ammo_box_ap,
	56 = rotary_auto_ammo_box_i,
	57 = heavy_auto_ammo_box_k,
	58 = heavy_auto_ammo_box_he,
	59 = heavy_auto_ammo_box_he_frag,
	60 = heavy_auto_ammo_box_ap,
	61 = heavy_auto_ammo_box_i,
	62 = battle_shell_k,
	63 = battle_shell_he,
	64 = battle_shell_he_frag,
	65 = battle_shell_ap,
	66 = battle_shell_i,
	67 = artillery_shell_k,
	68 = artillery_shell_he,
	69 = artillery_shell_he_frag,
	70 = artillery_shell_ap,
	71 = artillery_shell_i,
	72 = glowstick,
	73 = dog_whistle,

```

Despawn the specified object when it is out of a player's range. is_instant will instantly despawn the object.

```lua
is_success = server.despawnObject(object_id, is_instant)
```

Get the world position of a specified object. is_success returns false if the object cannot be found.

```lua
transform_matrix, is_success = server.getObjectPos(object_id)
```

Get the simulating state of a specified object. is_success returns false if the object cannot be found.

```lua
is_simulating, is_success = server.getObjectSimulating(object_id)
```

Set the world position of a specified object. is_success returns false if the object cannot be found.

```lua
is_success = server.setObjectPos(object_id, transform_matrix)
```

Set data for an existing world fire using its object_id.

```lua
server.setFireData(object_id, is_lit, is_explosive)
```

Get data for a world fire using its object_id.

```lua
is_lit, is_success = server.getFireData(object_id)
```

Kills the target character.

```lua
server.killCharacter(object_id)
```

Revives the target character.

```lua
server.reviveCharacter(object_id)
```

Sets the target character (or sit-able creature) to be seated in the first seat with the specified name found on the specified vehicle. Aliases: setCharacterSeated, setCreatureSeated

```lua
server.setSeated(object_id, vehicle_id, seat_name)
```

Sets the target character (or sit-able creature) to be seated in the seat with the specified voxel position found on the specified vehicle. Aliases: setCharacterSeated, setCreatureSeated

```lua
server.setSeated(object_id, vehicle_id, x, y, z)
```

Get character data for a specified character object. Returns a table if successful and nil upon failure. (Aliased to getCharacterData())

```lua
OBJECT_DATA = server.getObjectData(object_id)
```

```lua

	OBJECT_DATA = { 
		["object_type"] = OBJECT_TYPE
		["hp"] = hp, 
		["incapacitated"] = is_incapacitated, 
		["dead"] = is_dead, 
		["interactable"] = is_interactable,
		["ai"] = is_ai,
		["name"] = name,
		["creature_type"] = CREATURE_TYPE,
		["scale"] = scale,
	} 
```

Get the current vehicle_id for a specified character object.

```lua
vehicle_id, is_success = server.getCharacterVehicle(object_id)
```

Set character data for a specified character object. Non-interactable characters are frozen in place and cannot be moved. is_interactable has no effect on Player characters.

```lua
server.setCharacterData(object_id, hp, is_interactable, is_ai)
```

Sets the display name for a non-player character or creature.

```lua
server.setCharacterTooltip(object_id, display_name)
```

```lua
server.setCreatureTooltip(object_id, display_name)
```

Set the item slot data for a specified character object. Certain equipments hold data that can be initialized as detailed below.

```lua
is_success = server.setCharacterItem(object_id, SLOT_NUMBER, EQUIPMENT_ID, is_active, [integer_value], [float_value])
```

```lua

    SLOT_NUMBER |
    1 = Large Equipment Slot, 
    2, 3, 4, 5, 6, 7, 8, 9 = Small Equipment Slot, 
    10 = Outfit Slot
```

Get the item in the specified slot for a specified character object.

```lua
EQUIPMENT_ID, is_success = server.getCharacterItem(object_id, SLOT_NUMBER)
```
