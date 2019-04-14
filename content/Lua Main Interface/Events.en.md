---
title: "Events"
date: 2019-04-13T18:16:43+02:00
draft: false
---

You can register callbacks for different kind of events in Tacview.


#### Events.Update.RegisterListener( function )
*Tacview 1.7.2*

Once a frame, Tacview will call your function which must match the following signature:

Update( dt , absoluteTime )

- **dt** is the number of seconds elapsed in real life since the last **Update()**
- **absoluteTime** is the current telemetry time in seconds **since 1970-01-01** (this parameter is useful to talk with the Telemetry module)


#### Events.DrawOpaqueObjects.RegisterListener( function )
*Tacview 1.7.2*
#### Events.DrawTransparentObjects.RegisterListener( function )
*Tacview 1.7.2*

Once a frame, Tacview will call your function to draw 3D objects in the 3D view.

There is one pass for the opaque 3D models and one pass for the transparent models.

See **[UI.Renderer.DrawObjectVertexArray()](/lua-main-interface/ui.renderer/#ui-renderer-drawobjectvertexarray-transform-renderstatehandle-vertexarrayhandle-texturecoordinatearrayhandle)** and **[UI.Renderer.DrawOpaqueObject()](/lua-main-interface/ui.renderer/#ui-renderer-drawtransparentobject-objecthandle-transform-alpha)** to draw objects in the 3D world.


#### Events.DrawOpaqueUI.RegisterListener( function )
*Tacview 1.7.2*
#### Events.DrawTransparentUI.RegisterListener( function )
*Tacview 1.7.2*

Once a frame, Tacview will call your function to draw 2D transparent foreground UI on top of the 3D view.

You function will not receive any parameter.

See **[UI.Renderer.DrawUIVertexArray()](/lua-main-interface/ui.renderer/#ui-renderer-drawuivertexarray-transform-renderstatehandle-vertexarrayhandle-texturecoordinatearrayhandle)** to draw your UI on top of the 3D view.
