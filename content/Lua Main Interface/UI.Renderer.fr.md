---
title: "UI.Renderer"
date: 2019-04-13T18:16:44+02:00
draft: false
---

Le rendu est généralement utilisé pour afficher des objets dans la vue 3D principale.

{{% notice tip %}}
NOTE: Les fonctions de dessin peuvent être appelées *uniquement* pendant les événements de dessin.
{{% /notice %}}

Voir [Events.*](/lua-main-interface/events/) pour savoir comment enregistrer des callbacks de dessin.


#### UI.Renderer.GetWidth()
*Tacview 1.7.2*

Récupérer la largeur de rendu en pixels ou **nil** en dehors d'un événement de dessin.


#### UI.Renderer.GetHeight()
*Tacview 1.7.2*

Récupère la hauteur du moteur de rendu en pixels ou **nil** en dehors d'un événement de dessin.


#### UI.Renderer.LoadTexture( texturePath [, wrapRepeat [, compressed] ] )
*Tacview 1.7.3*
#### UI.Renderer.UnloadTexture( textureHandle )
*Tacview 1.7.3*

**wrapRepeat** = doit être défini sur true si vous souhaitez que la texture soit répétée (par défaut = true)

**compressed** = doit être défini sur true si vous souhaitez que la texture soit compressée (recommandé) (par défaut = true)

Chargez un fichier png ou jpg et compilez-le en tant que texture.

Seuls les formats 24 bits et 32 bits sont pris en charge.

Le format 32 bits peut être utilisé pour dessiner des textures translucides.

Les textures sont directement utilisées par **UI.Renderer.CreateRenderState**

Les textures sont utilisées indirectement (dans les états de rendu) par **UI.Renderer.DrawObjectVertexArray** et **UI.Renderer.DrawUIVertexArray**.

Les textures sont automatiquement déchargées lorsque le module complémentaire est libéré.

{{% notice note %}}
**Valeur retournée :**<br>
		Le handle de texture ou **nil** si le fichier n'a pas été trouvé ou invalide.
{{% /notice %}}


#### UI.Renderer.CreateVertexArray( vertexArray )
*Tacview 1.7.2*
#### UI.Renderer.ReleaseVertexArray( vertexArrayHandle )
*Tacview 1.7.2*

Les tableaux de vertex sont une liste de points 3D utilisés pour afficher des bandes de triangle, qui à leur tour représentent des objets 3D à l'écran.

Les matrices de vertex sont automatiquement libérées lorsque l'addon est déchargé.

Typiquement:

- Vous devez appeler une fois (par objet 3D) **UI.Renderer.CreateVertexArray()** pour préparer votre tableau de sommets.
- Ensuite, dans votre rappel **Events.DrawOpaqueObjects()**, vous pouvez utiliser le descripteur renvoyé par **CreateVertexArray()** pour dessiner votre objet à l'aide de **UI.Renderer.DrawVertexArray()**.
- Chaque fois que le tableau de vertex n'est plus requis, vous pouvez libérer la ressource associée en appelant **UI.Renderer.ReleaseVertexArray()**.

	vertexArray =
	{
		x, y, z,
		...
	}

{{% notice note %}}
**Valeur retournée :**<br>
		handle (entier) du tableau compilé ou **nil** si le tableau n'est pas valide.
{{% /notice %}}


#### UI.Renderer.CreateTextureCoordinateArray( textureCoordinateArray )
*Tacview 1.7.3*
#### UI.Renderer.ReleaseTextureCoordinateArray( textureCoordinateArrayHandle )
*Tacview 1.7.3*

Les tableaux de coordonnées de texture sont une liste de coordonnées 2D utilisées pour texturer des bandes de triangle.

Ils sont automatiquement libérés lorsque l'addon est déchargé.

	textureCoordinateArray =
	{
		u, u,
		...
	}

{{% notice note %}}
**Valeur retournée :**<br>
		handle (entier) du tableau compilé ou **nil** si le tableau n'est pas valide.
{{% /notice %}}


#### UI.Renderer.CreateRenderState( renderState )
*Tacview 1.7.2*
#### UI.Renderer.ReleaseRenderState( renderStateHandle )
*Tacview 1.7.2*

