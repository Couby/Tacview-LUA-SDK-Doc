---
title: "Context.Camera"
date: 2019-04-13T18:16:41+02:00
draft: false
---

La caméra est utilisée pour définir le point de vue de l'utilisateur dans la fenêtre 3D de Tacview.


#### Context.Camera.GetMode()
*Tacview 1.7.2*

Retourne le mode de caméra actuel.

{{% notice note %}}
**Valeur retournée :**<br>
		Camera.Cockpit<br>
		Camera.External<br>
		Camera.Satellite<br>
		Camera.Free
{{% /notice %}}


#### Context.Camera.SetOffset( offsetData )
*Tacview 1.7.2*

Décalage temporaire de la position et de la rotation de la caméra.

Le décalage est automatiquement réinitialisé à chaque nouvelle image lorsqu'il n'est pas remplacé par un addon.

Les composants suivants peuvent être spécifiés, ils sont tous facultatifs :

	offsetData =
	{
		lateral = meters_positive_to_the_right ,
		longitudinal = meters_positive_forward ,
		vertical = meters_positive_up ,
		roll = radian ,
		pitch = radian ,
		yaw = radian ,
	}


#### Context.Camera.SetFieldOfView( radian )
*Tacview 1.7.2*

Modifiez le champ de vision vertical de la caméra pour une image.

Le champ de vision est automatiquement réinitialisé à chaque nouvelle image lorsqu'il n'est pas remplacé par un addon.

Le champ de vision par défaut est 60 degrés.

{{% notice tip %}}
**NOTE :** Le champ de vision doit être défini en radian.
{{% /notice %}}
