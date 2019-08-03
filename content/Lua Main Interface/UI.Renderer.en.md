---
title: "UI.Renderer"
date: 2019-04-13T18:16:44+02:00
draft: false
---

The renderer is typically used to display objects in the main 3D view.

{{% notice tip %}}
NOTE: Drawing functions can be called *only* during draw events.
{{% /notice %}}

See [Events.*](/lua-main-interface/events/) for how to register drawing callbacks.


#### UI.Renderer.GetWidth()
*Tacview 1.7.2*

Retrieve the renderer width in pixels or **nil** when not in a draw event.


#### UI.Renderer.GetHeight()
*Tacview 1.7.2*

Retrieve the renderer height in pixels or **nil** when not in a draw event.


#### UI.Renderer.LoadTexture( texturePath [, wrapRepeat [, compressed] ] )
*Tacview 1.7.3*
#### UI.Renderer.UnloadTexture( textureHandle )
*Tacview 1.7.3*

**wrapRepeat** = must be set to true if you want the texture to be repeated (default = true)

**compressed** = must be set to true if you want the texture to be compressed (recommended) (default = true)

Load png or jpg file and compile it as a texture.

Only 24-bit and 32-bit formats are supported.

32-bit format can be used to draw translucent textures.

Textures are directly used by **UI.Renderer.CreateRenderState**

Textures are indirectly used (in render states) by **UI.Renderer.DrawObjectVertexArray** and **UI.Renderer.DrawUIVertexArray**

Textures are automatically unloaded when the add-on is freed.

{{% notice note %}}
**Return value:**<br>
		The texture handle or **nil** if the file was not found or invalid.
{{% /notice %}}


#### UI.Renderer.CreateVertexArray( vertexArray )
*Tacview 1.7.2*
#### UI.Renderer.ReleaseVertexArray( vertexArrayHandle )
*Tacview 1.7.2*

Vertex arrays are a list of 3D points used to display triangle strips, which in turn represent 3D objects on screen.

Vertex arrays are automatically freed when the addon is unloaded.

Typically:

- You must call once (per 3D object) **UI.Renderer.CreateVertexArray()** to prepare your vertex array.
- Then, in your **Events.DrawOpaqueObjects()** callback, you can use the handle returned by **CreateVertexArray()** to draw your object using **UI.Renderer.DrawVertexArray()**.
- Whenever the vertex array is not required anymore, you can release the associated resource by calling **UI.Renderer.ReleaseVertexArray()**.

	vertexArray =
	{
		x, y, z,
		...
	}

{{% notice note %}}
**Return value:**<br>
		handle (interger) of the compiled array or **nil** if the array is invalid.
{{% /notice %}}


#### UI.Renderer.CreateTextureCoordinateArray( textureCoordinateArray )
*Tacview 1.7.3*
#### UI.Renderer.ReleaseTextureCoordinateArray( textureCoordinateArrayHandle )
*Tacview 1.7.3*

Texture coordinate arrays are a list of 2D coordinates used to texture triangle strips.

They are automatically freed when the addon is unloaded.

	textureCoordinateArray =
	{
		u, u,
		...
	}

{{% notice note %}}
**Return value:**<br>
		handle (interger) of the compiled array or **nil** if the array is invalid.
{{% /notice %}}


#### UI.Renderer.CreateRenderState( renderState )
*Tacview 1.7.2*
#### UI.Renderer.ReleaseRenderState( renderStateHandle )
*Tacview 1.7.2*

The draw state describes constants which will be used for one or many draw calls.

Typically used to specify a single color for a whole 3D model, as well as a list of textures used during draw operations.

You can use at any time **UI.Renderer.ReleaseRenderState()** to free the resource associated to a previously compiled draw state.

Draw states are automatically freed when the addon is unloaded.

	renderState =
	{
		-- OPTIONAL color (default to opaque white)
		-- Opaque red is: 0xff0000ff
		-- Opaque green is: 0xff00ff00
		-- Opaque blue is: 0xffff0000

		[color = 32_bit_rgba_color_code,]

		-- OPTIONAL texture loaded with UI.Renderer.LoadTexture()

		[texture = textureHandle,]

		-- OPTIONAL blend-mode (for transparent rendering phases)

		[
			blendMode =
					Tacview.UI.Renderer.BlendMode.Normal
					Tacview.UI.Renderer.BlendMode.Additive
		]
	}

{{% notice note %}}
**Return value:**<br>
		handle (integer) of the compiled state or **nil** if the array is invalid.
{{% /notice %}}


#### UI.Renderer.DrawObjectVertexArray( transform , renderStateHandle , vertexArrayHandle )
*Tacview 1.7.2*
#### UI.Renderer.DrawObjectVertexArray( transform , renderStateHandle , vertexArrayHandle [, textureCoordinateArrayHandle] )
*Tacview 1.7.3*

**renderStateHandle** is an integer previously returned by **UI.Renderer.CreateRanderState()**

**vertexArrayHandle** is an integer previously returned by **UI.Renderer.CreateVertexArray()**

