# LUA SCRIPTING OVERVIEW

Lua scripting gives you the tools to create advanced logic components using the Lua scripting language. Stormworks provides a number of functions to allow your script to interface with your vehicle's logic system, as well as drawing to in-game monitors.

This guide outlines the functions that are available for use in your scripts but it is not a comprehensive tutorial on using the Lua language.

# SCRIPT BASICS

The tick function will be called once every logic tick and should be used for reading composite data and any required processing. Screen functions will have no effect if called within onTick.

```lua
function onTick()
	-- Example that adds two composite channels together and outputs the result
	in1 = input.getNumber(1)
	in2 = input.getNumber(2)
	output.setNumber(1, in1 + in2)
end
```

The draw function will be called any time this script is drawn by a monitor. Note that it can be called multiple times if this microcontroller is connected to multiple monitors whereas onTick is only called once. Composite input/output functions will have no effect if called within onDraw.

```lua
function onDraw()
	-- Example that draws a red circle in the center of the screen with a radius of 20 pixels
	width = screen.getWidth()
	height = screen.getHeight()
	screen.setColor(255, 0, 0)
	screen.drawCircleF(width / 2, height / 2, 20)
end
```

# COMPOSITE INPUT/OUTPUT

Read values from the composite input. Index ranges from 1 - 32.

```lua
input.getBool(index)
input.getNumber(index)
```

Set values on the composite output. Index ranges from 1 - 32.

```lua
output.setBool(index, value)
output.setNumber(index, value)
```

# PROPERTIES

Read the values of property components within this microcontroller directly. The label passed to each function should match the label that has been set for the property you're trying to access (case-sensitive).

```lua
property.getNumber(label)
property.getBool(label)
property.getText(label)
```

# DRAWING

Set the current draw color. Values range from 0 - 255.

```lua
screen.setColor(r, g, b)
```

Set the current draw color and transparency. Values range from 0 - 255.

```lua
screen.setColor(r, g, b, a)
```

Clear the screen with the current colour.

```lua
screen.drawClear()
```

Draw line from (x1, y1) to (x2, y2).

```lua
screen.drawLine(x1, y1, x2, y2)
```

Draw circle at (x, y) with radius.

```lua
screen.drawCircle(x, y, radius)
```

Draw filled circle at (x, y) with radius.

```lua
screen.drawCircleF(x, y, radius)
```

Draw rectangle at (x, y) with width and height.

```lua
screen.drawRect(x, y, width, height)
```

Draw filled rectangle at (x, y) with width and height.

```lua
screen.drawRectF(x, y, width, height)
```

Draw triangle between (x1, y1), (x2, y2) and (x3, y3).

```lua
screen.drawTriangle(x1, y1, x2, y2, x3, y3)
```

Draw filled triangle between (x1, y1), (x2, y2) and (x3, y3).

```lua
screen.drawTriangleF(x1, y1, x2, y2, x3, y3)
```

Draw text at (x, y). Each character is 4 pixels wide and 5 pixels tall.

```lua
screen.drawText(x, y, text)
```

Draw text within the rectangle at (x, y) with width and height. Text alignment can be specified using the last two parameters and ranges from -1 to 1 (left to right, top to bottom). If either of the alignment parameters are omitted, the text will be drawn top-left by default. Text will automatically wrap at spaces when possible, and will overflow the top/bottom of the specified rectangle if too large.

```lua
screen.drawTextBox(x, y, w, h, text, h_align, v_align)
```

Draw the world map centred on map coordinate (x,y) with zoom level ranging from 0.1 to 50.

```lua
screen.drawMap(x, y, zoom)
```

Set the colors used for rendering the map. Values range from 0 - 255, alpha is optional.

```lua
screen.setMapColorOcean(r, g, b, a)
screen.setMapColorShallows(r, g, b, a)
screen.setMapColorLand(r, g, b, a)
screen.setMapColorGrass(r, g, b, a)
screen.setMapColorSand(r, g, b, a)
screen.setMapColorSnow(r, g, b, a)
screen.setMapColorRock(r, g, b, a)
screen.setMapColorGravel(r, g, b, a)
```

