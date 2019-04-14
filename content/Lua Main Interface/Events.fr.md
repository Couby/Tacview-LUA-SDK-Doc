---
title: "Evénements"
date: 2019-04-13T18:16:43+02:00
draft: false
---

Vous pouvez enregistrer des rappels pour différents types d’événements dans Tacview.


#### Events.Update.RegisterListener( function )
*Tacview 1.7.2*

Une fois par image, Tacview appellera votre fonction qui doit correspondre à la signature suivante :

Update(dt, absoluteTime)

- **dt** est le nombre de secondes écoulées dans la vie réelle depuis le dernier **Update()**
- **absoluteTime** est la durée actuelle de la télémesure en secondes **depuis le 01/01/1970** (ce paramètre est utile pour parler avec le module de télémétrie)


#### Events.DrawOpaqueObjects.RegisterListener( function )
*Tacview 1.7.2*
#### Events.DrawTransparentObjects.RegisterListener( function )
*Tacview 1.7.2*

Une fois par image, Tacview appellera votre fonction pour dessiner des objets 3D dans la vue 3D.

Il existe une passe pour les modèles 3D opaques et une passe pour les modèles transparents.

Voir **[UI.Renderer.DrawObjectVertexArray()](/lua-main-interface/ui.renderer/#ui-renderer-drawobjectvertexarray-transform-renderstatehandle-vertexarrayhandle-texturecoordinatearrayhandle)** et **[UI.Renderer.DrawOpaqueObject)()](/lua-main-interface/ui.renderer/#ui-renderer-drawtransparentobject-objecthandle-transform-alpha)** pour dessiner des objets dans le monde 3D.


#### Events.DrawOpaqueUI.RegisterListener( function )
*Tacview 1.7.2*
#### Events.DrawTransparentUI.RegisterListener( function )
*Tacview 1.7.2*

Une fois par image, Tacview appelle votre fonction pour dessiner une interface utilisateur de premier plan transparente 2D au-dessus de la vue 3D.

Votre fonction ne recevra aucun paramètre.

Voir **[UI.Renderer.DrawUIVertexArray()](/lua-main-interface/ui.renderer/#ui-renderer-drawuivertexarray-transform-renderstatehandle-vertexarrayhandle-texturecoordinatearrayhandle)** pour dessiner votre UI au-dessus de la vue 3D.
