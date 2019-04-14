---
title: "Log"
date: 2019-04-13T18:16:51+02:00
draft: false
---


The log module is typically used to log messages and errors which can be used to diagnose specific issues.

All strings sent to the log will also be saved in the `%TEMP%\Tacview.log` file.

Please, use the log wisely and try to display only meaningful messages to the end-user.

Do not spam the log with internal development messages, this may confuse the user who is looking for more relevant status from other modules.


#### Log.Debug(...)
*Tacview 1.7.2*

Use this method to help you trace and diagnose problems with your addon.

{{% notice tip %}}
**NOTE:** Debug information will be displayed only when using the `/Debug:On` command line argument.
{{% /notice %}}


#### Log.Info(...)
*Tacview 1.7.2*

This method can be used to display specific information related to your addon which might be useful to the end-user.

{{% notice tip %}}
**NOTE:** Lua *print()* function is redirected to *Log.Info()*.
{{% /notice %}}


#### Log.Warning(...)
*Tacview 1.7.2*

Warnings can be used to notify the user of unusual circumstances like non-critical errors in input data.
Warnings will be highlighted in Tacview console to attract the user attention.


#### Log.Error(...)
*Tacview 1.7.2*

Error messages are typically used to display critical errors which usually prevent further operation.
