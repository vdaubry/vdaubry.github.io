---
layout:     post
title:      "Setup up a jekyll blog using github pages and disqus comments"
subtitle:   "An easy way to get a good looking blog"
description: "Learn how to setup a full jekyll blog, hosted on github pages, including a custom theme and Disqus comments"
date:       2014-10-19
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* <a href="{{site.url}}/2014/10/19/setup-a-jekyll-blog/">Part 1: Setup up a jekyll blog using github pages and disqus comments</a>
* <a href="{{site.url}}/2014/10/20/add-sharing-links-to-jekyll-blog/">Part 2: Add sharing links to a jekyll blog</a>
* <a href="{{site.url}}/2014/10/21/2014/10/21/SEO-for-your-Jekyll-blog/">Part 3: SEO for your Jekyll blog</a>

###Part 1: Setup a personal blog with Jekyll

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

The default template is not great in terms of design. If you go to <a href="http://jekyllthemes.org/">jekyllthemes.org</a>, you can find nicer templates. For this blog I used <a href="https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll">clean-blog</a>. To start your blog just fork the repo.

It's a good idea to customize the images, a very easy way to do that is choose a HD photo in creative common license. You can use <a href="http://www.sitebuilderreport.com/stock-up">stock-up</a> for that.

You are going to display white text over the image, in order to increase readability it's better to darken the image. You can do that with the mac preview app by changing the "exposure" :

<img src="/img//posts/2014-11-19-setup-a-jekyll-blog/exposure.jpg" width="800">


To preview your modification locally, you must install Jekyll, the doc <a href="http://jekyllrb.com/docs/installation/">here</a> but basically it's as complex as :

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

See any way to improve this setup ? share your thoughts in comments

Le code de ce blog est accessible ici : <a href="vdaubry.github.io">vdaubry.github.io</a>