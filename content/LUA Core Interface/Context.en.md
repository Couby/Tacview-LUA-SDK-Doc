---
title: "Context"
date: 2019-04-13T18:16:48+02:00
draft: false
---

This contains all the information relative the telemetry representation on screen.
{{% notice tip %}}
NOTE: See [Lua Main Interface](/lua-main-interface/) for additional functions.
{{% /notice %}}

#### Context.GetAbsoluteTime()
*Tacview 1.7.5*

Retrieves the current telemetry time in seconds **since 1970-01-01** (this parameter is useful to talk with the Telemetry module).


#### Context.SetAbsoluteTime( absoluteTime )
*Tacview 1.7.6*

Set current telemetry time for data playback in seconds **since 1970-01-01**.

{{% notice tip %}}
**NOTE:** DO NOT force the time at every frame, especially during real-time telemetry recording.<br>
This would conflict with Tacview internal time update leading to 3D view stutter.
{{% /notice %}}

If you want to synchronize Tacview time with an external tool, you should do so only when there is a important delta-time between both tools:

	-- Resynchronize Tacview time only if there is more than one second difference with the external tool

	if math.abs(Context.GetAbsoluteTime() - externalToolTime) > 1.0 then
		Context.SetAbsoluteTime(externalToolTime)
	end
