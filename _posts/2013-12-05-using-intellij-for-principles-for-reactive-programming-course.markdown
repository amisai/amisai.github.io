---
layout: post
title: "Using IntelliJ for Principles for Reactive Programming Course"
date: 2013-11-15 09:05
comments: true
categories: programming
---

This last quarter I'm focused in [Principles of Reactive Programming](https://www.coursera.org/course/reactive) with Scala taught by Martin Odersky, Erik Meijer and Roland Kuhn at Coursera.

As IDE they suggest to use [ScalaIDE](http://scala-ide.org/index.html), a powerful IDE based on Eclipse that, among other things, allows you to use an interactive worksheet (as a REPL) where to practice with objects, functions and all the stuff. 

My problem is that I'm a [IntelliJ IDEA](http://www.jetbrains.com/idea/) developer (sorry, we all have our defects ;-) ), so I've tried to import each week assignments to IntelliJ. After several attempts, I've found this sbt plugin [gen-idea](https://github.com/mpeltonen/sbt-idea). 

In order to install, you have to create (if it doesn't exist) plugins.sbt file in project folder and add following line:

	addSbtPlugin("com.github.mpeltonen" % "sbt-idea" % "1.5.2")

Once done this, you invoke plugin with:

	sbt gen-idea

and just wait while it downloads the whole internet twice and generate .iml and .idea files. Then, you have to open files with IntelliJ.

As an aside, I'm using [Scala Plugin for IntelliJ IDEA](http://confluence.jetbrains.com/display/SCA/Scala+Plugin+for+IntelliJ+IDEA), which includes a [worksheet](http://blog.jetbrains.com/scala/2012/12/04/scala-worksheet/) as well. So far, so good.