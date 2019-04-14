---
title: "UI"
date: 2019-04-13T18:16:46+02:00
draft: false
---

Fonctions générales pour manipuler l'interface utilisateur et l'aspect de Tacview.

#### UI.EnterFullScreen()
*Tacview 1.7.2*
#### UI.ExitFullScreen()
*Tacview 1.7.2*

Entrer/quitter le mode plein écran.

En mode plein écran, Tacview affiche uniquement la vue 3D dans une fenêtre sans bordure.

Cela peut être utile lors d'un débriefing en ligne, afin que l'utilisateur puisse se concentrer pleinement sur les objets affichés dans la vue 3D.

L'utilisateur peut basculer manuellement entre le mode plein écran et le mode fenêtré en appuyant sur [ALT] + [ENTER].

Il est également possible de quitter le mode plein écran en appuyant sur [Esc].


#### UI.EnterReadMode( [borderless] )
*Tacview 1.7.2*
#### UI.ExitReadMode()
*Tacview 1.7.2*

Entrer/sortir du mode lecture.

En mode lecture, Tacview affiche uniquement la vue 3D (les outils et les menus sont masqués).

**borderless** est un paramètre booléen facultatif qui peut être défini sur true si vous souhaitez également masquer la bordure de la fenêtre Tacview.

Cette fonction consiste principalement à intégrer la fenêtre Tacview dans une autre application lorsqu'elle est associée à **UI.SetWindowParent()**.


#### UI.SetWindowParent( parentWindowhandle )
*Tacview 1.7.2*

Attachez la fenêtre principale de Tacview à une autre fenêtre d'application.

Généralement utilisé avec **UI.EnterReadMode(true)** et **UI.SetWindowPosition()** pour afficher Tacview dans une autre application.

Appelez **SetWindowParent(nil)** pour détacher la fenêtre principale de Tacview de votre application.


#### UI.SetWindowPosition( x , y [, width , height] )
*Tacview 1.7.2*

Modifiez la position et la taille de la fenêtre principale de Tacview lorsque **width** et **height** sont fournies.
La position est spécifiée pour le coin supérieur/gauche de la fenêtre sur le bureau ou dans la fenêtre parente.


#### UI.SetWindowSize( width , height )
*Tacview 1.7.2*

Change la taille de la fenêtre principale de Tacview.

**width** et **height** doievent être > 0.


#### UI.GetWindowHandle()
*Tacview 1.7.5*

Renvoie le handle de la fenêtre principale de Tacview.

Vous pouvez utiliser cette fonction pour créer des fenêtres enfants ou des boîtes de dialogue pour votre addon.

N'UTILISEZ PAS cette fonction pour modifier manuellement la taille, la position ou le parent de la fenêtre de Tacview. Dans ce cas, utilisez les fonctions dédiées, qui font plus que simplement appeler le système d'exploitation.

{{% notice note %}}
**Valeur retournée :**<br>
		handle de la fenêtre principale de Tacview.<br>
		Ce handle peut être **nil** si Tacview est exécuté en mode silent en ligne de commande.
{{% /notice %}}
