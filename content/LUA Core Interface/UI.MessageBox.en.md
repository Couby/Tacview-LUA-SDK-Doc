---
title: "UI.MessageBox"
date: 2019-04-13T18:16:50+02:00
draft: false
---


Message boxes can be used to display modal notifications and ask for simple questions to the user.

It is suggested to not use too many message boxes as they are breaking the productivity flow of the user.

Whenever possible, you can use the log to output most of you messages and rely on settings to choose the appropriate behavior depending on the circumstances.

#### UI.MessageBox.Info( textMessage )
*Tacview 1.7.2*


#### UI.MessageBox.Error( textMessage )
*Tacview 1.7.2*

Displays a modal notification to inform or warn the user.


#### UI.MessageBox.Question( textMessage )
*Tacview 1.7.2*

Displays a question.

{{% notice note %}}
**Return value:**<br>
	One of the following constants:<br>
		- **UI.MessageBox.OK**<br>
		- **UI.MessageBox.Cancel**<br>
{{% /notice %}}
