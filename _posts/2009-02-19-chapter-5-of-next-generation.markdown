--- 
layout: post 
title: Chapter 5 of Next Generation Java Testing
published: true 
date: 2009-02-19 
categories: [book] 
--- 
The main apportation of jUnit, apart from jUnit itself is the impressive echosystem of plugins and extensions that appeared to extend its functionality.

jUnit is an unit test framework, and unit here implies "anything that doesn't use any external system nor use any external system, so doesn't connect to a RDBMS, nor open a socket, nor depends on a JMS queue, for example". But the truth is that once you have a unit test framework, why don't we use it for testing my DAOs, for instance?

Of course, jUnit is agnostic about your external systems, but it allows to be extended for testing your unit behaviour when connected to them. Previous chapter focused on intregation testing with J2EE containers, and showed several options for that testing (in-container or "out-container" testing). This chapter focused in other areas of integration testing.

It starts speaking about Spring and their group of classes for testing (and how to avoid their attachment to jUnit), but soon speaks about other tools, such as DbUnit, HtmlUnit, or Swing testing. I've found several tools I didn't know, such as Guice, or those oriented to test GUIs. Those that I already knew, such DbUnit, are well exposed, and the final part about Continuous integration has given me the same good feeling I had when I found a part about it in [Domain Driven Design](http://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=pd_bbs_sr_1?ie=UTF8&s=books&qid=1235036410&sr=8-1) book.

Interesting chapter, a bit short in several parts, but thought-provoking, and that's a good thing for this kind of books.

Next chapter, about extending testNG.
