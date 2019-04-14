# C’est le moment de mettre la main sur le tout nouveau SDK en Lua !

La version 1.7.2 est un grand pas en avant pour la communauté : J’ai enfin terminé l’intégration du langage **Lua 5.3.4**. Créez vos propres addons a l’aide de l’interface de programmation dédiée. Pour étendre les fonctionnalités existantes ou en développer des nouvelles !

Pour créer un addon il suffit de :

* Créer un dossier portant le nom de votre addon dans C:\ProgramData\Tacview\AddOns\
* Créer un fichier nommé "main.lua" dans ce dossier (il sera automatiquement chargé au démarrage de Tacview). Cela devrait ressembler à `C:\ProgramData\Tacview\AddOns\My Addon\main.lua`
* Référencer la toute dernière API de Tacview a l’aide d’un simple : `local Tacview = require("Tacview172")`
* Il ne reste plus qu’à utiliser les nombreuses fonctionnalités documentées dans `C:\Program Files (x86)\Tacview\AddOns\Tacview Lua * Interface.txt`
* Vous pouvez même utiliser **LuaSocket 3.0** qui a été intégré dans Tacview est qui est prêt à remplir tous vos besoins en termes de connectivité ! Il suffit de l’habituel code : `socket = require("socket")`

Il s’agit de la première itération, et bien que l’API actuelle soit relativement limitée, ses fonctionnalités vont s’étoffer rapidement au fil des mises a jours et en fonction de vos requêtes. Faites-moi simplement savoir de quoi vous avez besoin, et je ferais de mon mieux pour ajouter de nouvelles fonctions afin que vous puissiez développer l’addon de vos rêves.

Vous trouverez plusieurs exemples en Lua dans `C:\Program Files (x86)\Tacview\AddOns\`

Le plus notable étant « Landing Signal Officer » (officier d’appontage), actuellement en développement, qui affichera bientôt une camera LSO lorsque l’on passe en vue cockpit sur un porte avion. Prochainement, il calculera automatiquement les scores de tentatives d’atterrissage.

Voyez les la liste des changements ci-dessous pour plus de détail sur les nombreuses améliorations et corrections.

![Landing Signal Officer AddOn](https://www.tacview.net/rss/Tacview-Lua-SDK.png)
