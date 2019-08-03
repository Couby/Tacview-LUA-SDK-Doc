+++
title = "LUA Core Interface"
date = 2019-04-13T18:16:05+02:00
weight = 5
chapter = true
pre = "<b>1. </b>"
+++

---

#	Tacview 1.8.0 Lua Core Interface
##	Last update: 2019-06-10

---

Tacview will automatically load any Lua script named "main.lua" found in the immediate sub-folders of:

	C:\Program Files (x86)\Tacview\AddOns\
	%ProgramData%\Tacview\AddOns\
	%APPDATA%\Tacview\AddOns\

For example you could store your addon main script as:

	%ProgramData%\Tacview\AddOns\My add-on\main.lua

At the beginning of your script you will typically retrieve the available Lua interface for which your add-on has been programmed:

	Tacview = require("Tacview180")			-- Request Tacview 1.8.0 API

Then you can access any of the following methods like the following:

	Tacview.Log.Info("Successfully exported ", objectCount, " object(s)")

Depending on the context your script is executed in, you will have access to slightly different interfaces.
Your **main.lua** script will be executed in the main context. It will be granted access to all Tacview features but export and import interfaces.
While your import and export scripts will be granted access to the core features as well as respectively import or export interfaces.
To prevent multithreading issues as well as errors breaking other add-ons, each Lua add-on is loaded in its own virtual machine.
