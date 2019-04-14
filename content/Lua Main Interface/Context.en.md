---
title: "Context"
date: 2019-04-13T18:16:42+02:00
draft: false
---

This contains all the information relative the telemetry representation on screen.

{{% notice tip %}}
**NOTE:** See [Lua Core Interface](/lua-core-interface/) for additional functions.
{{% /notice %}}


#### Context.GetSelectedObject( objectIndex )
*Tacview 1.7.2*

Retrieves the handle of one of the selected objects.

**objectIndex** can be either 0 for the primary object or 1 for the secondary object.

It is currently possible to select two objects at the same time.


#### Context.SetSelectedObject( objectIndex , objectHandle )
*Tacview 1.7.2*

Choose which object is currently selected.

**objectIndex** can be either 0 for the primary object or 1 for the secondary object.

The user usually select object(s) to change the camera point-of-view or to define a specific context for some tools.

To get an object handle from its telemetry id, use the function **Telemetry.GetObjectHandle(id)**


#### Context.GetActiveObjectList()
*Tacview 1.7.3*

Retrieve the handles of all currently active (alive) objects at the current playback time.

The returned table contains the handles in no specific order.

Returns an empty table if no objects are currently active.

{{% notice note %}}
**Return value:**<br>
	{ objectHandle1 , objectHandle2 , ... }
{{% /notice %}}
