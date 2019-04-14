---
title: "Log"
date: 2019-04-13T18:16:51+02:00
draft: false
---


Le module log est typiquement utilisé pour afficher des messages et erreurs pouvant être utiles au diagnostique d'un problème particulier.

Tous les caractères envoyés au log sont également sauvegardés dans le fichier `%TEMP%\Tacview.log`.

S'il vous plait, utilisez le log avec sagesse et essayez de n'afficher que des messages ayant un sens pour l'utilisateur final.

Ne spammez pas le log avec des messages de développement internes, cela peut amener de la confusion pour l'utilisateur cherchant des informations plus pertinentes provenant des autres modules.


#### Log.Debug(...)
*Tacview 1.7.2*

Utilisez cette méthode pour vous aider à tracer et diagnostiquer des problèmes avec votre addon.

{{% notice tip %}}
**NOTE :** Les informations debug ne sont affichées que lorsque l'argument `/Debug:On` est utilisé en ligne de commande pour le lancement de Tacview.
{{% /notice %}}


#### Log.Info(...)
*Tacview 1.7.2*

Cette méthode peut être utilisée pour afficher une information spécifique sur votre addon pouvant être utile à l'utilisateur final.

{{% notice tip %}}
**NOTE :** la fonction Lua *print()* est redirigée sur *Log.Info()*.
{{% /notice %}}


#### Log.Warning(...)
*Tacview 1.7.2*

Les warnings peuvent être utilisés pour informer l'utilisateur de circonstances non usuelles comme des erreurs non critiques dans les données d'entrée.
Les warnings seront surlignés dans la console Tacview pour attirer l'attention de l'utilisateur.


#### Log.Error(...)
*Tacview 1.7.2*

Les messages d'erreur sont typiquement utilisés pour afficher les erreurs critiques qui habituellement empêchent la poursuite des opérations.
