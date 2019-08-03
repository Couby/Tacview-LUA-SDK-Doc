---
title: "Télémétrie"
date: 2019-04-13T18:16:47+02:00
draft: false
---

Ce module est le coeur de Tacview.

Utilisez le gestionnaire de télémétrie pour lire et écrire des données pour tout objet dynamique.

#### Telemetry.BeginningOfTime
*Tacview 1.7.5*
#### Telemetry.EndOfTime
*Tacview 1.7.5*

Constantes utilisées pour spécifier deux marqueurs de temps spéciaux.

	BeginningOfTime = -3.4028234663853e+38
	EndOfTime = 3.4028234663853e+38

**BeginningOfTime** est typiquement utilisé pour créer des objets intemporels comme les waypoints ou les bâtiments.
**EndOfTime** est utile par exemple pour identifier les objets encore vivants en fin d'enregistrement de télémétrie.

Si vous avec besoin de connaître l'horodatage des débuts et fin d'enregistrement de la télémétrie, regarder la fonction [Telemetry.GetDataTimeRange()](/Tacview-LUA-SDK-Doc/fr/lua-core-interface/telemetry/#telemetry-getdatatimerange)


#### Telemetry.InvalidPropertyIndex
*Tacview 1.7.5*

Constante utilisée pour détecter des propriétés invalides.


#### Telemetry.Tags
*Tacview 1.7.3*

Énumération des bits utilisés pour définir les types d'objets.

		-- Domain

		Telemetry.Tags.Air
		Telemetry.Tags.Ground
		Telemetry.Tags.Sea

		Telemetry.Tags.Weapon
		Telemetry.Tags.Sensor
		Telemetry.Tags.Navaid
		Telemetry.Tags.Misc

		-- Attributes

		Telemetry.Tags.Static
		Telemetry.Tags.Heavy
		Telemetry.Tags.Medium
		Telemetry.Tags.Light
		Telemetry.Tags.Minor

		-- Types basiques

		Telemetry.Tags.FixedWing
		Telemetry.Tags.Rotorcraft

		Telemetry.Tags.Armor
		Telemetry.Tags.AntiAircraft
		Telemetry.Tags.Vehicle
		Telemetry.Tags.Watercraft

		Telemetry.Tags.Human
		Telemetry.Tags.Biologic

		Telemetry.Tags.Missile
		Telemetry.Tags.Rocket
		Telemetry.Tags.Bomb
		Telemetry.Tags.Torpedo
		Telemetry.Tags.Projectile
		Telemetry.Tags.Beam

		Telemetry.Tags.Decoy

		Telemetry.Tags.Building

		Telemetry.Tags.Bullseye
		Telemetry.Tags.Waypoint

		-- Specific Type

		Telemetry.Tags.Tank
		Telemetry.Tags.Warship
		Telemetry.Tags.AircraftCarrier
		Telemetry.Tags.Submarine
		Telemetry.Tags.Infantry
		Telemetry.Tags.Parachutist

		Telemetry.Tags.Shell
		Telemetry.Tags.Bullet

		Telemetry.Tags.Flare
		Telemetry.Tags.Chaff
		Telemetry.Tags.SmokeGrenade

		Telemetry.Tags.Aerodrome

		Telemetry.Tags.Container
		Telemetry.Tags.Shrapnel
		Telemetry.Tags.Explosion

Cas d'usage pour identifier si un objet est de type avion :

	local objectTags = Tacview.Telemetry.GetCurrentTags( objectHandle )

	if (Tacview.Telemetry.AllGivenTagsActive(objectTags, Tacview.Telemetry.Tags.FixedWing)) then
	    this_is_a_plane;
	end


#### Telemetry.AllGivenTagsActive( objectTags , activeTagsCombination )
*Tacview 1.8.0*
#### Telemetry.AnyGivenTagActive( objectTags , activeTagsCombination )
*Tacview 1.8.0*

Aides pour savoir si tout ou partie de combinaisons de tags correspond aux tags d'un objet donné.
Vous retrouvez les tags actuels d'un objets (qui définissent le type de l'objet) avec la fonction [Telemetry.GetCurrentTags](/Tacview-LUA-SDK-Doc/fr/lua-core-interface/telemetry/#telemetry-getcurrenttags-objecthandle).

{{% notice note %}}
**Return value:**<br>
		true or false depending on the match
{{% /notice %}}


#### Telemetry.Property
*Tacview 1.7.6*

Liste des noms des propriétés supportées nativement par Tacview.

		-- Propriétés de textes

		Telemetry.Property.Text.Callsign
		Telemetry.Property.Text.Event
		Telemetry.Property.Text.Name

		-- Propriétés numériques

		Telemetry.Property.Numeric.Disabled
		Telemetry.Property.Numeric.EngagementRange


#### Telemetry.Clear()
*Tacview 1.7.2*

Purge toutes les données de télémétrie actuellement chargées en mémoire.

Cette fonction ne prévient pas l'utilisateur et ne lui donne pas la possibilité de sauvegarder des données.

Cette fonction n'interrompt ni n'arrête aucun enregistrement en cours. Il purge simplement toutes les données enregistrées jusque-là.


#### Telemetry.Load( fileName )
*Tacview 1.8.0*

Cette fonction fusionne le fichier de données indiqué avec celui déjà en mémoire.
Appelez *Telemetry.Clear()* avant de charger de nouvelles données si vous ne souhaitez pas fusionner.

{{% notice note %}}
**Valeur retournée :**<br>
true si le fichier indiqué a correctement été chargé<br>
{{% /notice %}}


#### Telemetry.IsEmpty()
*Tacview 1.7.6*

Indique si aucune télémétrie n'est actuellement chargée en mémoire.

Cela inclut les données intemporelles.


#### Telemetry.IsLikeEmpty()
*Tacview 1.7.6*

Indique si aucune télémétrie significative n'est actuellement chargée en mémoire.

Par exemple, si aucune donnée ou seulement des données intemporelles sont chargées, cette fonction renvoie **true**.

Sinon, il retourne **false**.


#### Telemetry.GetDataTimeRange()
*Tacview 1.7.6*

Récupère l'étendue des données de télémétrie actuellement chargées en mémoire.

Ceci exclut les échantillons intemporels tels que la position des bullseyes par exemple.

{{% notice note %}}
**Valeur retournée :**<br>
	{<br>
		beginTime,		-- premier échantillon de temps absolu<br>
		endTime			-- dernier échantillon de temps absolu<br>
	}
{{% /notice %}}


#### Telemetry.GetCurrentObjectHandle( objectId )
*Tacview 1.7.2*

Récupère le descripteur de l'objet - objectHandle - spécifié à l'heure de mise à jour actuelle.

S'il existe plusieurs objets ayant le même identifiant (par exemple, un joueur ayant été créés plusieurs fois dans le même aéronef au cours d'une même session), le gestionnaire de télémétrie renvoie l'objet le plus approprié pour la période actuelle.

