---
title: "UI"
date: 2019-04-13T18:16:46+02:00
draft: false
---

General functions to manipulate Tacview UI and aspect.

#### UI.EnterFullScreen()
*Tacview 1.7.2*
#### UI.ExitFullScreen()
*Tacview 1.7.2*

Enter/exit full screen mode.

When switched to full screen, Tacview displays only the 3D view in a borderless window.

This can be useful during an online debriefing, so the user can fully focus his attention on the objects displayed in the 3D view.

The user can manually switch between full screen and windowed mode by pressing [ALT] + [ENTER].

It is also possible to exit the full screen mode by pressing [Esc].


#### UI.EnterReadMode( [borderless] )
*Tacview 1.7.2*
#### UI.ExitReadMode()
*Tacview 1.7.2*

Enter/exit read-mode.

In read-mode Tacview displays only the 3D view (tools and menus are hidden).

**borderless** is an optional boolean parameter which can be set to true if you also want to hide Tacview window border.

This function is mainly to integrate Tacview window in another application when combined with **UI.SetWindowParent()**.


#### UI.SetWindowParent( parentWindowhandle )
*Tacview 1.7.2*

Attach Tacview main window to another application window.

Typically used with **UI.EnterReadMode(true)** and **UI.SetWindowPosition()** to display Tacview inside another application.

Call **SetWindowParent(nil)** to detach Tacview main window from your application.


#### UI.SetWindowPosition( x , y [, width , height] )
*Tacview 1.7.2*

Change Tacview main window position and size when **width** and **heigh** are provided.

Position is specified for the top/left corner of the window on the desktop, or in its parent window.


#### UI.SetWindowSize( width , height )
*Tacview 1.7.2*

Change Tacview main window size.

**width** and **height** must be > 0.


#### UI.GetWindowHandle()
*Tacview 1.7.5*

Returns Tacview main window handle.

You can use this function to create child windows or dialog boxes for your add-on.

DO NOT use this function to manually change Tacview window size, position or parent, in that case, use the dedicated functions which are doing more than just calling the OS.

{{% notice note %}}
**Return value:**<br>
		Tacview main window handle.<br>
		This handle may be **nil** if Tacview is executed in silent mode with the command line.
{{% /notice %}}
