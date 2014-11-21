---
layout:     post
title:      "Setup up a jekyll blog"
subtitle:   "An easy way to get a good looking blog using jekyll and github pages"
date:       2014-10-19
author:     "Vincent Daubry"
header-img: "img/post-bg-02.jpg"
---

###Setup a personal blog with Jekyll

TL;DR :

Are you a developer? You want to start a personal blog? Want to keep it simple and have a nice visual result? In this article we will see how to set up a blog with <a href="http://jekyllrb.com/">jekyll</a>, using a nice theme, and host it on <a href="https://pages.github.com/">github pages</a>


This is the first article of my blog and to start with a dizzying perspective, we'll see how I set up this blog. This blog gives you an immediate idea of the final result , so if you don't like it, you can skip this article.

###Why a static site generator?

There are several reasons to choose a static site generator instead of a CMS like wordpress. In this article we will focus on the simplicity provided by a static website generator :

* Quick start (if you know html markdown and you should be fine)
* Very little configuration
* Ease of deployment, there is no app server. A simple apache will do.
* Ability to host directly on Github thanks to <a href="https://pages.github.com/">github pages</a>

The list of solutions is <a href="https://staticsitegenerators.net">impressive</a>, so why Jekyll?

* Right now Jekyll is one of the most popular static website generator (<a href="https://www.staticgen.com/">source</a>)
* Used by Github (written by Tom Preston-Werner, founder of Github)
* The Ruby ecosystem


###Choose a blog theme for Jekyll :

The default template is not great in terms of design. If you go to <a href="http://jekyllthemes.org/">jekyllthemes.org</a>, you can find nicer templates. For this blog I used <a href="https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll">clean-blog</a>

To start your blog just fork the repo. To preview your modification locally, you must install Jekyll, the doc <a href="http://jekyllrb.com/docs/installation/">here</a> but basically it's as complex as :

```gem install jekyll```

To start the jekyll server and add post, just follow the <a href="http://jekyllrb.com/docs/usage/">getting started</a>


###Deploy your Jekyll blog

Generate the static version of your blog:

```jekyll build ```

You can then deploy this static site as you want:

* On your remote server
* Drop it on a S3 bucket (using S3 static website for example)
etc

Or you can also use the hosting service github pages. just create a repo using the following convention for the name of the repo:

```
your_github_username.github.io
```

Everytime you push the master branch Github will automagically build a static version of your site and deploy it.


###Add comments to your blog Jekyll with Disqus

To add a comments feature with Disqus, it's just as simple:

* Create an account on <a href="https://disqus.com">Disqus</a>
* Choose integration via "universal code"
* Copy the code provided in the layout of the post (_layout / post.hmtl)

That's it.


###Add links to share on twitter, facebook and google +

To add sharing links on your posts, the procedure is extremely simple for twitter and google +, just paste the provided code on your page :

* Twitter: To add a link to twitter sharing, visit <a href="https://about.twitter.com/resources/buttons#tweet">this page</a>
* Google +: To add a link sharing twitter, visit <a href="https://developers.google.com/+/web/share/">this page</a>

For Facebook c'est plus galère : il est nécessaire de créer une application, pour cela rendez vous sur la page <a href="https://developers.facebook.com/">facebook developer</a>

Puis rendez vous sur <a href="https://developers.facebook.com/docs/plugins/share-button/">la page du bouton partage</a> pour obtenir le code à ajouter sur votre page

Facebook inject le style pour son bouton via du javascript. Cela peut provoquer un décalage d'alignement vertical avec les autres boutons :

<img src="/img/posts/2014-11-19-setup-a-jekyll-blog/facebook-bug.png" height="90">

Dans mon cas j'ai résolu le problème avec un gros bout de sparadra :

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

Metadatas Google :




Metadatas Facebook OpenGraph :


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




Metadatas Twitter cards :

Le concept est similaire pour Twitter, pour afficher un appercu d'un lien dans un tweet vous pouvez fournir au crawler de Twitter des informations sur votre page :

* card : Texte, image, ou player (ex: video)
* url
* titre
* description
* image


Voilà un exemple de code que vous pouvez ajouter dans votre include ```head.html``` pour générer les metadatas Twitter cards :

{% gist d404f792a87699c665e2 %}







###Ajouter google analytics





###SEO



Le code de ce blog est accessible ici : <a href="vdaubry.github.io">vdaubry.github.io</a>