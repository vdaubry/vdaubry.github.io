---
layout:     post
title:      "Ruby client for Google Cloud Storage "
subtitle:   ""
description: "The sad story of downloading a file from Google Cloud Storage in Ruby"
date:       2014-01-26
author:     "Vincent Daubry"
header-img: "img/post-bg-03.jpg"
---

###Ruby client for Google Cloud Storage 

After using AWS  for some years, the Google Cloud platform feels like stone age :

* Oudated code sample
* Overall complexity
* Spaghetti documentation 
* Client still doesn't support file download (after 5 years, come on !)

API are everywhere and every single conference repeats the same mantra : "treat developers as customers", "think about onboarding".<br>
Either Google is deaf, or they left the startups market to AWS. I wish them good luck competing with Microsoft Azure for the entreprise business.

So enough bitching, if you need to download a file from Google Storage, here is a fixed version of their code sample :

{% highlight ruby %}
require 'google/api_client'
require 'highline/import'
require './oauth_util'

# Constants for use as request parameters.
API_VERSION = 'v1'
DEFAULT_BUCKET = 'githubawards'
FILENAME = 'your_file_to_download.txt'

# Creating a new API client and loading the Google Cloud Storage API.
client = Google::APIClient.new(:application_name => "githubawards", :application_version => "0.1")
storage = client.discovered_api('storage', API_VERSION)

# OAuth authentication.
auth_util = CommandLineOAuthHelper.new(
  'https://www.googleapis.com/auth/devstorage.full_control')
client.authorization = auth_util.authorize()

result = client.execute(
        :api_method => storage.buckets.get,
        :parameters => { 'bucket' => DEFAULT_BUCKET, 'object' => FILENAME }
      )

url = URI("http://storage.googleapis.com/#{DEFAULT_BUCKET}/#{FILENAME}")
access_token = "Bearer "+result.request.authorization.access_token

Net::HTTP.start(url.host, url.port) do |http|
  request = Net::HTTP::Get.new url.request_uri
  request.add_field("Authorization", access_token)

  http.request request do |response|
    open FILENAME, 'w' do |io|
      response.read_body do |chunk|
        io.write chunk
      end
    end
  end
end


{% endhighlight %}


You can checkout the full project [here](https://github.com/vdaubry/storage-getting-started-ruby)