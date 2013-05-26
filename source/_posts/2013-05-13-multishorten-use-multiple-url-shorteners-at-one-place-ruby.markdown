---
layout: post
title: "MultiShorten - Use multiple url shorteners at one place(Ruby)"
date: 2013-05-13 16:34
comments: true
categories: ruby api
---
There are many URL shorteners available out there. Each one has its own features and caveats. Many of the URL shorteners out there have APIs associated with them so that we can use them in our applications. The painful reality is that each one will have its own - way of handling request and producing the output, usage limitations, exceptions and so on.

So using URL shorteners in your ruby application be pretty tricky. This is where [MultiShorten](http://github.com/ronyv89/multi_shorten) comes to the rescue. This is a ruby gem you can use in your ruby app to utilize 9 different URL shortening services. These services don't require account registrations so using them is pretty straightforward. But mind you they have separate APIs and each have different input and output requirements. MultiShorten takes care of this on its own.

#### Installing

Add this line to your application's Gemfile:

```
gem 'multi_shorten'
```

And then execute:

```
$ bundle
```

Or install it yourself as:

```
$ gem install multi_shorten
```
#### Usage

First require the gem where you want to use it

```ruby
require 'multi_shorten'
```

Next step is to instantiate a MultiShorten::Client object

```ruby
client = MultiShorten::Client.new
```

Now we can use this client to shorten any number of URLs with any of the 9 services. The client object has only one method 'shorten'. Using this method we can shorten our required URLs. There are two modes

- ###### Single

  Use this to shorten a URL with a single service. For example,

```ruby
client.shorten({:mode => "single", :url => "http://www.google.com", :shortener => "b54"})
```
As you can see above, by passing the value of mode as single you can shorten the URL using a single shortener.

The above request may generate an output as below

```ruby
{ :status => :success, :short_url => "http://b54.in/9o" }
```

- ###### Multiple

You can also utilize multiple services to shorten the same URL. For this you have to specify the value of ':mode' option as "multiple"

```ruby
client.shorten({:mode => "multiple", :url => "http://www.google.com", :shorteners => ["b54", "qr_cx"]})
```

The above request may generate an output as below
```ruby
{"b54" => {:status => :fail }, "qr_cx" => {:status => :success, :short_url => "http://qr.cx/9o"}}
```

As you can see, the URL shortening request made to B54 failed. But still you can use the QrCx shortened URL. 

#### Available short codes


[b54](http://b54.in)<br/>
[linkee](http://linkee.com)<br/>
[goo_gl](http://goo.gl)<br/>
[is_gd](htpp://is.gd)<br/>
[jumbo_tweet](http://jmb.tw/)<br/>
[meta_mark](http://metamark.net)<br/>
[mt_ny](http://mtny.mobi")<br/>
[qr_cx](http://qr.cx)<br/>
[shortr](http://shortr.info)<br/>

You can use the above short codes, to select the service. Please refer to their respective pages to know more about the services.

Happy Shortening!