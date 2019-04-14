---
title: "Add Ons"
date: 2019-04-13T18:16:52+02:00
draft: false
---


The add-ons interface is mainly used to specify information about your add-on.

Your addon settings will be saved and restored at the next session of Tacview.


#### AddOns.Current.GetPath()
*Tacview 1.7.4*

Retrieve the current addon root path.

This is typically where your addon dll or lua file is stored.

This function is useful to access and load your custom resources without hardcoding a path to them.

{{% notice note %}}
**Return value:**<br>
		AddOn **path** (e.g. `C:\ProgramData\Tacview\AddOns\Tutorial 1 - Hello World - CS\`)<br>
		or **nil** if not applicable (typically for lua code injected over a pipe)
{{% /notice %}}


#### AddOns.Current.SetTitle( addOnTitle )
*Tacview 1.7.2*

Defines a user friendly-name in place of the folder name which is displayed by default in Tacview UI.


#### AddOns.Current.SetVersion( textVersionNumber )
*Tacview 1.7.2*

It is recommended to declare the version of your add-on using this function.

That way, it will be easier for the end-user to know if it's time to download an updated version of it.


#### AddOns.Current.SetAuthor( authorName )
*Tacview 1.7.2*

Let everyone know who is the author of this brilliant add-on!


#### AddOns.Current.SetNotes( textNotes )
*Tacview 1.7.2*

Defines a text which will be displayed in Tacview status bar when your addon is selected in the addons menu.

A dedicated window will be available in Tacview 2.


#### AddOns.Current.Settings.SetBoolean( settingName , newBooleanValue )
*Tacview 1.7.2*

Save a Boolean setting under the given name.


#### AddOns.Current.Settings.GetBoolean( settingName , defaultBooleanValue )
*Tacview 1.7.2*

Returns the current setting value, or the default provided one if no value was previously saved.

{{% notice note %}}
**Return value:**
corresponding setting boolean value.
{{% /notice %}}
