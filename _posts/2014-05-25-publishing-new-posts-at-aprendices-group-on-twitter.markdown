---
layout: post
title: "Publishing new posts from Aprendices group on Twitter"
date: 2014-05-25 20:59:26 +0200
comments: true
categories: 
---

(yes, english is not my first language, sorry for any typo or mistake)

Today I'm presenting a personal project I've been working lately, as it's going out of personal use sphere and, hopefully, will be useful to other people.

There are hundreds of communities in Google+. I'm blessed enough of knowing [Aprendices](https://plus.google.com/communities/114859785439968913587), a spanish Google+ community where life-long learners share programming resources: videos, posts, ... 

But, I'm more used to Twitter than Google+, as I'd rather use a RSS agregator than receiving an email each time someone publish something new (and visiting that page just to check if there is a new posts is so ... 90's...)

So, this project started when I asked, innocently, about if there was any possibility of posting in Twitter each time there was a new post in Aprendices, as I believed it was more useful. (Not) surprisely,  [that conversation](https://twitter.com/franciscoferri/status/443476308488900608) derived in a suggestion: "Do it yourself". Mmm, good idea, why not? :-)

This project, then, it is clear: I need "something" that watch Aprendices page and publish in Twitter each new post.

My first option was "I won't do it" :-O, I mean, let's check if someone else has done it.

Nope. 

Mmm, ok, but this fits perfectly with [ifttt](https://ifttt.com): "if there is a new post in Aprendices, publish it in Twitter". My problem with ifttt was I wasn't able to find any adapter to Google+. Mmm, ups, but there's an adapter to RSS. Is there something that translates Google+ posts RSS? Yes. I found [gplusrss)(http://gplusrss.com/). But (seriously, I remembering Edison and its 10,000 ways of not doing things) gplusrss doesn't work wiht Google+ communities, or at least with this community. I opened a ticket at March 12, no answer yet (and that's not a complaint, I understand what happens with open source projects).

All right, seems I'll have to look for other options. So, project is, indeed, to scrape this community page at regular intervals al publish new posts. Ok, so how do I scrape? As my idea was "do not what is already done", my first option was [import.io](import.io). Interesting too, with a Mac client very easy to use, you define which fields to extract from a web page and it converts it to a spreadsheet. Oddly enough, I wasn't able to make it work properly with Aprendices page within the timebox I had for this task(as I'm writing this I think I could insist a bit more, maybe, but I was already considering do it myself...)

Ok, so it seems I'm going to make it (I insist, it wasnt't my first option). Let's check again, I need a program, probably in ruby (as I've been playing with Twitter clients for ruby, I wanted to go on this option) that, in regular intervals, visits Aprendices page, scrapes new posts data and store them somewhere. Also I need another process that once in a while selects a post (oldest one, for instance) from downloaded ones and publishes it in Twitter.

Where will I deploy it? I'd like it to be cheap, free if it's possible, so my first option is to use [heroku](http://www.heroku.com), o a box at home (I discarted this option, my phone company is not as reliable as I want to...). Deploying to heroku has a lot of advantages, and it imposes some restrictions as well, namely, my first idea as persistence was a CSV file (I mean, we're talking about storing maybe 30-40 URLs and descriptions, do I need a full RDBMS? don't think so, if I can avoid it and it isn't going to bother me), but an application lifecycle in Heroku advise against it: heroku can stop your node at any moment so, yes, it seems I'll need a RDBMS. I really don't care what, heroku provides us with some free space in a postgres instance and Mongo as well. I chose Mongo as an excuse to learn about it.

It seems this application architecture is being clearer, so I move to gems selection:

* [nokogiri](http://nokogiri.org/) will help me in Aprendices page scrapping
* [mongodb gem](http://docs.mongodb.org/ecosystem/drivers/ruby/
* [twitter gem](http://sferik.github.io/twitter/
* [sucker_punch](https://github.com/brandonhilkert/sucker_punch) and [fist_of_fury](https://github.com/facto/fist_of_fury) will be used in both refreshing post task and Twitter publishing task scheduling
* [sinatra](http://www.sinatrarb.com/) will allow me to create a small web interface where to check pending posts
* [rspec](http://rspec.info/) for testing (yes, remember that TDD has risen again ;-) ...)

Talking about development process, I spent a lot of time in Aprendices page scrapping. Div with specific classes inside divs with other classes and 3 or 4 levels like this, and with diferents classes depending on type of posts. My first version allowed me to start real testing, and I had to schedule another timebox in order to tune it.

Once deployed at heroku, I checked that lifecycle of a application like this, that is not receiving continually traffic, but it's going to wake up now and then doesn't fit with heroku's idea, which caused sucker_punch didn't activate refreshing nor publishing task in expected moments. I tried to keep this application awake, with an external request (using wget) but it wasn't enough. At the end, I chose to rent a box in [digitalocean](https://www.digitalocean.com/) (20GB HD, 512Mb RAM for only $5/mothn) where to deploy this application (I use this as an excuse to learn about version 3 of [capistrano](https://github.com/capistrano/capistrano) and to refresh my [puppet](http://puppetlabs.com/) knowledge), and I consider this as a good move: it's a much more stable environment for this kind of applications.

I consider this project as in beta status: it works, and I'm using it:

![sample post](/images/sample_post.png)

although I'll be doing a bit of babysitting during next weeks, just to check ... Only thing missing is that I'm publishing new posts in my personal account and I prefer to publish in [Aprendices Twitter account](https://twitter.com/deaprendices).

By now, I'm not sure about sharing this project source code: it's very specific, I don't think it'll help anyone else, but I will (at github, for instance) if someone requests it.
