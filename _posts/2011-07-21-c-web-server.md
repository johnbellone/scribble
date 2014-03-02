---
layout: post
title: C++ Web Server

tags: C++,Nginx,Pennies For Thought,Programming
---
<p>So, this morning I couldn't sleep, and around 4:00AM I started messing around with nginx, fastcgi and C++. For awhile now I have been considering the feasibility of an extendable and reusable framework for serving up web content from C++ applications. Of course, all you web programers want to write code in Javascript and Ruby, but sometimes there are applications that can be core to a company that do not need to (or should not) be rewritten merely to service a different type of client. I wrote a little test program that I <a href="http://github.com/johnbellone/cpphttp">threw up on my Github.com account</a>.</p>
<p>That's my reasoning for developing this simple proof of concept application. I didn't want to actually download the fastcgi libraries that exist for C, mainly because it was 4AM and I am a lazy fuck, so I decided to write up something simple with accept(), recv() and send(). The actual configuration for nginx is quite simple, you can just use their example for proxying to an Apache web server.</p>
<p>For those of you that are just as lazy as I am, <a href="https://github.com/johnbellone/cpphttp/blob/master/main.cc">click on this big bad beautiful link</a>, and enjoy the show. Later, at some point, I will write up my thoughts on how an actual framework to solve this problem may work (and look), but right now I need to take a shower and go to work.</p> 
