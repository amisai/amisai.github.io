---
layout: post
title: "Modular development driven by tests workshop"
date: 2013-12-01 23:37
comments: true
categories: programming
---

Last weekend I attented to [Modular development driven by tests workshop(sp)](http://www.meetup.com/madswcraft/events/152606792) organized by [Software Craftsmanship Madrid](http://www.meetup.com/madswcraft/) and facilited by [@jacegu](https://twitter.com/jacegu) and [@pasku1](https://twitter.com/pasku1) and I really enjoyed it. 

Using as example a usual use case (user management in a social network), this workshop attempted to provoke some reflection about good practices in programming, modular architecture of an application, learning to differentiate between bus iness logic and implementation details, differences between frameworks and libraries, and how frameworks condition quite early your application architecture (we even had time to mention ORM and [The Vietnam of Computer Science](http://blogs.tedneward.com/2006/06/26/The+Vietnam+Of+Computer+Science.aspx)) 

Personally, I enjoyed quite a lot this workshop and conversations with my workshop partner were quite instructives. Our worshop code (java version) is in my [github](https://github.com/amisai/modularTDDWorkshop).

After a couple of days, I have some ideas:

* The architecture that emerges from this workshop is one aligned with [hexagonal architecture](http://alistair.cockburn.us/Hexagonal+architecture) (or Ports and Adapters) from Alistair Cockburn, or [Clean Architecture](http://blog.8thlight.com/uncle-bob/2012/08/13/the-clean-architecture.html) from Robert C. Martin. In our firsts iterations we developed our application core, with business logic, validation rules, ... and after that, we developed an external interface (or adapter) for that application core. We checked this architectural style allows you to use different user interfaces (such as a Web, REST, command line, ...) without needing to change you application core. Actually, my doubt has to do with how to pass information between adapters and core. Along several iterations, we were discussing about if parameters (and return values) should be simple types (such as String, for instance) or core entities (like User). At the end, and contrary to my first thought, we chose simple types and we saw this was the correct choice as we began to write our first user interface and realized that interface shouldn't (and probably couldn't as well) know anything about entities (this idea is confirmed at Robert C. Martin text: '...The important thing is that isolated, simple, data structures are passed across the boundaries... ', and he mentions dependency issues as well).

* My second thought talks about this idea of not getting attached too soon to implementation "details" (such as your persistence tool, user interface). In fact I have opposite feelings. On one side, I agree that I want an hexagonal architecture, to avoid changing my application core with each new interface (or changing my database due to performance reasons, for instance). On the other hand, we can see that market (and tradition or your company or  your team mates or ...) suggests you from the beginning (maybe 'forces' is a strong verb here) what development stack you're going to use. Obviously, they are not opposite choices, and you can use hexagonal architecture with spring or rails, but we all have seen too many applications attached to framework (or database, or ...). Discipline and knowledge will help in this type of situations, I imagine.

As a personal task, I'd like to do this workshop in other languages. I use Java because I (and my partner as well) was more comfortable with it, but as firsts options I see Ruby (to try with a dynamic language) or Scala (to try a more functional approach).