**textureCoordinateArrayHandle** is an optional integer previously returned by **UI.Renderer.CreateTextureCoordinateArray()**

	transform =
	{
		-- If the cartesian xyz position in the Earth global space is not provided, it will be calculated based on the spherical position (longitude, latitude, altitude).

		x = number,
		y = number,
		z = number,

		-- If the spherical position is not provided, it will be calculated based on xyz cartesian position.

		longitude = radian,
		latitude = radian,
		altitude = meters,

		-- Optional rotation info

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Optional scale

		scale = number
	}

Draw the given 3D model (from a previous call to **UI.Renderer.CreateVertexArray**) using the given state (from a previous call to **UI.Renderer.CreateRenderState**) at the given position/rotation/scale in the 3D view.

State and vertex array must be created only ONCE.

DO NOT re-declare the state and/or the vertex array at each draw call, this will result in a resource leak.


#### UI.Renderer.DrawUIVertexArray( transform , renderStateHandle , vertexArrayHandle )
*Tacview 1.7.2*
#### UI.Renderer.DrawUIVertexArray( transform , renderStateHandle , vertexArrayHandle [, textureCoordinateArrayHandle] )
*Tacview 1.7.3*

**renderStateHandle** is an integer previously returned by **UI.Renderer.CreateRenderState()**

**vertexArrayHandle** is an integer previously returned by **UI.Renderer.CreateVertexArray()**

**textureCoordinateArrayHandle** is an optional integer previously returned by **UI.Renderer.CreateTextureCoordinateArray()**

	transform =
	{
		-- Mandatory screen coordinates

		x = number,
		y = number,
		z = number,				-- 0 by default

		-- Optional orientation

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Optional uniform scale

		scale = number

		-- Optional non-uniform scale
		-- Tacview 1.8.0

		scaleX = number
		scaleY = number
	}

During the UI pass, 2D coordinates are like the following:

	UI.Renderer.GetHeight()

	    ^
	    |transform.Y
	    |
	    |
	    |      transform.x
	    +------------------> UI.Renderer.GetWidth()
	   0,0

Draw the given 2D/3D model (from a previous call to **UI.Renderer.CreateVertexArray**) using the given state (from a previous call to **UI.Renderer.CreateRenderState()**) at the given position/rotation/scale on top of the 3D view.

State and vertex array must be created only ONCE.

DO NOT re-declare the state and/or the vertex array at each draw call, this will result in a resource leak.


#### UI.Renderer.DrawOpaqueObject( objectHandle , transform [, alpha ] )
*Tacview 1.7.2*
#### UI.Renderer.DrawTransparentObject( objectHandle , transform [, alpha ] )
*Tacview 1.7.2*

High level function to draw the opaque or transparent parts of the corresponding telemetry object in the 3D view.

These functions will automatically use the current object shape and color to properly display the 3D model in the 3D view.

**UI.Renderer.DrawOpaqueObject()** is typically called in **Events.DrawOpaqueObjects** callbacks to draw the main object body.

*UI.Renderer.DrawTransparentObject()** is typically called in **Events.DrawTransparentObjects** callbacks to draw the remaining transparent parts of objects (e.g. properlters).

	transform =
	{
		-- If the spherical position in not provided, Tacview will use cartesian xyz position in the Earth global space

		x = number,
		y = number,
		z = number,

		-- Spherical position will be used in priority to render the object

		longitude = radian,
		latitude = radian,
		altitude = meters,

		-- Optional rotation info

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Optional scale

		scale = number
	}

You can scale the object or set scale to -1 for automatic scale (depending on user settings)

You can force the transparency of the object or set alpha to -1 for automatic (depending on dead/alive status)


#### UI.Renderer.Print( transform , renderStateHandle , text )
*Tacview 1.7.3*

Print the given text at the corresponding x,y coordinates.

Should be used only during 2D transparent UI operations.

You can set **renderState.blendMode** to **Tacview.UI.Renderer.BlendMode.Additive** to display HUD style text.

	transform =
	{
		-- If the cartesian xyz position in the Earth global space is not provided, it will be calculated based on the spherical position (longitude, latitude, altitude).

		x = number,
		y = number,

		-- Optional scale

		scale = number
	}


#### UI.Renderer.ContextMenu.RegisterListener( function )
*Tacview 1.7.6*

Use this function to register a callback to add options to the context menu Tacview will display on right click in the 3D view.

Right before displaying the 3D view context menu Tacview will call the following function so you can have the opportunity to add custom option:

		function( contextMenuId , objectHandle )

		-- **contextMenuId** (integer): Id of the context menu in which you can add options.
		-- **objectHandle** (integer): object associated to the context menu (0 if no object is related to the menu)

Use **UI.Menus** functions with **parentMenuId** set to **contextMenuID** to add your own options to the context menu according to the selected object.

The context menu is volatile and will be automatically destroyed as soon as it will be closed by the user.

Every time your callback is called, your options will be added to a brand new menu.
