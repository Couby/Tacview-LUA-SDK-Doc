---
title: "Contexte"
date: 2019-04-13T18:16:48+02:00
draft: false
---

Comprend toutes les informations relatives à la représentation de la télémétrie à l'écran.
{{% notice tip %}}
NOTE : voir [Lua Main Interface](/lua-main-interface/) pour des fonctions additionnelles.
{{% /notice %}}

#### Context.GetAbsoluteTime()
*Tacview 1.7.5*

Retrouve le temps courant de la télémétrie en seconde **depuis le 01-01-1970** (ce paramètre est utile pour échanger avec le module Télémétrie).


#### Context.SetAbsoluteTime( absoluteTime )
*Tacview 1.7.6*

Règle le temps courant de la télémétrie pour le rejeu des données en secondes **depuis le 01-01-1970**.

{{% notice tip %}}
**NOTE :** NE PAS forcer le temps à chaque frame, en particulier durant l'enregistrement temps réel d'une télémétrie.<br>
Cela entrerait en conflit avec la mise à jour du temps interne à Tacview, ce qui amènerait des sauts dans la vue 3D.
{{% /notice %}}

Si vous souhaitez synchroniser le temps Tacview avec un outils externe, vous devriez ne le faire que lorsqu'il y a une différence de temps significative entre les deux outils :

	-- Synchronisation du temps Tacview seulement lorsque la différence de temps avec l'outils externe est supérieure à une seconde

	if math.abs(Context.GetAbsoluteTime() - externalToolTime) > 1.0 then
		Context.SetAbsoluteTime(externalToolTime)
	end
