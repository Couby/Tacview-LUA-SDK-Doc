---
title: "Paramètres"
date: 2019-04-13T18:16:53+02:00
draft: false
---

Cette interface permet d'accéder au paramètrage de Tacview.
Si vous souhaitez sauvegarder ou charger les paramètres de votre addon, regardez [AddOns.Current.Settings](/lua-core-interface/addons/#addons-current-settings-setboolean-settingname-newbooleanvalue-tacview-1-7-2)


#### Settings.SetBoolean( settingPath, newBooleanValue )
*Tacview 1.7.2*

Sauvegarde un réglage Booléen sous le nom donnée.

**settingPath** peut prendre une des valeurs suivantes :

*	`"UI.View.Grid.Visible"`			-- Active/désactive la grille latitude/longitude
*	`"UI.View.HUD.Visible"`			-- Active/désactive le head-up-display du cockpit
*	`"UI.View.Overlay.Visible"`		-- Active/désactive la surcouche d'informations affichée sur la vue 3D


#### Settings.GetBoolean( settingFullPath )
*Tacview 1.7.2*

Retourne la valeur du réglage actuel ou nil si le chemin indiqué ne pointe pas sur un réglage booléen.
Regardez [Settings.SetBoolean](/lua-core-interface/settings/#settings-setboolean-settingpath-newbooleanvalue) pour les valeurs possibles de **settingFullPath**.

{{% notice note %}}
**Valeur retournée :**<br>
valeur booléenne du réglage correspondant.
{{% /notice %}}


#### Settings.SetString( settingFullPath , newStringValue )
*Tacview 1.7.2*

Sauvegarde un réglage en chaîne de caractère sous le nom donné.

**settingFullPath** et **newStringValue** peuvent prendre les valeurs suivantes :

*	`"UI.View.Terrain.Mode"` -- Change la manière dont le terrain est affiché dans la vue 3D
*	`"Empty"`
*	`"Flat"`
*	`"3D"`
*	`"Full3D"`


#### Settings.GetString( settingFullPath )
*Tacview 1.7.2*

Retourne la valeur du réglage actuel ou nil si le chemin indiqué ne pointe pas sur un réglage sous forme de chaîne de caractères.
Regardez[Settings.SetString](/lua-core-interface/settings/#settings-setstring-settingfullpath-newstringvalue) pour les valeurs possibles de **settingFullPath**.

{{% notice note %}}
**Valeur retournée :**<br>
chaîne de caractères du réglage correspondant.
{{% /notice %}}
