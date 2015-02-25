---
layout:     post
title:      "SEO for Rails"
subtitle:   ""
description: "Improve the search engine ranking of your Rails app"
date:       2015-02-23
author:     "Vincent Daubry"
header-img: "img/post-bg-02.jpg"
---

### SEO for Rails

My latest project is a web app to allow developpers to find what is their ranking on github : [Gitub awards](http://github-awards.com/). I looked for advices on how to improve SEO, one again, so I decided to gather a little check list here, to save some time next time. 
These search engine optimization advices won't be specific for a Rails app but i'll focus on the tools in ruby that are available to help.  

#### Step 1 : setup Google webmaster tools

It takes only minutes to add your website on google webmaster tools and you'll be able to see how many pages are indexed, check that your sitemap was found, etc.

Just go to : [google webmaster tools](https://www.google.com/webmasters/tools/home?hl=en)

And follow the instructions.


#### Step 2 : generate a sitemap

Generating a sitemap is as easy as generating a XML file, if you have a fairly simple sitemap you can do it just with [Nokogiri](http://www.nokogiri.org/). It would look like this :

{% highlight ruby %}

base_url = 'http://example.com'
sitemap = Nokogiri::XML::Builder.new do |xml|
  xml.urlset('xmlns' => 'http://www.sitemaps.org/schemas/sitemap/0.9') {
    your_objects.find_each do |obj|
      xml.url {
        xml.loc base_url + an_url
        xml.lastmod a_modification_date
        xml.changefreq "monthly"
        xml.priority "0.7"
      }
    end
  }
end.to_xml

{% endhighlight %}


If your sitemap is more complex (thousands of pages for example) you can use the [sitemap_generator](https://github.com/kjvarga/sitemap_generator) gem. You'll get some nice features out of the box : slice your sitemap by 50.000 links, gzip them, and create the [sitemap index](https://support.google.com/webmasters/answer/75712?hl=en). You can also upload it to S3

Follow the readme, but here is a sample so you can compare :


{% highlight ruby %}

require 'sitemap_generator'

SitemapGenerator::Sitemap.default_host = 'http://example.com'
SitemapGenerator::Sitemap.create do
  add '/home', :changefreq => 'daily', :priority => 0.9
  add '/contact_us', :changefreq => 'weekly'
end
SitemapGenerator::Sitemap.ping_search_engines # Not needed if you use the rake tasks

{% endhighlight %}

When you have a small number of pages (few hundreds or less), just add all your pages to the sitemap, specifying refresh frequency and priority.
Once the sitemap is generated, just put it either in your public folder.



What if you have millions of pages to index ?

That's exactly the situation i faced with Github awards : i have a page each Github user, so potentially that's more than 10 Millions pages to include in the sitemap.
So should i generate a huge sitemap with all these pages ?

You should add to the sitemap pages that are not easily reachable trhough link walking. That's exactly the situation for Github awards : the vast majority of user pages are only accessible through the search, there no way for a search engine crawler to find them on its own.

Another thing to consider is the relevancy of this pages for a search engine, i.e: what is the amount of unique content on these pages ?
For example on a e-commerce website each product has a unique description (if the same description is not on 10 different sites...), user comments, so potentially  it's valuable to index all these pages.
For github awards i'm only generating stats for each user, there is basically no unique content to index for google.

Some discussion on Moz.com even suggest that this could hurt your ranking : "we've found it detrimental to give Google hundreds of pages to crawl on a sitemap that we don't feel are important" ([source](http://moz.com/community/q/should-xml-sitemaps-include-all-pages-or-just-the-deeper-ones))

So in this case i decided not to include user search from the sitemap. I ended up with a 2 relevant page sitemap instead of a 10+ Millions irrelevant pages.


#### Step 3 : submit your sitemap

Now that your sitemap is generated, go to Google webmaster tools. In the site dashboard wheck that your sitemap was found by google crawler. If not, submit it.

Tips : If your have a very large sitemap, you should split it into several files, with a maximum of 50k urls each. Create a sitemap index describing all the sitemap files, this is an xml file looking like this :

{% highlight xml %}

<?xml version="1.0" encoding="UTF-8"?>
   <sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
   <sitemap>
      <loc>http://www.example.com/sitemap1.xml.gz</loc>
      <lastmod>2004-10-01T18:23:17+00:00</lastmod>
   </sitemap>
   <sitemap>
      <loc>http://www.example.com/sitemap2.xml.gz</loc>
      <lastmod>2005-01-01</lastmod>
   </sitemap>
   </sitemapindex>
  
{% endhighlight %}


You can learn more about sitemap index [here](https://support.google.com/webmasters/answer/75712?hl=en) 



#### Step 4 : add meta tags

* __[Title](http://moz.com/learn/seo/title-tag)__ : Displayed in search engine results, important for SEO. Recommended format is : 'Primary Keyword - Secondary Keyword - Brand Name'

* __[Description](http://moz.com/learn/seo/meta-description)__ : Not used for rankings, displayed in search results. Optimal length is about 150 characters. Use a description that will make the user click on this link

* __[Keywords](http://moz.com/community/q/meta-keywords-should-we-use-them-or-not)__ : Not important for SEO, not displayed in search results, better to not include them.

* __[nofollow](http://moz.com/learn/seo/robotstxt)__ : Tell crawlers to index that page but don't follow any links on that page. Can be combined with noindex in the same tag : "nofollow, noindex"

* __[noindex](http://moz.com/learn/seo/robotstxt)__ : Tell crawlers not to index that page

* __[canonical](http://moz.com/blog/complete-guide-to-rel-canonical-how-to-and-why-not)__ : Set the original url for the content (de-duplicate root domain and www)

To include meta tags in your views use the [content_for](http://guides.rubyonrails.org/layouts_and_rendering.html#using-the-content-for-method) helper :

In ``` application.html.erb ``` :

{% highlight ruby %}

<head>
  ...
  <%= yield :head %>
</head>
  
{% endhighlight %}

In your view : 

{% highlight html %}

<%= content_for :head do %>
  <title> Github ranking | github-awards</title>
  <meta name="description" content="Discover your ranking on Github ! Find out what is your rank by language, in your city and in your country"/>
  <link rel="canonical" href=<%= welcome_url %> />
<% end %>

{% endhighlight %}


That's it ! Any more ideas on how to improve a Ruby On Rails ranking on search engines ? If so Post a comment.
