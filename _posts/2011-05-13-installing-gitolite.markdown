--- 
layout: post 
title: Installing gitolite 
published: true 
date: 2011-05-13 
categories: [software] 
---
I was thinking about migrating my personal projects from subversion to git, to be able to practice git usage and learn more about git workflows.

I'm reading right now [Pro git](http://progit.org/), and it mentions [gitosis](http://eagain.net/gitweb/?p=gitosis.git) and [gitolite](https://github.com/sitaramc/gitolite). It seems that both
allow you to have private repositories, and they are configurated by changing a configuration file and pushing it to server again, so I decided to install gitolite, because it has more fine-grained
permissions, allowing you to control who can push to different branches of same repository.

As I have a debian-based machine (an ubuntu server, namely), gitolite is quite easy to install following instructions you can find anywhere in internet through google. I've used
[these](http://www.davedevelopment.co.uk/2010/12/05/how-to-install-gitolite-on-ubuntu-10-10-maverick-meerkat/) instructions (after updating my server from Jaunty to Natty, as explained [here](http://www.unixmen.com/linux-tutorials/linux-distributions/linux-distributions4-ubuntu/1526-how-to-upgrade-from-ubuntu-1010-to-ubuntu-1104-natty-desktop-a-server). Gitolite didn't have a .deb package in ubuntu repositories until 10.10 version, I believe).

Once you have installed, gitolite works perfectly, allowing you to practice another git workflows. In case you need, you can install also gitweb, to have read-access to projects in your repository. As usual, there are a lot of resources in internet explaining how-to, I used instructions shared [here](http://computercamp.cdwilson.us/git-gitolite-git-daemon-gitweb-setup-on-ubunt "here").
