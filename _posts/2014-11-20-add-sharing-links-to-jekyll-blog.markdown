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

Facebook is a bigger hassle:
First you need to create an application, on this page <a href="https://developers.facebook.com/">facebook developer</a>
Then get code on the <a href="https://developers.facebook.com/docs/plugins/share-button/">sharing button page</a>

And of course it doesnt work out of the box :
Facebook inject style for its button via javascript. This can cause a vertical alignment offset with other buttons:

<img src="/img/posts/2014-11-19-setup-a-jekyll-blog/facebook-bug.png" height="90">

In my case I solved the problem with a dirty hack :

{% highlight html %}
<div class="fb-share-button" data-href="{{site.url}}{{page.url}}" data-layout="button_count" style="position: relative; top: -8px; left: 33px;"></div>
{% endhighlight %}

Warning: The code provided by the facebook is not customised for your app (no, you do not have 1 million shares on your blog article).
You can use the <a href="http://jekyllrb.com/docs/variables/">Jekyll variables</a> to get the URL of the current page:

```
{{site.url}}{{page.url}}
```


###Add meta for google, facebook and twitter :

Search engines and social networks crawl your page and index its metadatas. Google uses it to calculate your <a href="http://en.wikipedia.org/wiki/PageRank">pagerank</a>, Facebook (meta og) and Twitter (twitter cards) use them to enrich the way your page is displayed in shares and tweets.

Web page metadata is a vast subject, I recommend you to read this excellent article on the state of the art of meta in 2013: <a href="http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013">18 Meta Tags Every Webpage Should Have in 2013</a>


In this article we'll only see how to add the meta tag in the head of every page of Jekyll.


####Metadatas Facebook OpenGraph :

Shares on Facebook are reference to an object of the <a href="http://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol">open graph.</a>
Facebook crawls the web and adds each page as an object of the graph. By default, the crawler will try to guess informations about your page such as the title, a thumbnail (by making a screenshot), etc.

You can improve the way your page is displayed in shares by providing metadatas about  your page :

* titre du site
* titre du post
* url nettoyée (utilisé comme identifiant unique)
* description
* image (thumbnail)
* Facebook app id
* type
* language
* author

You must add these tags in the ```<head>``` tag of each page.
In a Jekyll blog there will be 2 kind of pages :

Posts with informations about the article
Other pages with informations about the blog itself (homepage, about, etc)

To to so you can add a code type in your ```head.html``` include:

{% gist 69f089affeff3b6ca627 %}

Do not forget to check the proper integration of metadatas using the open graph <a href="https://developers.facebook.com/tools/debug/og/object/">facebook debugger</a>

The open graph attributes are described in <a href="http://ogp.me/">this doc</a>


####Metadatas Twitter cards :

Twitter cards are similar to Facebook meta-og. When a tweet contains a link to your page, the Twitter crawler will gather informations about the page to entich the tweet (display a preview, etc)
Here are some informations you can provide :

* card : Texte, image, ou player (ex: video)
* url
* titre
* description
* image

Here is a sample code that you can include in your ```head.html``` to generate the metadata Twitter cards:


{% gist d404f792a87699c665e2 %}

Dont forget to validate the metadata via Twitter <a href="https://cards-dev.twitter.com/validator">Card validator</a>r

Twitter will only display images from your domain if it has been previously validated by Twitter. To do this go on the <a href="https://cards-dev.twitter.com/validator">Card validator</a> tool and click on "request approval".

Validation for this blog was made a few minutes after the application.

Thats it ! People can now share a link to your post on social networks.

Voyez vous des améliorations à apportés, avez vous procédé différement Do you see room for improvement, have you done something differently? if so leave a comment.

Code for this blog can be found here : <a href="vdaubry.github.io">vdaubry.github.io</a>