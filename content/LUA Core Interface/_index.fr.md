+++
title = "LUA Core Interface"
date = 2019-04-13T18:16:05+02:00
weight = 5
chapter = true
pre = "<b>1. </b>"
+++

---

#	Tacview 1.7.6 Lua Core Interface
##	Dernière mise à jour : 18-04-2019

---

Tacview charge automatiquement tout script Lua intitulé "main.lua" trouvé dans le sous-dossier immédiatement sous :

	C:\Program Files (x86)\Tacview\AddOns\
	%ProgramData%\Tacview\AddOns\
	%APPDATA%\Tacview\AddOns\

Vous pouvez par exemple enregistrer le script principal de votre addon comme :

	%ProgramData%\Tacview\AddOns\Mon add-on\main.lua

Au début de votre script vous retrouverez typiquement l'interface lua pour laquelle le add-on a été programmé :

	Tacview = require("Tacview176")			-- Request Tacview 1.7.6 API

Ensuite vous pouvez accéder à n'importe quelle méthode du SDK comme dans l'exemple suivant :

	Tacview.Log.Info("Successfully exported ", objectCount, " object(s)")

Selon le contexte dans lequel votre script est exécuté, vous aurez accès à des interfaces légèrement différentes.
Votre script **main.lua** sera exécuté dans le contexte principal. Il accèdera à toutes les fonctionnalités de Tacview hormis les interfaces d'export et import.

Tandis que vos scripts import et export accèderont aux fonctionnalités coeurs comme respectivement aux interfaces d'import ou export.

Afin d'éviter des problèmes liés au multithreading ou bien des erreurs se répercutant sur les autres add-ons, chaque add-on Lua est chargé dans sa propre machine virtuelle.