Get the width/height of the screen currently being rendered to.

```lua
screen.getWidth()
screen.getHeight()
```

# MAP

Convert pixel coordinates into world coordinates.

```lua
worldX, worldY = map.screenToMap(mapX, mapY, zoom, screenW, screenH, pixelX, pixelY)
```

Convert world coordinates into pixel coordinates.

```lua
pixelX, pixelY = map.mapToScreen(mapX, mapY, zoom, screenW, screenH, worldX, worldY)
```

# TOUCHSCREEN DATA

The composite output from the monitors contains data that can be interpreted in your script to create touchscreens. The layout of the composite data is as follows:

Number Channels
1: monitorResolutionX
2: monitorResolutionY
3: input1X
4: input1Y
5: input2X
6: input2Y

On/Off Channels:
1: isInput1Pressed
2: isInput2Pressed

This is an example of a script that outputs a signal on composite channel 1 if the player is pressing the screen within a specific rectangle:

```lua
function onTick()
	-- Read the touchscreen data from the script's composite input
	inputX = input.getNumber(3)
	inputY = input.getNumber(4)
	isPressed = input.getBool(1)

	-- Check if the player is pressing the rectangle at (10, 10) with width and height of 20px
	isPressingRectangle = isPressed and isPointInRectangle(inputX, inputY, 10, 10, 20, 20)

	-- Set the composite output, on/off channel 1
	output.setBool(1, isPressingRectangle)
end

-- Returns true if the point (x, y) is inside the rectangle at (rectX, rectY) with width rectW and height rectH
function isPointInRectangle(x, y, rectX, rectY, rectW, rectH)
	return x > rectX and y > rectY and x < rectX+rectW and y < rectY+rectH
end

function onDraw()
	-- Draw a rectangle that fills in when the player is pressing it
	if isPressingRectangle then
		screen.drawRectF(10, 10, 20, 20)
	else
		screen.drawRect(10, 10, 20, 20)
	end
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

# TELEMETRY FUNCTIONS

The following global async functions are available:

- httpGet

HTTP requests are sent to the localhost on the specified port. Responses are caught with the httpReply(port, request_body, response_body) callback function.

async.httpGet(port, request_body)

Example of a HTTP request sent to port 80:

```lua

-- a function to send a simple http request to port 80 with some body parameters (body must start with a /)
async.httpGet(80, "/set_light_mode?index=1&mode=3")


-- This callback function automatically triggers when a reply is recieved for a http request
function httpReply(port, request_body, response_body)
	
end
```

# META FROM THE DEVS

This scripting API is very powerful and as such there are some important reminders to take note of:

- Your script has a max execution time of 1000 milliseconds, however it is still possible to create scripts that significantly slow down the game. It is your responsibility to ensure your script runs efficiently.

- Random number functions are provided by the Lua math library. Use of randomness in your scripts is likely to cause desync in multiplayer, so use these functions at your own risk.

- When your vehicle despawns and respawns, your script will be executed 'fresh' and any state stored within the script will be lost. We recommend keeping your script as stateless as possible, and making use of existing logic components (e.g. memory register) to store values that you wish to persist.

- Your scripts run as a 'black box' with only the logic inputs/outputs being synced in multiplayer. Keep in mind that complex logic in your script may behave differently for different players in a multiplayer session.

- A number of safeguards are in place to sandbox your script, however it is still possible to write scripts that will potentially crash your game. If you crash your game with a script, it's likely that you're doing something (very) wrong. This is your own responsibility. If you suspect you have encountered a legitimate bug, please report it on the Stormworks issue tracker (accessible from the pause-menu).

- Malicious and harmful scripts will not be tolerated on the Stormworks Steam Workshop.

Finally, enjoy the almost limitless possibilities that these scripts provide. This short wiki aims to give a good overview of how scripting in Stormworks works, however if you have any questions that are not covered here, please feel free to join us on Discord (accessible from the pause-menu)!
