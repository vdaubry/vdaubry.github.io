---
layout:     post
title:      "Setup up a jekyll blog"
subtitle:   "An easy way to get a good looking blog using jekyll and github pages"
date:       2014-10-19 12:00:00
author:     "Vincent Daubry"
header-img: "img/post-bg-02.jpg"
---

###Mettre en ligne un blog perso avec Jekyll

TL;DR :

Vous êtes développeur ? Vous avez envie de démarrer un blog perso ? Vous voulez faire simple et avoir un résultat sympa visuellement ?
Dans cet article nous allons voir comment mettre en place un blog avec <a href="http://jekyllrb.com/">jekyll</a>, utiliser un thème sympa, et héberger le tout sur <a href="https://pages.github.com/">github pages</a>


C'est le 1er article de mon blog et pour commencer par une vertigineuse mise en abime, on va voir comment j'ai mis en place ce blog. Ca vous donne tout de suite une idée du résultat finale, si ça ne vous convient pas vous pouvez passer votre chemin.


###Pourquoi un générateur de site statique ?

Il y a plusieurs raisons de choisir un générateur de site statique plutôt qu'un CMS du type wordpress. Dans cet article on va se concentrer sur la simplicité apportée par un générateur de site statique :

* Prise en main rapide (si vous connaissez markdown et html ça devrait aller)
* Très peu de configuration
* Facilité de déploiement, il n'y a pas de serveur d'app
* Possibilité d'héberger directement sur Github grace à <a href="https://pages.github.com/">github pages</a>

La liste des solutions est <a href="https://staticsitegenerators.net">impressionnante</a>, alors pourquoi Jekyll ?

* C'est un des plus répandu selon <a href="https://www.staticgen.com/">ce classement</a>
* Utilisé par Github (écrit par Tom Preston-Werner, fondateur de Github)
* L'écosystème Ruby


###Installer Jekyll à partir d'un thème

Le template par défaut de Jekyll est pas terrible en terme de design. Si vous allez sur <a href="http://jekyllthemes.org/">jekyllthemes.org</a>, vous trouverez des templates plus sympa. Pour ce blog je suis parti du thème <a href="https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll">clean-blog</a>

Pour démarrer votre blog vous pouvez simplement forker le repo. Pour pré-visualiser les article il faut installer Jekyll :

```gem install jekyll```


###Deployer votre blog Jekyll

Il suffit de générer la version statique de votre blog :

```jekyll build ```

Vous pouvez ensuite servir ce site statique comme vous voulez :

* Depuis votre serveur
* Depuis un bucket S3
etc

Vous pouvez également utiliser le service d'hébergement de github pages, pour ça il suffit de créer un repo en utilisant la convention suivante pour le nom du repo :

```
your_github_username.github.io
```

A chaque commit sur master Github va automagiquement builder une version statique de votre site et la déployer.


###Ajouter des commentaires à votre blog jekyll avec disqus

Pour ajouter la possibiliter de laisser des commentaires avec disqus, c'est tout aussi simple :

* Créer un compte sur <a href="https://disqus.com">disqus</a>
* Choisissez l'intégration via "universal code"
* Copier le code fournit dans le layout des post (```_layout/post.hmtl```)

C'est tout.


###Ajouter des liens de partage sur twitter, google+ et facebook

Pour ajouter des liens de partage sur vos posts, la procédure est extrèmement simple pour twitter et google+ , il suffit de coller le lien dans votre page

* Twitter : Pour ajouter un lien de partage twitter, rendez vous sur <a href="https://about.twitter.com/resources/buttons#tweet">cette page</a>
* Google + : Pour ajouter un lien de partage twitter, rendez vous sur <a href="https://developers.google.com/+/web/share/">cette page</a>

Pour facebook il est nécessaire de créer une application, pour cela rendez vous sur : https://developers.facebook.com/
Puis rendez vous sur la page du bouton partage pour obtenir le code à ajouter sur votre page : https://developers.facebook.com/docs/plugins/share-button/

Décalage de pixels bouton partage de facebook : ajouter : position: relative; top: -8px; left: 33px;


Ajouter google analytics

SEO



Le code de ce blog est accessible ici : <a href="vdaubry.github.io">vdaubry.github.io</a>