Contrairement aux ID, les descripteurs d'objets identifient de manière unique chaque objet actuellement chargé en mémoire.

{{% notice note %}}
**Valeur retournée :**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetCurrentOrCreateObjectHandle( objectId )
*Tacview 1.7.5*

Récupère le descripteur de l'objet - objectHandle - spécifié à l'heure de mise à jour actuelle.

Si l'identifiant d'objet donné n'est pas trouvé, un nouvel objet sera créé à la mise à jour actuelle avec l'identifiant donné.

Contrairement aux ID, les descripteurs d'objets identifient de manière unique chaque objet actuellement chargé en mémoire.

{{% notice note %}}
**Valeur retournée :**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetOrCreateObjectHandle( objectId , absoluteTime )
*Tacview 1.7.5*

Récupère le descripteur de l'objet spécifié à l'heure spécifiée.

Si l'identifiant d'objet donné n'est pas trouvé, un nouvel objet sera créé à l'heure spécifiée avec l'identifiant donné.

Contrairement aux ID, les descripteurs d'objets identifient de manière unique chaque objet actuellement chargé en mémoire.

Pour créer un objet intemporel comme un waypoint, vous pouvez utiliser les éléments suivants :
`local newObjectHandle = Tacview.Telemetry.GetOrCreateObjectHandle( objectId , Tacview.Telemetry.BeginningOfTime )`

