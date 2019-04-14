---
title: "Context"
date: 2019-04-13T18:16:42+02:00
draft: false
---

Ce module contient toutes les informations relatives à la représentation de télémétrie à l'écran.

{{% notice tip %}}
**NOTE :** Voir [Lua Core Interface](/lua-core-interface/) pour des fonctions supplémentaires.
{{% /notice %}}


#### Context.GetSelectedObject( objectIndex )
*Tacview 1.7.2*

Récupère le handle de l'un des objets sélectionnés.

**objectIndex** peut être 0 pour l'objet primaire ou 1 pour l'objet secondaire.

Il est actuellement possible de sélectionner deux objets en même temps.


#### Context.SetSelectedObject( objectIndex , objectHandle )
*Tacview 1.7.2*

Choisissez quel objet est actuellement sélectionné.

**objectIndex** peut être 0 pour l'objet primaire ou 1 pour l'objet secondaire.

L'utilisateur sélectionne généralement un ou plusieurs objets pour modifier le point de vue de la caméra ou pour définir un contexte spécifique pour certains outils.

Pour obtenir un descripteur - handle - d'objet à partir de son identifiant de télémétrie, utilisez la fonction **Telemetry.GetObjectHandle(id)**.


#### Context.GetActiveObjectList()
*Tacview 1.7.3*

Récupérez les descripteurs - handles - de tous les objets actuellement actifs (vivants) à l'heure de lecture actuelle.

La table renvoyée contient les descripteurs sans ordre spécifique.

Retourne une table vide si aucun objet n'est actuellement actif.

{{% notice note %}}
**Valeur retournée :**<br>
	{ objectHandle1 , objectHandle2 , ... }
{{% /notice %}}
