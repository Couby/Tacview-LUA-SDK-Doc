---
title: "UI.MessageBox"
date: 2019-04-13T18:16:44+02:00
draft: false
---


Message boxes can be used to display modal notifications and ask for simple questions to the user.
It is suggested to not use too many message boxes as they are breaking the productivity flow of the user.
Whenever possible, you can use the log to output most of you messages and rely on settings to choose the appropriate behavior depending on the circumstances.


#### UI.MessageBox.GetSaveFileName( options )
*Tacview 1.8.0*

Asks the user which under which file name he/she wants to save a file.

options =
{
	defaultFileExtension = defaultFileExtension,	-- excluding '.', for example "csv"
	fileName = defaultFileNameToSave,				-- (OPTIONAL) default full path or file name for the file to save

	fileTypeList =									-- List of file types supported for save (usually one item of the typical type)
	{
		{ extensions, description }					-- File type(s) and description {"*.jpg;*.png", "Picture"}
	}
}

{{% notice note %}}
**Return value:**<br>
    full path of the file name to save<br>
    *nil* if the user has canceled the operation
{{% /notice %}}

{{% notice tip %}}
Example:<br>
<br>
	local options =<br>
	{<br>
		defaultFileExtension = "csv",<br>
		fileTypeList =<br>
		{<br>
			{ "*.csv" , "Comma-separated values"  }<br>
			{ "*.xml" , "Extensible Markup Language" }<br>
			{ "*.json;*.js" , "JavaScript Object Notation" }<br>
		}<br>
	}<br>
{{% /notice %}}

#### UI.MessageBox.GetFolderName( options )
*Tacview 1.8.0*

Prompts the user to select a folder and retrieve selected folder full path.

options =
{
	folderName = defaultFolderNameToSelect,			-- (OPTIONAL) full path of the folder to select by default
	canCreateNewFolder = boolean,					-- (OPTIONAL) set to *true* to enable the user to create new folders
}

{{% notice note %}}
**Return value:**<br>
  full path of the folder name<br>
  *nil* if the user has canceled the operation
{{% /notice %}}

{{% notice tip %}}
Example:<br>
<br>
	local options =<br>
	{<br>
		folderName = "C:/Downloads/",<br>
		canCreateNewFolder = true,<br>
	}
{{% /notice %}}
