---
title: "Context.Camera"
date: 2019-04-13T18:16:41+02:00
draft: false
---

The camera is used to define the user point-of-view in the 3D window of Tacview.


#### Context.Camera.GetMode()
*Tacview 1.7.2*

Returns the current camera mode.

{{% notice note %}}
**Return value:**<br>
		Camera.Cockpit<br>
		Camera.External<br>
		Camera.Satellite<br>
		Camera.Free
{{% /notice %}}


#### Context.Camera.SetOffset( offsetData )
*Tacview 1.7.2*

Temporarily offset camera position and rotation.

The offset is automatically reset at each new frame when not overridden by an addon.

The following components can be specified, all of them are optional:

	offsetData =
	{
		lateral = meters_positive_to_the_right ,
		longitudinal = meters_positive_forward ,
		vertical = meters_positive_up ,
		roll = radian ,
		pitch = radian ,
		yaw = radian ,
	}


#### Context.Camera.SetFieldOfView( radian )
*Tacview 1.7.2*

Change the camera vertical field-of-view for one frame.

The field-of-view is automatically reset at each new frame when not overridden by an addon.

The default field-of-view is 60 degrees.

{{% notice tip %}}
**NOTE:** The field-of-view must be defined in radian.
{{% /notice %}}
