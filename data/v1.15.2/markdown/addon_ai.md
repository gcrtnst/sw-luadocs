# AI

Lua AI can be run on any character, and their resulting actions are dictated by their state and the AI Type of the seat they are attached to.

Gun components and Camera components can be linked to a seat by naming them identically. 

Sets the AI state for a character object.

```lua
server.setAIState(object_id, AI_STATE)

	SEAT TYPE = Ship Pilot
		AI_STATE |
		0 = none,
		1 = path to destination,

	SEAT TYPE = Helicopter Pilot
		AI_STATE |
		0 = none,
		1 = path to destination,
		2 = path to destination accurate (smaller increments for landing/takeoff),
		3 = gun run (Fly at target and press the trigger hotkey when locked on),

	SEAT TYPE = Plane Pilot
		AI_STATE |
		0 = none,
		1 = path to destination,
		2 = gun run (Fly at target and press the trigger hotkey when locked on),

	SEAT TYPE = Gunner
		AI_STATE |
		0 = none,
		1 = fire at target (Accounts for bullet drop / effective range when pulling the trigger),

	SEAT TYPE = Designator
		AI_STATE |
		0 = none,
		1 = aim at target (Pulls the trigger when looking directly at target),

```

Seat Outputs:

```lua

	SEAT TYPE = Ship Pilot
		Hotkey 1 = Engine On
		Hotkey 2 = Engine Off
		Axis W = Throttle
		Axis D = Steering

	SEAT TYPE = Helicopter Pilot
		Hotkey 1 = Engine On 
		Hotkey 2 = Engine Off
		Axis W = Pitch
		Axis D = Roll
		Axis Up = Collective
		Axis Right = Yaw
		Trigger = Shoot

	SEAT TYPE = Plane Pilot
		Hotkey 1 = Engine On 
		Hotkey 2 = Engine Off
		Axis W = Pitch
		Axis D = Roll
		Axis Up = Throttle
		Axis Right = Yaw
		Trigger = Shoot

	SEAT TYPE = Gunner
		Axis W = Pitch
		Axis D = Yaw
		Trigger = Shoot

	SEAT TYPE = Designator
		Axis W = Pitch
		Axis D = Yaw
		Trigger = Designate

```

Sets the target destination for an AI.

```lua
server.setAITarget(object_id, matrix_destination)
```

Gets the target destination for an AI. Returns nil on failure.

```lua
TARGET_DATA = server.getAITarget(object_id)
```

```lua

	TARGET_DATA = {
		["character"] = target character object id,
		["vehicle"] = target vehicle id,
		["x"] = target_x,
		["y"] = target_y,
		["z"] = target_z,
	}

```

Sets the target character for an AI. Different AIs use this data for their unique tasks.

```lua
server.setAITargetCharacter(object_id, target_object_id)
```

Sets the target vehicle for an AI. Different AIs use this data for their unique tasks.

```lua
server.setAITargetVehicle(object_id, target_vehicle_id)
```

# AI Teams

Characters and vehicles can be assigned to teams. Characters with AI enabled can be set to target certain teams, which will allow a character with handheld weapons equipped to automatically shoot at the targeted teams.

A team is an index between 0(default) and 30.

Default Teams:

0 - Default

29 - Prey Creatures

28 - Predator Creatures

27 - Zombies

1 - Used by default scripts for player team

2 - Used by default scripts for enemy AI

Set team value for a character. 0 to 29.

```lua
server.setAICharacterTeam(character_id, team)
```

Set team value for a vehicle. 0 to 29.

```lua
server.setAIVehicleTeam(vehicle_id, team)
```

Set if a character should target a team. 0 to 29.

```lua
server.setAICharacterTargetTeam(character_id, team, is_target)
```
