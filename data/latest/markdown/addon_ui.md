# Chat

Sends a chat message. peer_id is optional and defaults to -1 for all peers. Announce messages are not handled as commands.

```lua
server.announce(name, message, (peer_id))
```

Sends a command message directly to all other scripts. Uses peer id -1 when arriving in the onCustomCommand callback.

```lua
server.command(message)
```

Sends a pop up notification to the specified peer(s)

```lua
server.notify(peer_id, title, message, NOTIFICATION_TYPE)
```

```lua

	NOTIFICATION_TYPE |
	0 = new_mission,
	1 = new_mission_critical,
	2 = failed_mission,
	3 = failed_mission_critical,
	4 = complete_mission,
	5 = network_connect,
	6 = network_disconnect,
	7 = network_info,
	8 = chat_message,
	9 = rewards,
	10 = network_info_critical,
	11 = research_complete,

```

# Map & World

Returns a unique UI id number for use with all other UI functions, The UI ID can be used to track, edit and clean UI elements up.

```lua
ui_id = server.getMapID()
```

Removes all UI with the specified UI ID for the specified peer(s)

```lua
server.removeMapID(peer_id, ui_id)
```

Add a map marker for the specified peer(s). x, z represent the worldspace location of the marker, since the map is 2D a y coordinate is not required. If POSITION_TYPE is set to 1 or 2 (vehicle or object) then the marker will track the object/vehicle of object_id/vehicle_id and offset the position by parent_local_x, parent_local_z. Custom color defaults to red (0-255).

```lua
server.addMapObject(peer_id, ui_id, POSITION_TYPE, MARKER_TYPE, x, z, parent_local_x, parent_local_z, vehicle_id, object_id, label, radius, hover_label)
```

```lua
server.addMapObject(peer_id, ui_id, POSITION_TYPE, MARKER_TYPE, x, z, parent_local_x, parent_local_z, vehicle_id, object_id, label, radius, hover_label, r, g, b, a)
```

```lua

	POSITION_TYPE |
	0 = fixed,
	1 = vehicle,
	2 = object

	MARKER_TYPE |
	0 = delivery_target,
	1 = survivor,
	2 = object,
	3 = waypoint,
	4 = tutorial,
	5 = fire,
	6 = shark,
	7 = ice,
	8 = search_radius
	9 = flag_1
	10 = flag_2
	11 = house
	12 = car
	13 = plane
	14 = tank
	15 = heli
	16 = ship
	17 = boat
	18 = attack
	19 = defend

```

Removes a map object with the specified UI ID for the specified peer(s)

```lua
server.removeMapObject(peer_id, ui_id)
```

Add a map label for the specified peer(s). x, z represent the worldspace location of the marker. Map labels appear under fog of war. Custom color defaults to black (0-255).

```lua
server.addMapLabel(peer_id, ui_id, LABEL_TYPE, name, x, z)
```

```lua
server.addMapLabel(peer_id, ui_id, LABEL_TYPE, name, x, z, r, g, b, a)
```

```lua
	
	LABEL_TYPE |
	0 = none,
	1 = cross,
	2 = wreckage,
	3 = terminal,
	4 = military,
	5 = heritage,
	6 = rig,
	7 = industrial,
	8 = hospital,
	9 = science,
	10 = airport,
	11 = coastguard,
	12 = lighthouse,
	13 = fuel,
	14 = fuel_sell,
	15 = hospital_ship,
	16 = refuel_plane,
	17 = ore,
	18 = ingot,
	19 = fish,
	20 = dollar,

```

Removes a map label with the specified UI ID for the specified peer(s)

```lua
server.removeMapLabel(peer_id, ui_id)
```

Adds a map line between two world space matrices with the specified UI ID for the specified peer(s). Custom color defaults to red.

```lua
server.addMapLine(peer_id, ui_id, start_matrix, end_matrix, width)
```

```lua
server.addMapLine(peer_id, ui_id, start_matrix, end_matrix, width, r, g, b, a)
```

Removes a map line with the specified UI ID for the specified peer(s)

```lua
server.removeMapLine(peer_id, ui_id)
```

Creates a popup to the world/screen with the specified UI ID for the specified peer(s). If render distance is set to 0 then the popup will always render. Optionally Parent to a vehicle or Object, with x,y,z acting as a relative position.

```lua
server.setPopup(peer_id, ui_id, name, is_show, text, x, y, z, render_distance, [vehicle_parent_id], [object_parent_id])
```

Creates a popup to the screen with the specified UI ID for the specified peer(s). Screen space offset ranges from -1,-1 (Bot Left) to 1,1 (Top Right).

```lua
server.setPopupScreen(peer_id, ui_id, name, is_show, text, horizontal_offset, vertical_offset)
```

Removes a popup with the specified UI ID for the specified peer(s)

```lua
server.removePopup(peer_id, ui_id)
```
