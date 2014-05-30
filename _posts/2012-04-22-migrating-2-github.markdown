---
layout: post
title: "migrating 2 github"
date: 2012-04-22
published: true
comments: true
categories: [blog]
---

I'm moving this blog from [Posterous](http://amisai.posterous.com) to [Github](http://amisai.github.com). I could look for a lot of reasons, but main one is that I want to learn how to use github as more than a projects repository, and also to improve my markdown knowledge.

I know I'm losing some things, such as Posterous inherent easyness: want to publish a post? Send an email..., or attachments management, and that I'm going back to static pages world, although this is through a template engine.

Github team recomends to use Jekyll, but after a bit Internet searching, I've selected Octopress, that adds some functionality to Jekyll.

This migration project had 3 steps

1. Initial blog setup.
2. Migrating posts from posterous to github.
3. Write this post.

As always, there's nothing new under this sun, so I've just followed some ideas from several internet pages.


Initial blog setup
------------------
In this step, I've followed instructions at [http://code.dblock.org/octopress-setting-up-a-blog-and-contributing-to-an-existing-one](http://code.dblock.org/octopress-setting-up-a-blog-and-contributing-to-an-existing-one), and in 15-20 minutes I had a "Hello World!!" page at github


Migrating posts from posterous to github
----------------------------------------
Intention was not to lose no published posts. In order to do that, first I thought using migration utility Jekyll provides: [blog migrations]([https://github.com/mojombo/jekyll/wiki/blog-migrations]), but Posterous team have changed their API, so that tool didn't work. Jekyll team has already developed a solution, but it isn't yet in deployed version, so I downloaded from here: [https://gist.github.com/2143368](https://gist.github.com/2143368), and after obtaining a Posterous key (directly generated here: [Posterous API](http://posterous.com/api]) ), I run this program that worked properly.

Remains, obviously, check each post content, not only text, but blog needed information (published date, categories,...) and translating to english, but something to be doing in free moments.


Write this post
---------------
And that's all, folks :-)
