# Time to get your hands on the brand-new Lua SDK !

1.7.2 release is a big step forward more customization: I have integrated **Lua 5.3.4** in Tacview and started to develop an easy to use API. Now, anyone with some programing skills can create addons to extend existing features and even add new features to Tacview!
How to create your own addon?

* Create a sub folder named after your addon in C:\ProgramData\Tacview\AddOns\
* Create a file named "main.lua" in this folder (it will be automatically loaded at Tacview startup). It will look like `C:\ProgramData\Tacview\AddOns\My Addon\main.lua`
* At the beginning of your script, reference the latest API like the following: `local Tacview = require("Tacview172")`
* Now you can use any of the features documented in `C:\Program Files (x86)\Tacview\AddOns\Tacview Lua * Interface.txt` to create your own addon!
* **LuaSocket 3.0** which has been integrated in Tacview and ready to fulfill all of your connectivity needs! Just reference it as usual: `socket = require("socket")`

Keep in mind that this is a first iteration. While the current API is still relatively limited, new features will be added over the coming releases. Just let me know whatever you need. I will do my best to add more Lua functions, so everyone can develop the addon of your dream.

Have a look at the samples are available in `C:\Program Files (x86)\Tacview\AddOns\`

The most notable example is the **Landing Signal Officer** (currently in development) which (will) displays an LSO view when you select an aircraft carrier as switch to cockpit view. This addon will soon automatically score landing attempts.

![Landing Signal Officer AddOn](https://www.tacview.net/rss/Tacview-Lua-SDK.png)