L'état de dessin décrit les constantes qui seront utilisées pour un ou plusieurs appels à dessin.

Généralement utilisé pour spécifier une couleur unique pour un modèle 3D complet, ainsi qu'une liste de textures utilisées lors des opérations de dessin.

Vous pouvez utiliser à tout moment **UI.Renderer.ReleaseRenderState()** pour libérer la ressource associée à un état de dessin précédemment compilé.

Les états de dessin sont automatiquement libérés lorsque l'addon est déchargé.

	renderState =
	{
		-- Couleur OPTIONNELLE (blanc opaque par défaut)
		-- Rouge opaque : 0xff0000ff
		-- Vert opaque : 0xff00ff00
		-- Bleu opaque : 0xffff0000

		[color = 32_bit_rgba_color_code,]

		-- Texture OPTIONNELLE chargée avec UI.Renderer.LoadTexture()

		[texture = textureHandle,]

		-- Mode de fusion OPTIONNELLE (pour les phases de rendu transparentes)

		[
			blendMode =
					Tacview.UI.Renderer.BlendMode.Normal
					Tacview.UI.Renderer.BlendMode.Additive
		]
	}

{{% notice note %}}
**Valeur retournée :**<br>
		handle (entier) du tableau compilé ou **nil** si le tableau n'est pas valide.
{{% /notice %}}


#### UI.Renderer.DrawObjectVertexArray( transform , renderStateHandle , vertexArrayHandle )
*Tacview 1.7.2*
#### UI.Renderer.DrawObjectVertexArray( transform , renderStateHandle , vertexArrayHandle [, textureCoordinateArrayHandle] )
*Tacview 1.7.3*

**renderStateHandle** est un entier précédemment renvoyé par **UI.Renderer.CreateRanderState()**

**vertexArrayHandle** est un entier précédemment renvoyé par **UI.Renderer.CreateVertexArray()**

**textureCoordinateArrayHandle** est un entier optionnel précédemment renvoyé par **UI.Renderer.CreateTextureCoordinateArray()**

	transform =
	{
		-- Si la position cartésienne xyz dans l'espace global terrestre n'est pas fournie, elle sera calculée en fonction de la position sphérique (longitude, latitude, altitude).

		x = nombre,
		y = nombre,
		z = nombre,

		-- Si la position sphérique n'est pas fournie, elle sera calculée en fonction de la position cartésienne xyz.

		longitude = radian,
		latitude = radian,
		altitude = meters,

		-- Infor de rotation optionnelle

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Echelle optionnelle

		scale = nombre
	}

