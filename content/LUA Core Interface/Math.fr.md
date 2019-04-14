---
title: "Math"
date: 2019-04-13T18:16:49+02:00
draft: false
---

Ce module contient tous les outils nécessaires pour convertir et modifier les données typiques de la télémétrie.

Ici, nous appelons vecteurs, des tables comprenant trois composantes :

	{
		x = nombre,
		y = nombre,
		z = nombre,
	}

#### Math.Angle.Subtract( leftAngle , rightAngle )
*Tacview 1.7.2*

Soustraction entre deux angles en radian.

{{% notice note %}}
**Valeur retournée :**<br>
	Différence entre **leftAngle** et **rightAngle**.<br>
	Le résultat est normalisé entre **[-pi, +pi]**.
{{% /notice %}}


#### Math.Vector.LongitudeLatitudeToCartesian( {longitude = number , latitude = number , altitude = number} )
*Tacview 1.7.2*

Convertis des coordonnées sphériques terrestres en coordonnées cartésiennes.
Il est possible de directement donner une transformée d'objet à cette fonction, voir [Telemetry.GetCurrentTransform](/telemetry/#telemetry-getcurrenttransform-objecthandle-tacview-1-7-2).

**Longitude** et **latitude** sont en radian.
**Altitude** est en mètres.

{{% notice note %}}
**Valeur retournée :**<br>
	Un **vecteur** représentant une position cartésienne dans l'espace terrien global.
{{% /notice %}}


#### Math.Vector.CartesianToLongitudeLatitude( {x = number , y = number , z = number} )
*Tacview 1.7.5*

Convertis des coordonnées cartésiennes en coordonnées sphériques terrestres.

{{% notice note %}}
**Valeur retournée :**<br>
	Une **table** contenant { longitude = ... , latitude = ... , altitude = ...}<br>
	Longitude et latitude sont en radian.<br>
	Altitude est en mètres.
{{% /notice %}}


#### Math.Vector.Add( vector1 , vector2 )
*Tacview 1.7.2*

Somme de deux vecteurs 3D.

{{% notice note %}}
**Valeur retournée :**<br>
	Un **vecteur** représentant la somme de **vector1** et **vector2**.
{{% /notice %}}


#### Math.Vector.Subtract( vector1 , vector2 )
*Tacview 1.7.2*

Différence entre deux veteurs 3D.

{{% notice note %}}
**Valeur retournée :**<br>
	Un **vecteur** représentant la différence entre **vector1** et **vector2**.
{{% /notice %}}


#### Math.Vector.Multiply( factor , vector )
*Tacview 1.7.5*

Multiplie un vecteur désigné par une valeur scalaire.

{{% notice note %}}
**Valeur retournée :**<br>
	La **vector** mis à l'échelle.
{{% /notice %}}


#### Math.Vector.Normalize( vector )
*Tacview 1.7.2*

Normalise un vecteur donné.

{{% notice note %}}
**Valeur retournée :**<br>
	**vector** normalisé.<br>
	Cette fonction est sûre, aussi un vecteur nul indique que le vecteur est nul.
{{% /notice %}}


#### Math.Vector.AngleBetween( vector1 , vector2 )
*Tacview 1.7.2*

Calcule l'angle entre deux vecteurs *normalisés*.
{{% notice info %}}
NE PAS oublier de normaliser les vecteurs avant l'appel GetAngle!
{{% /notice %}}
{{% notice tip %}}
NOTE : Si vous souhaitez un calcul quadran exact, vous devriez plutôt utiliser la fonction à trois paramètres.
{{% /notice %}}

{{% notice note %}}
**Valeur retournée :**<br>
	**Angle** en radian entre les deux vecteurs donnés.<br>
	Cela correspond à `ArcCos( DotProduct( vector1, vector2 ) )`
{{% /notice %}}


#### Math.Vector.AngleBetween( vector , referenceVector1 , referenceVector2 )
*Tacview 1.7.2*

Calcule l'angle entre deux vecteurs *normalisés*.
{{% notice info %}}
NE PAS oublier de normaliser les vecteurs avant l'appel GetAngle!
{{% /notice %}}
Contrairement à **AngleBetween( vector1 , vector2 )**, cette fonction donne le quadran exact.

{{% notice note %}}
**Valeur retournée :**<br>
	**Angle** en radian entre les deux vecteurs donnés.<br>
	Cela correspond à `ArcTan( DotProduct( vector, referenceVector1 ), DotProduct( vector, referenceVector2 ) )`
{{% /notice %}}


#### Math.Vector.LocalToGlobal( objectTransform , localCoordinates )
*Tacview 1.7.2*

Convertis le point donné des coordonnées d'un objet local en coordonnées cartésiennes terrestres.

Vous pouvez directement passer en argument de cette fonction, la table **objectTransform** provenant de **Telemetry.GetCurrentTransform()** dans laquelle **localCoordinates** est un vecteur.

	objectTransform =
	{
		-- Si xyz ne sont pas précisés, ils seront calculés à partir des informations longitude, latitude, et altitude.

		x = cartesianPositionX,					-- mètres
		y = cartesianPositionY,					-- mètres
		z = cartesianPositionZ,					-- mètres

		-- Si longitude ou latitude n'est pas précisé, ils sont calculés à partir du xyz.

		longitude = sphericalLongitude,			-- radian
		latitude = sphericalLatitude,			-- radian
		altitude = absoluteAltitude,			-- (mètres) requis seulement si xyz n'est pas spécifié

		roll = objectRoll,						-- radian
		pitch = objectPitch,					-- radian
		yaw = objectYaw,						-- radian
	}

{{% notice note %}}
**Valeur retournée :**<br>
	**coordonnées comme vecteur** dans l'espace global cartésien terrestre.<br>
	retourne **nil** dans le cas où la quantité d'information fournie n'est pas suffisante.
{{% /notice %}}