{{% notice note %}}
**Valeur retournée :**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetCurrentTags( objectHandle )
*Tacview 1.7.3*

Return given object tags as a bit field.
Renvoie le tag de l'objet indiqué sous forme de champ de bits.

{{% notice note %}}
**Valeur retournée :**<br>
		Chaque bit du nombre entier renvoyé correspond à un tag spécifique. <br>
		La combinaison de ces balises définit le type d'objet actuel. <br>
		Le type d'objet peut évoluer dans le temps et être affiné en fonction de la télémétrie disponible à ce moment.
{{% /notice %}}


#### Telemetry.GetCurrentShortName( objectHandle )
*Tacview 1.7.2*

Renvoie le nom abrégé de l'objet donné à la mise à jour actuelle.

{{% notice note %}}
**Valeur retournée :**<br>
		Texte qui correspond généralement au code OTAN ou à toute autre désignation courte appropriée pour l'objet.
{{% /notice %}}


#### Telemetry.GetTransform( objectHandle , absoluteTime )
*Tacview 1.7.5*
#### Telemetry.GetCurrentTransform( objectHandle )
*Tacview 1.7.2*

Renvoie la position / rotation de l'objet donnée à la mise à jour actuelle ou à l'heure spécifiée.

Certains objets (généralement les obus) peuvent ne pas avoir toutes les informations disponibles.

Par exemple, les informations de rotation peuvent ne pas être disponibles pour tous les aéronefs.

Les coordonnées natives correspondent aux coordonnées d'origine dans le simulateur de vol source (généralement pour BMS et DCS).

{{% notice note %}}
**Valeur retournée :**<br>
{{% /notice %}}

		ObjectTransform =
		{
			time = sample_absolute_time,			-- (secondes) L'heure absolue effective de cet échantillon peut être différente de l'heure de mise à jour actuelle si l'objet n'existe pas encore, ou plus...

			x = cartesianPositionX,					-- (mètres) position cartésienne (TOUJOURS DISPONIBLE)
			y = cartesianPositionY,					-- (mètres) position cartésienne (TOUJOURS DISPONIBLE)
			z = cartesianPositionZ,					-- (mètres) position cartésienne (TOUJOURS DISPONIBLE)

			longitude = sphericalLongitude,			-- (radian) position sphérique (TOUJOURS DISPONIBLE)
			latitude = sphericalLatitude,			-- (radian) position sphérique (TOUJOURS DISPONIBLE)
			altitude = absoluteAltitude,			-- (mètres) position sphérique (TOUJOURS DISPONIBLE)

			roll = objectRoll,						-- (radian) axe de rotation en roulis (si rotationIsValid == true)
			pitch = objectPitch,					-- (radian) axe de rotation en tangage (sif rotationIsValid == true)
			yaw = objectYaw,						-- (radian) axe de rotation en lacet (si rotationIsValid == true)

			u = nativePositionX,					-- (mètres) coordonnée native x (si nativeCoordinatesAreValid == true)
			v = nativePositionY,					-- (mètres) coordonnée native y (si nativeCoordinatesAreValid == true)
			heading = nativeHeadingToNorth,			-- (radian) Heading dans le système de coordonnées natif (si nativeCoordinatesAreValid == true & rotationIsValid == true)

			rotationIsValid = boolean,				-- Définie à true si les informations de rotation sont valides (sinon, les données peuvent être émulées)
			nativeCoordinatesAreValid = boolean,	-- Définie à true si les coordonnées natives sont valides (sinon u, v et heading sont mis à zéro)
		}

