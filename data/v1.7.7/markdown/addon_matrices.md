# Matrix Manipulation

Stormworks provides a limited set of matrix functions that are useful for transforming positions of objects in scripts:


Multiply two matrices together.

```lua
out_matrix = matrix.multiply(matrix1, matrix2)
```

Invert a matrix.

```lua
out_matrix = matrix.invert(matrix1)
```

Transpose a matrix.

```lua
out_matrix = matrix.transpose(matrix1)
```

Return an identity matrix.

```lua
out_matrix = matrix.identity()
```

Return a rotation matrix rotated in the X axis.

```lua
out_matrix = matrix.rotationX(radians)
```

Return a rotation matrix rotated in the Y axis.

```lua
out_matrix = matrix.rotationY(radians)
```

Return a rotation matrix rotated in the Z axis.

```lua
out_matrix = matrix.rotationZ(radians)
```

Return a translation matrix translated by x,y,z.

```lua
out_matrix = matrix.translation(x,y,z)
```

Get the x,y,z position from a matrix.

```lua
x,y,z = matrix.position(matrix1)
```

Find the distance between two matrices.

```lua
dist = matrix.distance(matrix1, matrix2)
```

Multiplies a matrix by a vec 4.

```lua
out_x, out_y, out_z, out_w = matrix.multiplyXYZW(matrix1, x, y, z, w)
```

Returns the rotation required to face an X Z vector

```lua
out_rotation = matrix.rotationToFaceXZ(x, z)
```

# Example

Most API functions take a matrix as a parameter so users that do not wish to use matrices directly can convert between matrices and coordinates as follows:

```lua

-- Teleport peer_1 10m up
peer_1_pos, is_success = server.getPlayerPos(1)
if is_success then
	local x, y, z = matrix.position(peer_1_pos)
	y = y + 10
	server.setPlayerPos(1, matrix.translation(x,y,z))
end

```
