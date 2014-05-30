--- 
layout: post 
title: continuous testing in java with infinitest
published: true 
date: 2011-12-23 
categories: [tools] 
--- 

I've been playing with infinitest ([http://infinitest.github.com/](http://infinitest.github.com/)), a Eclipse plugin that is executing continuously your tests. In fact it's not executing ALL your tests, but those afected for your last changes. So far, so good.

Mental reminder:As I'm using maven as my basic building tool, the main problem is to teach Eclipse where my tests are (Project preferences-\>Java Build Path, check 'Allow output folders for source folders', and insert tartget/test-classes where needed), and ask Eclipse to build project automatically. That's all...
