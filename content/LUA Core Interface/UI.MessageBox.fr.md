---
title: "UI.MessageBox"
date: 2019-04-13T18:16:50+02:00
draft: false
---


Les boîtes de dialogue peuvent afficher des notifications modales et permettre de poser des questions simples à l'utilisateur.

Il est recommandé de ne pas utiliser des boîtes de dialogue de manière excessive parce qu'elles cassent le flow de productivité de l'utilisateur.

Lorsque c'est possible, vous pouvez utiliser le log pour afficher la plupart de vos messages et vous appuyer sur les paramètres pour choisir le comportement approprié selon les circonstances.


#### UI.MessageBox.Info( textMessage )
*Tacview 1.7.2*


#### UI.MessageBox.Error( textMessage )
*Tacview 1.7.2*

Affiche une notficiation modale pour informer ou avertir l'utilisateur.


#### UI.MessageBox.Question( textMessage )
*Tacview 1.7.2*

Affiche une question.

{{% notice note %}}
**Valeur retournée :**<br>
	Une des constantes suivantes :<br>
		- **UI.MessageBox.OK**<br>
		- **UI.MessageBox.Cancel**<br>
{{% /notice %}}
