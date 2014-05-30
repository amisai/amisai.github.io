--- 
layout: post 
title: Moving to SSD 
published: true 
date: 2012-02-26
categories: [hardware] 
--- 

This weekend project was migrate laptop HD to SSD. As SSDs prices are a bit high yet, I'm moving from a
500Gb HD to this 120Gb SSD:
[http://www.amazon.es/OCZ-Technology-VTX3-25SAT3-120G-Vertex-pulgadas/dp/B004Q81CKY/ref=sr\_1\_1?ie=UTF8&qid=1330250512&sr=8-1](http://www.amazon.es/OCZ-Technology-VTX3-25SAT3-120G-Vertex-pulgadas/dp/B004Q81CKY/ref=sr_1_1?ie=UTF8&qid=1330250512&sr=8-1).
(It's the first time I buy something as expensive as this in amazon, but
I wasn't able to find it cheaper anywhere else, and that's a sign of how
Amazon is changing game). This implies that I'm going to use external
storage for temporal storage, and also as backup, ...

So, I've read a lot of info from Internet about these devices, how to
install them and treat them properly. Two ideas here: you have to format
it paying attention to alignment, you have to avoid unnecessary
read/write operations.

Basic instalation sequence is following:

1.  SSD Partition
2.  Partition(s) Formatting
3.  OS Installation (Kubuntu in my case)
4.  Management of swapping operations, temporary files (such apt-get cache, for instance)...
5.  Journaling scheduler configuration
6.  Browser cache configuration
7.  Install of usual software
8.  Enjoy!!

\
 In order to no repeating what you could find with a quick search, I'm
sharing two links with a lot of information and ideas (one of them in
english, the other one in spanish):

- [http://foro.noticias3d.com/vbulletin/showthread.php?t=352706](http://foro.noticias3d.com/vbulletin/showthread.php?t=352706)\
- [http://www.ocztechnologyforum.com/forum/showthread.php?77769-A-Simple-How-To-on-Partitioning-and-Alignment-on-GNU-Linux-using-fdisk](http://www.ocztechnologyforum.com/forum/showthread.php?77769-A-Simple-How-To-on-Partitioning-and-Alignment-on-GNU-Linux-using-fdisk)

Install process, apart from partition and formatting step, went without
any problem.

It's a bit early to say there's a huge difference, but I've already
noticed that startup is faster, and the system is bit more responsive.
We'll see...

