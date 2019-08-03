---
title: "Add Ons"
date: 2019-04-13T18:16:52+02:00
draft: false
---


L'interface add-ons est principalement destinée à préciser des informations concernant votre add-on.

Les réglages de votre addon seront sauvegardés à la fermeture et rechargés à l'ouverture de Tacview.


#### AddOns.Current.GetPath()
*Tacview 1.7.4*

Retrouve le chemin racine actuel du addon.

C'est typiquement là où se trouve le dll ou lua de votre addon.

Cette fonction est utile pour accéder ou charger vos ressources personnalisées sans avoir à coder en dur le chemin vers celles-ci.

{{% notice note %}}
**Valeur retournée :**<br>
		**chemin** du addon (i.e. `C:\ProgramData\Tacview\AddOns\Tutorial 1 - Hello World - CS\`)<br>
		ou **nil** si non applicable (généralement pour le code Lua injecté sur un tuyau)
{{% /notice %}}


#### AddOns.Current.SetTitle( addOnTitle )
*Tacview 1.7.2*

Défini un nom plus joli à montrer que le nom de répertoire du addon qui est affiché par défaut dans l'UI Tacview.


#### AddOns.Current.SetVersion( textVersionNumber )
*Tacview 1.7.2*

Il est recommandé de déclarer la version de votre add-on en utilisant cette fonction.

De cette manière, il sera plus facile pour l'utilisateur final de savoir si le moment est venu d'en télécharger une mise à jour.


#### AddOns.Current.SetAuthor( authorName )
*Tacview 1.7.2*

Faire savoir à tout le monde qui est l'auteur de ce magnifique add-on !


#### AddOns.Current.SetNotes( textNotes )
*Tacview 1.7.2*

Défini un texte affiché dans la barre de statut Tacview lorsque le addon est sélectionné dans le menu addons.

Une fenêtre dédiée sera disponible dans Tacview 2.


#### AddOns.Current.Settings.SetBoolean( settingName , newBooleanValue )
*Tacview 1.7.2*

Sauvegarde un réglage booléen sous le nom donné.

SettingName doit être une chaîne de caractère permettant d'identifier sans ambiguitée votre réglage.
SettingName ne doit pas prendre la valeur "Enabled" laquelle est réservée par Tacview pour activer/désactiver le addon.


#### AddOns.Current.Settings.GetBoolean( settingName , defaultBooleanValue )
*Tacview 1.7.2*

Retourne la valeur courante du réglage, ou bien celle fournie par défaut si aucune valeur n'a été sauvegardée auparavant.

{{% notice note %}}
**Valeur retournée :**<br>
valeur booléenne du réglage correspondant.
{{% /notice %}}
