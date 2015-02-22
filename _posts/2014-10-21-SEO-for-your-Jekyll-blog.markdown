---
layout:     post
title:      "SEO for your Jekyll blog"
subtitle:   "Improve search engine optimization for your blog"
description: "Learn how to optimize your Jekyll blog posts for search engines"
date:       2014-10-21
author:     "Vincent Daubry"
header-img: "img/post-bg-07.jpg"
---

<i>This post is part of a series of articles on how to setup a Jekyll blog :</i>

* [Part 1: Setup up a jekyll blog using github pages and disqus comments]({{site.url}}/2014/10/19/setup-a-jekyll-blog/)
* [Part 2: Add social sharing buttons with Jekyll]({{site.url}}/2014/10/20/add-social-sharing-buttons-with-jekyll/)
* [Part 3: SEO for your Jekyll blog]({{site.url}}/2014/10/21/SEO-for-your-Jekyll-blog/)

###Part 3: SEO

There are some simple things you can do to improve the SEO of your blog, here is the list of changes I made to the clean blog template :

#### 1) Do not systematically include the blog name in the title tag

source : [5 Common SEO Mistakes with Web Page Titles](http://sixrevisions.com/content-strategy/5-common-seo-mistakes-with-web-page-titles/)

The clean blog template include the blog name in every post title, which is bad :

{% highlight html %}
{% raw %}
<title>{% if page.title %}{{ page.title }} - {{ site.title }}{% else %}{{ site.title }}{% endif %}</title>
{% endraw %}
{% endhighlight %}



#### 2) Use a specific meta description for each page of the blog

source : [Meta Description Tag - Learn SEO](http://moz.com/learn/seo/meta-description)

The clean blog template include the blog description on post page, you should use a specific description for each post :

{% highlight html %}
{% raw %}
<meta name="description" content="{{ site.description }}">
{% endraw %}
{% endhighlight %}


#### 3) Use the meta rel = author for each blog page

source: [How to Implement the Rel=”Author” Tag – A Step by Step Guide](http://www.vervesearch.com/blog/how-to-implement-the-relauthor-tag-a-step-by-step-guide/)

Link the page to your google+ profil :

{% highlight html %}
<link rel="author" href="https://plus.google.com/+vincentdaubry"/>
{% endhighlight %}


#### 4) Generate a sitemap for your blog

A [sitemap](https://support.google.com/webmasters/answer/156184?hl=en) provides search engine crawler informations about your website structure and pages it should index.

You can easily generate one by adding the ```jekyll-sitemap``` gem to your ```_config.xml```, just follow these [instructions](https://help.github.com/articles/sitemaps-for-github-pages/)

#### 5) Add a robots.txt file

A robots.txt file provides informations to crawlers about pages you want to exclude from indexing. You should also specify the path to your sitemap.

Add a similar file to the root of your project :

{% highlight html %}
{% raw %}
# www.robotstxt.org/
# www.google.com/support/webmasters/bin/answer.py?hl=en&answer=156449

User-agent: *
Sitemap: {{ site.url }}/sitemap.xml
{% endraw %}
{% endhighlight %}


That's it !
Do you see other improvements we can make to a Jekyll blog SEO ?

Code for this blog can be found here : [vdaubry.github.io](https://github.com/vdaubry/vdaubry.github.io)