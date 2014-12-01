---
layout:     post
title:      "Add sharing links to a jekyll blog"
subtitle:   "Share your blog post on Facebook, Twitter and Google+"
description: "Learn how to add sharing links on Facebook, Twitter and Google+"
date:       2014-10-20
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* <a href="{{site.url}}/2014/10/19/setup-a-jekyll-blog/">Part 1: Setup up a jekyll blog using github pages and disqus comments</a>
* <a href="{{site.url}}/2014/10/20/add-sharing-links-to-jekyll-blog/">Part 2: Add sharing links to a jekyll blog</a>
* <a href="{{site.url}}/2014/10/21/2014/10/21/SEO-for-your-Jekyll-blog/">Part 3: SEO for your Jekyll blog</a>

###Part 2: Add links to share on twitter, facebook and google +

To add sharing links on your posts, the procedure is extremely simple for twitter and google +, just paste the provided code on your page :

* Twitter: To add a link to twitter sharing, visit <a href="https://about.twitter.com/resources/buttons#tweet">this page</a>
* Google +: To add a link sharing twitter, visit <a href="https://developers.google.com/+/web/share/">this page</a>

For Facebook c'est plus galère : il est nécessaire de créer une application, pour cela rendez vous sur la page <a href="https://developers.facebook.com/">facebook developer</a>

Puis rendez vous sur <a href="https://developers.facebook.com/docs/plugins/share-button/">la page du bouton partage</a> pour obtenir le code à ajouter sur votre page

Facebook inject le style pour son bouton via du javascript. Cela peut provoquer un décalage d'alignement vertical avec les autres boutons :

<img src="/img/posts/2014-11-19-setup-a-jekyll-blog/facebook-bug.png" height="90">

Dans mon cas j'ai résolu le problème avec un gros bout de sparadrap :

{% highlight html %}
<div class="fb-share-button" data-href="{{site.url}}{{page.url}}" data-layout="button_count" style="position: relative; top: -8px; left: 33px;"></div>
{% endhighlight %}

Les developper front end doivent avoir les yeux qui brulent en lisant ça. Si vous avez une solution plus clean les commentaires sont là pour ça.

Attention: Le code fournit par facebook référence la page facebook du bouton partage (non vous n'avez pas 1 million de partage sur votre article de blog).
Vous pouvez utiliser les <a href="http://jekyllrb.com/docs/variables/">variables Jekyll</a> pour obtenir l'url de la page courrante :

```
{{site.url}}{{page.url}}
```


###Ajouter des meta pour google, facebook and twitter

Les moteurs de recherches et les réseaux sociaux crawl voter page et l'index ses metadats, dans le cas de google cela participe au calcul de votre <a href="http://en.wikipedia.org/wiki/PageRank">pagerank</a>, dans le cas de Facebook (meta og) et Twitter (twitter cards) cela permet d'enrichir l'affichage de votre page dans les partages et les tweets.

Le sujet est vaste et je vous recommende cet excellent article sur l'état de l'art des meta en 2013 : <a href="http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013">18 Meta Tags Every Webpage Should Have in 2013</a>

Nous allons simplement voir dans cet article comment ajouter ces meta dans la balise head de toutes les pages de jekyll.



####Metadatas Facebook OpenGraph :


Partager un lien sur Facebook consiste à référencer sur sa timeline un objet de <a href="http://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol">l'open graph de facebook</a>

Facebook crawl le web et ajoute chaque page en tant qu'objet de son graph. Par défaut le crawler va utiliser les informations dont il dispose comme le titre de votre page.

Vous pouvez améliorer le référencement de votre page dans l'open graph en fournissant au crawler les informations dont il a besoin :

* titre du site
* titre du post
* url nettoyée (utilisé comme identifiant unique)
* description
* image (thumbnail)
* Facebook app id
* type
* language
* author

Vous devez ajouter ces tags dans la balise ```<head>``` de chaque page du site, il faut donc prévoir le cas des pages qui sont des posts et le cas des autres pages du site (homepage, about, etc)

Pour celà vous pouvez ajouter un code de type dans votre include ```head.html``` :

{% gist 69f089affeff3b6ca627 %}

N'oubliez pas de vérifier la bonne intégration des metadatas open graph sur le <a href="https://developers.facebook.com/tools/debug/og/object/">debugger facebook</a>

Si vous souhaitez une liste des attributs de l'open graph vous pouvez lire la doc <a href="http://ogp.me/">ici</a>


####Metadatas Twitter cards :

Le concept est similaire pour Twitter, pour afficher un appercu d'un lien dans un tweet vous pouvez fournir au crawler de Twitter des informations sur votre page :

* card : Texte, image, ou player (ex: video)
* url
* titre
* description
* image


Voilà un exemple de code que vous pouvez ajouter dans votre include ```head.html``` pour générer les metadatas Twitter cards :

{% gist d404f792a87699c665e2 %}

Comme pour Facebook pensez à valider l'intégration des metadatas Twitter cards via le <a href="https://cards-dev.twitter.com/validator">Card validator</a>

Pour que twitter affichent les images fournit il faut que votre domaine soit validé par Twitter. Pour celà rendez vous sur le <a href="https://cards-dev.twitter.com/validator">Card validator</a> et cliquez sur "request approval".

Pour ce blog la validation a été faite quelques minutes après avoir fait la demande.

Voyez vous des améliorations à apportés, avez vous procédé différement ? si c'est le cas laissez un commentaire.

Le code de ce blog est accessible ici : <a href="vdaubry.github.io">vdaubry.github.io</a>