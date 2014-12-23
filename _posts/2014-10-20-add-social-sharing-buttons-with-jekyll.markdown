---
layout:     post
title:      "Add social sharing buttons with Jekyll"
subtitle:   "Share your blog post on Facebook, Twitter and Google+"
description: "Learn how to add sharing links on Facebook, Twitter and Google+"
date:       2014-10-20
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* [Part 1: Setup up a jekyll blog using github pages and disqus comments]({{site.url}}/2014/10/19/setup-a-jekyll-blog/)
* [Part 2: Add social sharing buttons with Jekyll]({{site.url}}/2014/10/20/add-social-sharing-buttons-with-jekyll/)
* [Part 3: SEO for your Jekyll blog]({{site.url}}/2014/10/21/SEO-for-your-Jekyll-blog/)

###Part 2: Add links to share on twitter, facebook and google +

Adding sharing buttons to your posts is extremely simple for twitter and google+, just paste the provided code on your page :

* Twitter: visit <a href="https://about.twitter.com/resources/buttons#tweet">this page</a>
* Google+: visit <a href="https://developers.google.com/+/web/share/">this page</a>

Facebook is a bigger hassle:
First you need to create an application on this page [facebook developer]("https://developers.facebook.com/").
Then get the sample code on the [sharing button page]("https://developers.facebook.com/docs/plugins/share-button/")

And of course it doesnt work out of the box :

Contrary to Twitter and and Google+, the injected code doesn't auto-discover your current page url. It's a static link, and the sample code include a link to the developper page itself (no, you do not have 1 million shares on your blog article already).

You need to use a [Jekyll variable]("http://jekyllrb.com/docs/variables/") to get the URL of the current page:

{% gist df233106010970ddb237 %}

Facebook also injects style via javascript, this can cause a vertical alignment offset with other buttons:

<img src="/img/posts/2014-11-19-setup-a-jekyll-blog/facebook-bug.png" height="90">


###Add meta for google, facebook and twitter :

Search engines and social networks crawl your page and index its metadatas. Google uses it to calculate your [pagerank]("http://en.wikipedia.org/wiki/PageRank"), Facebook (meta og) and Twitter (twitter cards) use them to enrich the way your page is displayed in shares and tweets.

Web page metadatas is a vast subject, I recommend you to read this excellent article on the state of the art of meta in 2013: [18 Meta Tags Every Webpage Should Have in 2013]("http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013")


####Metadatas Facebook OpenGraph :

Shares on Facebook are objects of the [open graph]("http://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol")
By default, the crawler will gather informations about your page such as the title, a preview of your page, etc.

You can improve the way your page is displayed by providing metadatas about your page :

* Your website name
* Post title
* Clean url (used as a unique identifier for your object)
* Description
* Image (preview for the page)
* Facebook app id
* Type
* Language
* Author

You must add these tags in the ```<head>``` of each page.
On a Jekyll blog there will be 2 kind of pages :

* Posts with metadatas about the article
* Other pages with metadatas about the blog itself (homepage, about, etc)

Here is a sample code :

{% gist 69f089affeff3b6ca627 %}

You can check the result using the open graph [facebook debugger]("https://developers.facebook.com/tools/debug/og/object/")

The open graph attributes are described in [this doc]("http://ogp.me/")


####Metadatas Twitter cards :

Twitter cards are similar to Facebook meta-og. When a tweet contains a link to your page, the Twitter crawler will gather informations about the page to enrich the tweet (display a preview, etc)
Here are some informations you can provide :

* Card : Texte, image, ou player (ex: video)
* Url
* Title
* Description
* Image

Here is a sample code to generate Twitter cards metadatas :

{% gist d404f792a87699c665e2 %}

Twitter also provides a tool to validate your metadatas : [Card validator]("https://cards-dev.twitter.com/validator")

Twitter will only display images from your domain if it has been previously validated. To get your blog validated, go on the [Card validator]("https://cards-dev.twitter.com/validator") tool and click on "request approval".

Validation for this blog took only a few minutes.

Thats it ! People can now share a link to your post on social networks.

Do you see room for improvement, have you done something differently? if so leave a comment.

Code for this blog can be found here : [vdaubry.github.io]("vdaubry.github.io")