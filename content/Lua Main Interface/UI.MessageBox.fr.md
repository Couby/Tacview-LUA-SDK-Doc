---
title: "UI.MessageBox"
date: 2019-04-13T18:16:44+02:00
draft: false
---


Les boîtes de message peuvent être utilisées pour afficher des notifications et poser des questions simple à l'utilisateur.
Il est recommandé de ne pas abuser de ce type d'interface au risque de casser le flux de productivité de l'utilisateur.
Lorsque c'est possible, vous pouvez utiliser le log pour afficher la plupart des messages et vous appuyer sur settings pour choisir des comportements appropriés dépendants des circonstances.


#### UI.MessageBox.GetSaveFileName( options )
*Tacview 1.8.0*

Demande à l'utilisateur sous quel nom de fichier il/elle souhaite sauvegarder un fichier.

options =
{
	defaultFileExtension = defaultFileExtension,	-- exclu le '.', par exemple "csv"
	fileName = defaultFileNameToSave,				-- (OPTIONNEL) chemin complet ou nom de fichier par défaut pour le fichier à sauvegarder

	fileTypeList =									-- Liste des types acceptés pour la sauvegarde (habituellement un item du type usuel)
	{
		{ extensions, description }					-- Type(s) de fichier(s) et description {"*.jpg;*.png", "Picture"}
	}
}

{{% notice note %}}
**Valeur retournée :**<br>
    chemin complet du nom de fichier à sauvegarder<br>
    *nil* si l'utilisateur a annulé l'opération
{{% /notice %}}

{{% notice tip %}}
Exemple:<br>
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

Invite l'utilisateur à sélectionner un répertoire et retrouve le chemin complet du répertoire sélectionné.

options =
{
	folderName = defaultFolderNameToSelect,			-- (OPTIONNEL) chemin complet du répertoire à sélectionner par défaut
	canCreateNewFolder = boolean,					-- (OPTIONNEL) régler sur *true* pour permettre à l'utilisateur de créer de nouveaux répertoires
}

{{% notice note %}}
**Valeur retournée :**<br>
  chemin complet du nom de répertoire<br>
  *nil* si l'utilisateur a annulé l'opération
{{% /notice %}}

{{% notice tip %}}
Exemple:<br>
<br>
	local options =<br>
	{<br>
		folderName = "C:/Downloads/",<br>
		canCreateNewFolder = true,<br>
	}
{{% /notice %}}