{{% notice note %}}
**Valeur retournée :**<br>
		value , validity<br>
		validity est défini sur false si la valeur ne s'applique pas vraiment pour le moment donné (généralement si l'objet n'existe pas à ce moment-là) événement lorsque la validité est définie sur false, la valeur est valide et utilisable (cela simplifie le code client)
{{% /notice %}}


#### Telemetry.GetVerticalGForce( objectHandle , absoluteTime )
*Tacview 1.8.0*
#### Telemetry.GetCurrentVerticalGForce( objectHandle )
*Tacview 1.7.3*

Retourne le facteur de charge vertical s'il est disponible à l'heure actuelle.

Le g-Force vertical est le g-Force qui s'applique au pilote et à son avion. C'est celui généralement affiché en cabine.

Si le facteur de charge vertical a été enregistré, Tacview renverra l'échantillon interpolé.
Si le facteur de charge vertical n'a pas été enregistré, mais que les données de rotation sont disponibles, Tacview calculera le facteur de charge vertical.

{{% notice note %}}
**Valeur retournée :**<br>
		**Vertical G-Force** si disponible.<br>
		**nil** quand il n'y a pas suffisamment de données disponibles (ou l'objet n'existe pas à ce moment).
{{% /notice %}}


#### Telemetry.GetAbsoluteGForce( objectHandle , absoluteTime )
*Tacview 1.8.0*
#### Telemetry.GetCurrentAbsoluteGForce( objectHandle )
*Tacview 1.8.0*

Retourne le facteur de charge absolu de l'objet s'il est disponible à l'heure actuelle.

Le g-Force absolu est l'accélération de l'objet divisé par G. Il est indépendant de l'orientation de l'objet ou de sa trajectoire.

{{% notice note %}}
**Valeur retournée :**<br>
		**Absolute g-Force** si disponible.<br>
		**nil** quand il n'y a pas suffisamment de données disponibles (ou l'objet n'existe pas à ce moment).
{{% /notice %}}


#### Telemetry.GetGlobalNumericPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.6*
#### Telemetry.GetGlobalTextPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.6*

Récupérer une propriété pour l'objet global (0).

Si la propriété n'existe pas encore :

- Si autoCreate est à true, la propriété sera créée et son index renvoyé.
- Si autoCreate est sur false, Telemetry.InvalidPropertyIndex sera renvoyé.

Pour optimiser la charge CPU et mémoire, les propriétés numériques et textuelles sont séparées dans le gestionnaire de télémétrie.

{{% notice info %}}
**ATTENTION :** Les propriétés numériques et textuelles étant séparées, les index des échantillons numériques et textuels peuvent se chevaucher et ne peuvent pas être mélangés.
{{% /notice %}}


#### Telemetry.GetObjectsNumericPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.5*
#### Telemetry.GetObjectsTextPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.5*

Récupérez un index de propriété pour tout ce qui n'est pas l'objet global.

L'index renvoyé est le même pour tous les objets.

Si la propriété n'existe pas encore:

- Si autoCreate est à true, la propriété sera créée et son index renvoyé.
- Si autoCreate est sur false, Telemetry.InvalidPropertyIndex sera renvoyé.

Pour optimiser la charge CPU et mémoire, les propriétés numériques et textuelles sont séparées dans le gestionnaire de télémétrie.

{{% notice info %}}
**ATTENTION :** Les propriétés numériques et textuelles étant séparées, les index des échantillons numériques et textuels peuvent se chevaucher et ne peuvent pas être mélangés.
{{% /notice %}}


#### Telemetry.GetNumericSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.7.5*
#### Telemetry.GetTextSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.7.5*

Récupère la valeur numérique ou textuelle de la propriété à un moment donné.

