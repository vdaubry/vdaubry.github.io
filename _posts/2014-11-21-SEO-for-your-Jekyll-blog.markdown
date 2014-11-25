---
layout:     post
title:      "SEO for your Jekyll blog"
subtitle:   "Take care of search engine optimization for your blog"
description: "Learn how to optimize your Jekyll blog posts for search engines"
date:       2014-10-21
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* <a href="{{site.url}}/2014/10/19/setup-a-jekyll-blog/">Part 1: Setup up a jekyll blog using github pages and disqus comments</a>
* <a href="{{site.url}}/2014/10/20/add-sharing-links-to-jekyll-blog/">Part 2: Add sharing links to a jekyll blog</a>
* <a href="{{site.url}}/2014/10/21/2014/10/21/SEO-for-your-Jekyll-blog/">Part 3: SEO for your Jekyll blog</a>

###Part 3: SEO

Je ne suis pas expert SEO et ce n'est pas le sujet de cet article, cela étant dit il y a t'il des choses simple que l'on peut faire pour améliorer le référencement de ce blog ?

Voilà la liste des modifications que j'ai apporté au template clean blog :

1) Ne pas inclure systématiquement le nom du blog dans la balise title

source : <a href="http://sixrevisions.com/content-strategy/5-common-seo-mistakes-with-web-page-titles/)">5 Common SEO Mistakes with Web Page Titles</a>

Avant :

{% highlight html %}
{% raw %}
<title>{% if page.title %}{{ page.title }} - {{ site.title }}{% else %}{{ site.title }}{% endif %}</title>
{% endraw %}
{% endhighlight %}

Après :
{% highlight html %}
{% raw %}
<title>{% if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}</title>
{% endraw %}
{% endhighlight %}


2) Utiliser une meta description spécifique pour chaque page du blog

source : <a href="http://moz.com/learn/seo/meta-description">Meta Description Tag - Learn SEO</a>

Avant :

{% highlight html %}
{% raw %}
<meta name="description" content="{{ site.description }}">
{% endraw %}
{% endhighlight %}

Après :
{% highlight html %}
{% raw %}
<meta name="description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
{% endraw %}
{% endhighlight %}


3) Utiliser la meta rel=author pour chaque page du blog

source: <a href="http://www.vervesearch.com/blog/how-to-implement-the-relauthor-tag-a-step-by-step-guide/">How to Implement the Rel=”Author” Tag – A Step by Step Guide</a>

{% highlight html %}
<link rel="author" href="https://plus.google.com/+vincentdaubry"/>
{% endhighlight %}

Voyez vous d'autres améliorations que l'on peut apporter au référencement d'un blog Jekyll ?


Le code de ce blog est accessible ici : <a href="vdaubry.github.io">vdaubry.github.io</a>