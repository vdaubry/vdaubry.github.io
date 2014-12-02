---
layout:     post
title:      "Add social sharing buttons into Jekyll"
subtitle:   "Share your blog post on Facebook, Twitter and Google+"
description: "Learn how to add sharing links on Facebook, Twitter and Google+"
date:       2014-10-20
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* <a href="{{site.url}}/2014/10/19/setup-a-jekyll-blog/">Part 1: Setup up a jekyll blog using github pages and disqus comments</a>
* <a href="{{site.url}}/2014/10/20/add-sharing-links-to-jekyll-blog/">Part 2: Add social sharing buttons into Jekyll</a>
* <a href="{{site.url}}/2014/10/21/2014/10/21/SEO-for-your-Jekyll-blog/">Part 3: SEO for your Jekyll blog</a>

###Part 2: Add links to share on twitter, facebook and google +

Adding sharing buttons to your posts is extremely simple for twitter and google +, just paste the provided code on your page :

* Twitter: <a href="https://about.twitter.com/resources/buttons#tweet">this page</a>
* Google +: <a href="https://developers.google.com/+/web/share/">this page</a>

Facebook is a bigger hassle:
First you need to create an application on this page <a href="https://developers.facebook.com/">facebook developer</a>
Then get code on the <a href="https://developers.facebook.com/docs/plugins/share-button/">sharing button page</a>

And of course it doesnt work out of the box :
Contrary to Twitter and and Google+, the injected code doesn't auto-discover your current page url. It's a static link, and the sample code include a link to the developper page itself (no, you do not have 1 million shares on your blog article already).

You need to use a <a href="http://jekyllrb.com/docs/variables/">Jekyll variable</a> to get the URL of the current page:

```
<div class="fb-share-button" data-href="{{site.url}}{{page.url}}" data-layout="button_count" style="position: relative; top: -8px; left: 33px;"></div>
```

Facebook also injects style via javascript, this can cause a vertical alignment offset with other buttons:

<img src="/img/posts/2014-11-19-setup-a-jekyll-blog/facebook-bug.png" height="90">


###Add meta for google, facebook and twitter :

Search engines and social networks crawl your page and index its metadatas. Google uses it to calculate your <a href="http://en.wikipedia.org/wiki/PageRank">pagerank</a>, Facebook (meta og) and Twitter (twitter cards) use them to enrich the way your page is displayed in shares and tweets.

Web page metadata is a vast subject, I recommend you to read this excellent article on the state of the art of meta in 2013: <a href="http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013">18 Meta Tags Every Webpage Should Have in 2013</a>


####Metadatas Facebook OpenGraph :

Shares on Facebook are reference to an object of the <a href="http://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol">open graph.</a>
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

You can check the result using the open graph <a href="https://developers.facebook.com/tools/debug/og/object/">facebook debugger</a>

The open graph attributes are described in <a href="http://ogp.me/">this doc</a>


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

Twitter also provides a tool to validate your metadatas : <a href="https://cards-dev.twitter.com/validator">Card validator</a>r

Twitter will only display images from your domain if it has been previously validated. To get your blog validated, go on the <a href="https://cards-dev.twitter.com/validator">Card validator</a> tool and click on "request approval".

Validation for this blog took only a few minutes.

Thats it ! People can now share a link to your post on social networks.

Do you see room for improvement, have you done something differently? if so leave a comment.

Code for this blog can be found here : <a href="vdaubry.github.io">vdaubry.github.io</a>