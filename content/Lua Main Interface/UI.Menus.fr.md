---
title: "UI.Menus"
date: 2019-04-13T18:16:45+02:00
draft: false
---

L’interface Menu est utile pour créer et insérer des commandes et des options dans les menus de Tacview.

Tous les nouveaux menus seront ajoutés au menu des addons.

Tacview supprimera automatiquement les éléments de menu d'un addon qui est déchargé.


#### UI.Menus.AddMenu( parentMenuId , textLabel )
*Tacview 1.7.2*

Crée et insère un menu dans le menu Tacview.

Vous pouvez spécifier l'identifiant d'un menu parent ou vous pouvez utiliser **nil** pour insérer votre menu dans le menu principal des add-ons Tacview.

{{% notice note %}}
**Valeur retournée :**<br>
		un id de menu (entier) qui peut être utilisé plus tard pour insérer des sous-éléments ou pour supprimer le menu.
{{% /notice %}}


#### UI.Menus.AddSeparator( parentMenuId )
*Tacview 1.8.0*

Ajoute un séparateur dans le menu indiqué.
Utilisez des séparateurs pour grouper des options et commandes, rendant ainsi vos menus plus intuitifs pour vos utilisateurs.


#### UI.Menus.AddCommand( parentMenuId , textLabel , function )
*Tacview 1.7.2*

Insére une commande dans le menu donné.

Vous pouvez spécifier l'identifiant d'un menu parent ou vous pouvez utiliser **nil** pour insérer votre menu dans le menu principal des add-ons Tacview.

**function** sera appelé chaque fois que cette commande de menu aura été cliquée.

{{% notice note %}}
**Valeur retournée :**<br>
		un id de menu (entier) qui peut être utilisé plus tard pour insérer des sous-éléments ou pour supprimer le menu.
{{% /notice %}}


#### UI.Menus.AddOption( parentMenuId , textLabel , optionBoolean , function )
*Tacview 1.7.2*

Insére une commande avec une coche dans le menu donné.

Si **optionBoolean** est true, une coche apparaîtra après le libellé de la commande.

Vous pouvez spécifier l'identifiant d'un menu parent ou vous pouvez utiliser **nil** pour insérer votre menu dans le menu principal des add-ons Tacview.

**function** sera appelé chaque fois que cette option de menu aura été cliquée.

{{% notice note %}}
**Return value:**<br>
		id de Manu qui peut être utilisé plus tard pour changer la valeur de l'option au moyen de **UI.Menus.SetOption()**.
{{% /notice %}}


#### UI.Menus.SetOption( menuId , optionBoolean )
*Tacview 1.7.2*

Changer la valeur d'une option de menu.
Si **optionBoolean** est true, une coche apparaîtra à côté du libellé de la commande correspondante.
