# Callback Functions

Listed below are callback functions that can be added to a script and are automatically called when their specific conditions are met, the simplest callback function is onTick which is automatically called every game tick.

Called every game tick. game_ticks refers to the number of ticks that have passed this frame (normally 1, while sleeping 400).

```lua
function onTick(game_ticks)
```

onCreate is called when the script is initialized (whenever creating or loading a world. is_world_create is true only on world generate (first load).

```lua
function onCreate(is_world_create)
```

onDestroy is called whenever the world is exited.

```lua
function onDestroy()
```

onCustomCommand is called when a command is typed into chat. full_message contains the entire message including spaces, command contains the first parameter including the ? e.g. ?teleport, args ... represents the variadic arguments of the command (can also be explicitly declared, see example below)

```lua
function onCustomCommand(full_message, user_peer_id, is_admin, is_auth, command, args ...)
```

onChatMessage is called when a chat message is posted.

```lua
function onChatMessage(peer_id, sender_name, message)
```

onPlayerJoin is called when a player joins the game.

```lua
function onPlayerJoin(steam_id, name, peer_id, is_admin, is_auth)
```

onPlayerSit is called when a player sits in a seat.

```lua
function onPlayerSit(peer_id, vehicle_id, seat_name)
```

onPlayerUnsit is called when a player gets out of a seat.

```lua
function onPlayerUnsit(peer_id, vehicle_id, seat_name)
```

onCharacterSit is called when any character (including players) sits in a seat.

```lua
function onCharacterSit(object_id, vehicle_id, seat_name)
```

onCharacterUnsit is called when a any character (including players)gets out of a seat.

```lua
function onCharacterUnsit(object_id, vehicle_id, seat_name)
```

onCharacterPickup is called when a character object picks up a character.

```lua
function onCharacterPickup(object_id_actor, object_id_target)
```

onCreatureSit is called when any creature sits in a seat.

```lua
function onCreatureSit(object_id, vehicle_id, seat_name)
```

onCreatureUnsit is called when a any creature gets out of a seat.

```lua
function onCreatureUnsit(object_id, vehicle_id, seat_name)
```

onCreaturePickup is called when a character object picks up a creature.

```lua
function onCreaturePickup(object_id_actor, object_id_target, CREATURE_TYPE)
```

onEquipmentPickup is called when a character object picks up an equipment Item.

```lua
function onEquipmentPickup(object_id_actor, object_id_target, EQUIPMENT_TYPE)
```

onEquipmentDrop is called when a character object drops an equipment Item.

```lua
function onEquipmentDrop(object_id_actor, object_id_target, EQUIPMENT_TYPE)
```

onPlayerRespawn is called when a player respawns.

```lua
function onPlayerRespawn(peer_id)
```

onPlayerLeave is called when a player leaves the game.

```lua
function onPlayerLeave(steam_id, name, peer_id, is_admin, is_auth)
```

onToggleMap is called when a player opens/closes the map. is_open represents whether their map is open.

```lua
function onToggleMap(peer_id, is_open)
```

onPlayerDie is called when a player dies.

```lua
function onPlayerDie(steam_id, name, peer_id, is_admin, is_auth)
```

onGroupSpawn is called when a vehicle group is spawned. If group is spawned by a script peer_id will be -1. All vehicles in a group must still load locally so they can begin simulating for players. Cost is currently only calculated for player spawned vehicle groups. x, y, z are the group's spawn coordinates in world space.

```lua
function onGroupSpawn(group_id, peer_id, x, y, z, group_cost)
```

onVehicleSpawn is called when a vehicle is spawned. If vehicle is spawned by a script peer_id will be -1. Spawned vehicles must still load locally so they can begin simulating for players. Cost is currently only calculated for player spawned vehicle groups. x, y, z are the group's spawn coordinates in world space. For physics-accurate sub-grid transform values the vehicles must be loaded to initialize their physics which then acts as their new base transform; Until the physics is created unloaded vehicles always treat their group origin as their position.

```lua
function onVehicleSpawn(vehicle_id, peer_id, x, y, z, group_cost, group_id)
```

onVehicleDespawn is called when a vehicle is despawned. If vehicle is despawned by a script peer_id will be -1.

```lua
function onVehicleDespawn(vehicle_id, peer_id)
```

onVehicleLoad is called when a vehicle has loaded and is ready to simulate.

```lua
function onVehicleLoad(vehicle_id)
```

onVehicleUnload is called when a vehicle has unloaded and is no longer simulating.

```lua
function onVehicleUnload(vehicle_id)
```

onVehicleTeleport is called when a vehicle is teleported or returned to workbench. If vehicle is teleported by a script peer_id will be -1. x,y,z are the destination coordinates in world space.

```lua
function onVehicleTeleport(vehicle_id, peer_id, x, y, z)
```

onObjectLoad is called when an object (character/prop/animal) has loaded and is ready to simulate.

```lua
function onObjectLoad(object_id)
```

onObjectUnload is called when an object (character/prop/animal) has unloaded and is no longer simulating.

```lua
function onObjectUnload(object_id)
```

onButtonPress is called when a button is interacted with (still triggers on locked buttons). To get a button's current state please use getVehicleButton()

```lua
function onButtonPress(vehicle_id, peer_id, button_name, is_pressed)
```

onSpawnAddonComponent is called when a vehicle or object is spawned by a script. addon_index is the internal index of the addon the object was spawned from (see mission functions below)

```lua
function onSpawnAddonComponent(object_id/vehicle_id, component_name, TYPE_STRING, addon_index)
```

```lua

	TYPE_STRING |
	"zone",
	"object",
	"character",
	"vehicle",
	"flare",
	"fire",
	"loot",
	"button",
	"animal"
	"ice"
```

onVehicleDamaged is called when a vehicle is damaged or repaired. Damage amount will be negative if the component is repaired. The voxel parameters refer to the voxel position on the vehicle that sustained the damage relative to the origin of the vehicle. body_index is 0 for the main vehicle body, checking this parameter may be helpful for vehicles with sub bodies such as missiles that should be ignored.

```lua
function onVehicleDamaged(vehicle_id, damage_amount, voxel_x, voxel_y, voxel_z, body_index)
```

httpReply is called when a HTTP request has returned. The callback details the request and the received reply.

```lua
function httpReply(port, request, reply)
```

onFireExtinguished is called when a fire is extinguished. The returned coordinates represent the fire's world coordinates.

```lua
function onFireExtinguished(fire_x, fire_y, fire_z)
```

onForestFireSpawned is called when 5 or more trees are detected to be on fire within a small radius. The returned coordinates represent the fire's world coordinates. The objective ID is used to track separate forest fire events.

```lua
function onForestFireSpawned(fire_objective_id, fire_x, fire_y, fire_z)
```

onForestFireExtinguished is called when all trees within a forest fire objective have been extinguished. The returned coordinates represent the fire's world coordinates. The objective ID is used to track separate forest fire events.

```lua
function onForestFireExtinguished(fire_objective_id, fire_x, fire_y, fire_z)
```

Called when a tornado is spawned.

```lua
function onTornado(transform)
```

Called when a meteor is spawned.

```lua
function onMeteor(transform, magnitude)
```

Called when a tsunami is spawned.

```lua
function onTsunami(transform, magnitude)
```

Called when a whirlpool is spawned.

```lua
function onWhirlpool(transform, magnitude)
```

Called when a volcano is triggered.

```lua
function onVolcano(transform)
```

Called when an oil spill is updated, with the change (positive or negative) and the resulting total oil amount. Vehicle id is -1 for script command or oil tick updates.

```lua
function onOilSpill(tile_x, tile_y, delta, total, vehicle_id)
```

Called when oil is fully cleared via clearOilSpill or the creative menu button.

```lua
function onClearOilSpill()
```