{{% notice note %}}
**Valeur retournée :**<br>
		value , validity<br>
		validité est définie sur false si la valeur ne s'applique pas vraiment pour le moment donné (généralement si l'objet n'existe pas à ce moment-là) événement lorsque la validité est définie sur false, la valeur est valide et utilisable (cela simplifie le code client)
{{% /notice %}}


#### Telemetry.SetNumericSample( objectHandle , absoluteTime , propertyIndex , value )
*Tacview 1.7.5*
#### Telemetry.SetTextSample( objectHandle , absoluteTime , propertyIndex , value )
*Tacview 1.7.5*

Définir ou redéfinir une valeur numérique ou une propriété de texte donnée à un moment donné.

Vous pouvez définir **absoluteTime** sur **Tacview.Telemetry.BeginningOfTime** pour déclarer les propriétés des objets intemporels tels que les waypoints.


#### Telemetry.GetNumericSampleCount( objectHandle , propertyIndex )
*Tacview 1.8.0*
#### Telemetry.GetTextSampleCount( objectHandle , propertyIndex )
*Tacview 1.8.0*

Récupère le nombre d'échantillons actuellement chargés en mémoire pour l'objet spécifié.
Cette fonction est généralement utilisée pour énumérer les échantillons d'objets.


#### Telemetry.GetNumericSampleFromIndex( objectHandle , sampleIndex , propertyIndex )
*Tacview 1.8.0*
#### Telemetry.GetTextSampleFromIndex( objectHandle , sampleIndex , propertyIndex )
*Tacview 1.8.0*

Récupérer une donnée de télémétrie d'objet spécifique à partir de son index.
SampleIndex commence à 0 et se termine au compte-1.

{{% notice note %}}
**Return value:**<br>
		sampleValue , sampleTime , validity<br>
		Retourne nil si invalide
{{% /notice %}}


#### Telemetry.SetTransform( objectHandle , absoluteTime , transform )
*Tacview 1.7.5*

Définir ou redéfinir la position et la rotation de l'objet à l'heure indiquée.

**absoluteTime** est un nombre à virgule flottante de 64 bits représentant le nombre de secondes écoulées jusqu'au 1970-01-01T00: 00: 00Z

Les angles injectés (y compris la longitude et la latitude) DOIVENT être normalisés entre ]-pi, +pi]

Si vous ne le faites pas, certaines formules pourraient produire des résultats non définis.

Pour des raisons de performances, les angles récupérés par le gestionnaire de télémétrie **NE sont PAS** toujours normalisés entre ]-pi, +pi]

N'oubliez pas de normaliser les angles avant d'afficher ensuite le texte à l'utilisateur final !

