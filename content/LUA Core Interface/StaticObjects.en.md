---
title: "StaticObjects"
date: 2019-04-13T18:16:52+02:00
draft: false
---


#### StaticObjects.GetHandleByName( objectName )
*Tacview 1.8.0*

Retrieve static object handle from its name.
The name of the object can be defined via the <name> xml tag in kml files.

Names are case sensitive and may not be unique.
This function will return the first matching object.
Beware that object handles are volatile and may not be preserved the next time your addon is being called by Tacview.

{{% notice note %}}
**Return value:**<br>
handle of the static object
or nil of no object correspond to the given name
{{% /notice %}}	Return value:


#### StaticObjects.SetVisible( staticObjectHandle , isVisible )
*Tacview 1.8.0*

Show or hide given object.
You can use StaticObjects.GetHandleByName() to retrieve the handle of the object you would like to show/hide.
