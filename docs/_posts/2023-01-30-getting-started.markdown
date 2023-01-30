---
layout: post
title:  "Démarrer le projet localement"
date:   2023-01-30 05:09:59 -0600
categories: welcome
---

Il existe des images Docker préparées pour GitHub Pages. Vous pouvez utiliser l'[**image officielle Jekyll**](https://github.com/envygeeks/jekyll-docker) disponible sur Docker Hub pour exécuter votre site GitHub Pages.

Voici un exemple de commande docker run pour utiliser l'image Jekyll :
```
docker run --rm -v "/$PWD/docs":/srv/jekyll -p 4000:4000 jekyll/jekyll:4.2.0 sh -c "bundle install && bundle exec jekyll serve --host=0.0.0.0"
```

Cette commande monte le répertoire actuel (`"/$PWD"` sur windows et `$(pwd)` pour le reste) sur le chemin `/srv/jekyll` dans le conteneur (répertoire de travail de Jekyll), ce qui vous permet de travailler sur votre projet sur votre ordinateur local tout en exécutant des commandes dans le conteneur. Le paramètre `--rm` indique à Docker de supprimer le conteneur une fois que vous arrêtez le serveur Jekyll.

Vous pouvez maintenant accéder au serveur Jekyll en utilisant un navigateur Web et en entrant l'adresse [http://localhost:4000](http://localhost:4000) dans la barre d'adresse. Si vous exécutez Docker sur une machine distante (par exemple, un serveur), utilisez l'adresse IP de la machine et le port 4000 pour accéder au serveur, par exemple `http://<server_ip>:4000`.

Pour entrer en mode interactif dans un conteneur Docker, vous pouvez utiliser la commande docker run avec l'option -it :
```
docker run --rm -it -v "/$PWD/docs":/srv/jekyll -p 4000:4000 jekyll/jekyll:4.2.0 bash
```

Cela vous permettra par exemple de relancer le serveur après une modification. Une fois à l'intérieur, vous pouvez exécuter vos commandes (ex. installe les composants et démarre le serveur):
```
bundle install
bundle exec jekyll serve --host=0.0.0.0
```

Une fois que vous avez terminé, vous pouvez sortir du conteneur en utilisant la commande exit.