-- les membres non spécifiés seront définis sur la valeur interpolée des échantillons précédent et suivant.

	transform
	{
		-- position sphérique

		f64 longitude;		-- (radian) position sphérique (+ est vers l'est)
		f64 latitude;		-- (radian) position sphérique (+ est vers le nord)
		f32 altitude;		-- (mètres) position sphérique

		-- Rotation

		f32 roll;			-- (radian) axe de rotation en roulis
		f32 pitch;			-- (radian) axe de rotation en tangage
		f32 yaw;			-- (radian) axe de rotation en lacet

		-- Les coordonnées natives, utilisées principalement pour obtenir un calcul précis de la distance et de la vitesse pour les simulateurs de monde plat.

		f32 u;				-- (mètres) coordonnée native x
		f32 v;				-- (mètres) coordonnée native y
		f32 heading;		-- (radian) Heading dans le système de coordonnées natif
	};


#### Telemetry.GetTransformTimeRange( objectHandle )
*Tacview 1.8.0*

Retrouve les temps du premier et du dernier échantillon transform de l'objet spécifié.
Cette fonction est typiquement utilisé pour énumérer les échantillons sur la période de vie effective.
Retourne *nil* si l'objet n'a pas d'échantillon transform disponible.
Notez que *Telemetry.BeginningOfTime* peut être retournée si l'objet n'est pas temporel comme le Bullseye.

{{% notice note %}}
**Valeur retournée :**<br>
	{<br>
		firstTransformSampleTime,		-- temps absolu du premier échantillon transform existant<br>
		lastTransformSampleTime			-- temps absolu du dernier échantillon transform existant<br>
	}
{{% /notice %}}


#### Telemetry.GetLifeTime( objectHandle )
*Tacview 1.7.6*

Renvoie l'heure absolue de la première apparition de l'objet et l'heure de sa disparition, le cas échéant.
A la différence de *GetObjectDataTimeRange()*, cette fonction peut retourner une plage de temps plus grande pouvant aller jusqu'à *Telemetry.EndOfTime* si l'objet n'a jamais été détruit ou retiré du champs de bataille.
Utilisez préférentiellement *GetTransformTimeRange()* si vous souhaitez itérer sur les échantillons de télémétrie de l'objet via un compteur de temps.

{{% notice note %}}
**Valeur retournée :**<br>
		lifeTimeBegin, lifeTimeEnd
{{% /notice %}}

Si l'objet existe depuis le début des temps (par exemple, un bullseye), son **lifeTimeBegin** est **Telemetry.BeginningOfTime**.

Si l'objet n'a jamais été détruit ni supprimé du champ de bataille, **lifeTimeEnd** est **Telemetry.EndOfTime**.


#### Telemetry.SetLifeTimeEnd( objectHandle , absoluteTime )
*Tacview 1.7.5*

Définit la fin de vie de l'objet spécifié.

Généralement utilisé pour spécifier quand un objet a été détruit ou a été retiré du champ de bataille.


#### Telemetry.RemoveNumericSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.8.0*
#### Telemetry.RemoveNumericSampleFromIndex( objectHandle , sampleIndex , propertyIndex )
*Tacview 1.8.0*
#### Telemetry.RemoveTextSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.8.0*
#### Telemetry.RemoveTextSampleFromIndex( objectHandle , sampleIndex , propertyIndex )
*Tacview 1.8.0*

Supprimer la valeur de l'échantillon à l'heure ou à l'index spécifié.

{{% notice note %}}
**Return value:**<br>
		true si l'opération de suppression s'est bien passée<br>
		false si l'un des paramètres est obsolète (en raison d'un changement de télémétrie en temps réel, par exemple)
{{% /notice %}}


#### Telemetry.DeleteObject( objectHandle )
*Tacview 1.7.5*

Supprime l'objet spécifié du gestionnaire de télémétrie.

Cette opération est sécurisée: le descripteur - handle - correspondant restera valide jusqu'à la prochaine purge effective (généralement lors du chargement d'un nouveau fichier de télémétrie) afin que les autres modules ne se bloquent pas s'ils tentent de référencer l'objet par la suite.

Cependant, toutes les données liées à cet objet seront libérées.


#### Telemetry.GetObjectCount()
*Tacview 1.7.6*

Récupère le nombre total d'objets actuellement actifs dans le gestionnaire de télémétrie.

Généralement utilisé pour énumérer tous les objets.


#### Telemetry.GetObjectHandleByIndex( index )
*Tacview 1.7.6*

Récupère un objet par son index.
{{% notice tip %}}
**NOTE :** L'index va de **0** à **GetObjectCount() - 1**.
{{% /notice %}}

{{% notice note %}}
**Valeur retournée :**<br>
		Le descripteur - **handle** - de l'objet ou **nil** si l'index est hors de portée.
{{% /notice %}}


#### Telemetry.GetObjectId( objectHandle )
*Tacview 1.7.6*

Récupère l'identifiant d'objet donné.

Attention, les identifiants d'objet peuvent être recyclés et ne peuvent pas identifier des objets de manière unique.

Pour cette raison, évitez de les utiliser, à moins que ce soit pour l'injection de télémétrie (création d'événement) ou l'exportation.