Dessinez le modèle 3D donné (à partir d'un précédent appel à **UI.Renderer.CreateVertexArray**) en utilisant l'état donné (à partir d'un précédent appel à **UI.Renderer.CreateRenderState**) à l'emplacement/la rotation/l'échelle donné(e) dans la vue 3D.

Les tableaux state et vertex doivent être créés uniquement UNE FOIS.

NE re-déclarez PAS l'état et/ou le tableau de vertex à chaque appel de dessin, cela entraînerait une fuite des ressources.


#### UI.Renderer.DrawUIVertexArray( transform , renderStateHandle , vertexArrayHandle )
*Tacview 1.7.2*
#### UI.Renderer.DrawUIVertexArray( transform , renderStateHandle , vertexArrayHandle [, textureCoordinateArrayHandle] )
*Tacview 1.7.3*

**renderStateHandle** est un entier précédemment renvoyé par **UI.Renderer.CreateRenderState()**

**vertexArrayHandle** est un entier précédemment renvoyé par **UI.Renderer.CreateVertexArray()**

**textureCoordinateArrayHandle** est un entier optionnel précédemment renvoyé par **UI.Renderer.CreateTextureCoordinateArray()**

	transform =
	{
		-- Coordonnées d'écran obligatoires

		x = nombre,
		y = nombre,
		z = nombre,				-- 0 par défaut

		-- Orientation optionnelle

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Echelle uniforme optionnelle

		scale = number

		-- Echelle non uniforme optionnelle
		-- Tacview 1.8.0

		scaleX = number
		scaleY = number
	}

Lors du passage de l'interface utilisateur, les coordonnées 2D sont comme en suivant :

	UI.Renderer.GetHeight()

	    ^
	    |transform.Y
	    |
	    |
	    |      transform.x
	    +------------------> UI.Renderer.GetWidth()
	   0,0

Dessine le modèle 2D / 3D donné (à partir d'un précédent appel à **UI.Renderer.CreateVertexArray**) en utilisant l'état donné (à partir d'un précédent appel à **UI.Renderer.CreateRenderState()**) à la position donnée/rotation/échelle par dessus la vue 3D.

Les tableaux state et vertex doivent être créés uniquement UNE FOIS.

NE re-déclarez PAS l'état et/ou le tableau de vertex à chaque appel de dessin, cela entraînerait une fuite des ressources.


#### UI.Renderer.DrawOpaqueObject( objectHandle , transform [, alpha ] )
*Tacview 1.7.2*
#### UI.Renderer.DrawTransparentObject( objectHandle , transform [, alpha ] )
*Tacview 1.7.2*

Fonction de haut niveau pour dessiner les parties opaques ou transparentes de l'objet de télémétrie correspondant dans la vue 3D.

Ces fonctions utiliseront automatiquement la forme et la couleur de l'objet actuel pour afficher correctement le modèle 3D dans la vue 3D.

**UI.Renderer.DrawOpaqueObject()** est généralement appelé dans les rappels **Events.DrawOpaqueObjects** pour dessiner le corps de l'objet principal.

**UI.Renderer.DrawTransparentObject ()** est généralement appelé dans les rappels **Events.DrawTransparentObjects** pour dessiner les parties transparentes restantes des objets (par exemple, les aptitudes correctes).

	transform =
	{
		-- Si la position sphérique n'est pas fournie, Tacview utilisera la position cartésienne xyz dans l'espace global terrestre

		x = nombre,
		y = nombre,
		z = nombre,

		-- La position sphérique sera utilisée en priorité pour rendre l'objet

		longitude = radian,
		latitude = radian,
		altitude = meters,

		-- Info de rotation optionnelle

		roll = radian,
		pitch = radian,
		yaw = radian,

		-- Echelle optionnelle

		scale = nombre
	}

	Vous pouvez redimensionner l'objet ou définir l'échelle sur -1 pour une mise à l'échelle automatique (en fonction des paramètres utilisateur)

	Vous pouvez forcer la transparence de l'objet ou définir alpha sur -1 pour le mode automatique (selon le statut mort/vivant)


#### UI.Renderer.Print( transform , renderStateHandle , text )
*Tacview 1.7.3*

Imprimer le texte donné aux coordonnées x, y correspondantes.

Devrait être utilisé uniquement lors d'opérations d'interface utilisateur transparente en 2D.

Vous pouvez définir **renderState.blendMode** sur **Tacview.UI.Renderer.BlendMode.Additive** pour afficher le texte de style HUD.

	transform =
	{
		-- Si la position cartésienne xyz dans l'espace global terrestre n'est pas fournie, elle sera calculée en fonction de la position sphérique (longitude, latitude, altitude).

		x = nombre,
		y = nombre,

		-- Echelle optionnelle

		scale = nombre
	}


#### UI.Renderer.ContextMenu.RegisterListener( function )
*Tacview 1.7.6*

Utilisez cette fonction pour enregistrer un rappel et ajouter des options au menu contextuel que Tacview affichera par clic droit dans la vue 3D.

Juste avant d'afficher le menu contextuel de la vue 3D, Tacview appellera la fonction suivante pour vous permettre d'ajouter une option personnalisée :

		function( contextMenuId , objectHandle )

		-- **contextMenuId** (entier) : Id du menu contextuel dans lequel vous pouvez ajouter des options.
		-- **objectHandle** (entier) : objet associé au menu contextuel (0 si aucun objet n'est lié au menu)

Utilisez les fonctions **UI.Menus** avec **parentMenuId** défini sur **contextMenuID** pour ajouter vos propres options au menu contextuel en fonction de l'objet sélectionné.

Le menu contextuel est volatile et sera automatiquement détruit dès sa fermeture par l'utilisateur.

Chaque fois que votre rappel est appelé, vos options seront ajoutées à un tout nouveau menu.
