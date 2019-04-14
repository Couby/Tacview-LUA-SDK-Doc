---
title: "Settings"
date: 2019-04-13T18:16:53+02:00
draft: false
---

This interface is provided to access Tacview configuration.
If you want to save and load settings for your own addon, see [AddOns.Current.Settings](/lua-core-interface/addons/#addons-current-settings-setboolean-settingname-newbooleanvalue-tacview-1-7-2)


#### Settings.SetBoolean( settingPath, newBooleanValue )
*Tacview 1.7.2*

Save a Boolean setting under the given name.

**settingPath** can be one of the following:

*	`"UI.View.Grid.Visible"`			-- Enable/disable latitude/longitude grid
*	`"UI.View.HUD.Visible"`			-- Enable/disable cockpit head-up-display
*	`"UI.View.Overlay.Visible"`		-- Enable/disable all the informations displayed on top of the 3D view


#### Settings.GetBoolean( settingFullPath )
*Tacview 1.7.2*

Returns the current setting value or nil if the provided path does not point to a boolean setting.
See [Settings.SetBoolean](/lua-core-interface/settings/#settings-setboolean-settingpath-newbooleanvalue) for the possible values of **settingFullPath**.

{{% notice note %}}
**Return value:**
corresponding setting boolean value.
{{% /notice %}}


#### Settings.SetString( settingFullPath , newStringValue )
*Tacview 1.7.2*

Save a string setting under the given name.

**settingFullPath** and **newStringValue** can be one of the following:

*	`"UI.View.Terrain.Mode"` -- Change the way the terrain is displayed in the 3D view
*	`"Empty"`
*	`"Flat"`
*	`"3D"`
*	`"Full3D"`


#### Settings.GetString( settingFullPath )
*Tacview 1.7.2*

Returns the current setting value or nil if the provided path does not point to a string setting.
See [Settings.SetString](/lua-core-interface/settings/#settings-setstring-settingfullpath-newstringvalue) for the possible values of **settingFullPath**.

{{% notice note %}}
**Return value:**
corresponding setting string value.
{{% /notice %}}
