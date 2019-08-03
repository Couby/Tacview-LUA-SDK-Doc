---
title: "UI.Menus"
date: 2019-04-13T18:16:45+02:00
draft: false
---

The Menu interface is useful to create and insert commands and options in Tacview menus.

All new menus will be added to the addons menu.

Tacview will automatically remove menu items of an addon which is unloaded.


#### UI.Menus.AddMenu( parentMenuId , textLabel )
*Tacview 1.7.2*

Creates and inserts a menu in Tacview menu.

You can specify the id of a parent menu, or you can use **nil** to insert your menu in Tacview addons main menu.

{{% notice note %}}
**Return value:**<br>
		a menu id (integer) which can be used late to insert sub items or to remove the menu.
{{% /notice %}}


#### UI.Menus.AddSeparator( parentMenuId )
*Tacview 1.8.0*

Add a separator in the specified menu.
Use separators to group options and commands to make your menus more intuitive for your users.


#### UI.Menus.AddCommand( parentMenuId , textLabel , function )
*Tacview 1.7.2*

Insert a command in the given menu.

You can specify the id of a parent menu, or you can use **nil** to insert your menu in Tacview addons main menu.

**function** will be called whenever this very menu command has been clicked.

{{% notice note %}}
**Return value:**<br>
		a menu id (integer) which can be used late to insert sub items or to remove the menu.
{{% /notice %}}


#### UI.Menus.AddOption( parentMenuId , textLabel , optionBoolean , function )
*Tacview 1.7.2*

Insert a command with a tick mark in the given menu.

If **optionBoolean** is true, then a tick mark will be displayed after the command label.

You can specify the id of a parent menu, or you can use **nil** to insert your menu in Tacview addons main menu.

**function** will be called whenever this menu option has been clicked.

{{% notice note %}}
**Return value:**<br>
		Menu id which can later be used to change the option value using **UI.Menus.SetOption()**.
{{% /notice %}}


#### UI.Menus.SetOption( menuId , optionBoolean )
*Tacview 1.7.2*

Change the value of a menu option.
If **optionBoolean** is true, then a tick mark will be displayed next to the corresponding command label.
