---
title: "StaticObjects"
date: 2019-04-13T18:16:52+02:00
draft: false
---


#### StaticObjects.GetHandleByName( objectName )
*Tacview 1.8.0*

Retrvoue le handle de l'objet statique à partir de son nom.
Le nom de l'objet peut être défini via le tag xml <name> dans les fichiers kml.

Names est sensible à la casse et peut ne pas être unique.
Cette fonction retourne le projet objet trouvé correspondant.
Ne pas oublier que les handles sont volatiles et peuvent ne pas être préservés à l'appel suivant du addon dans Tacview.

{{% notice note %}}
**Valeur retournée :**<br>
handle de l'objet statique
ou nil si aucun objet à ce nom n'est trouvé.
{{% /notice %}}	Return value:


#### StaticObjects.SetVisible( staticObjectHandle , isVisible )
*Tacview 1.8.0*

Montre ou cache l'objet indiqué.
Vous pouvez utiliser *StaticObjects.GetHandleByName()* pour retrouver le handle de l'objet que vous souhaitez cacher/montrer.
