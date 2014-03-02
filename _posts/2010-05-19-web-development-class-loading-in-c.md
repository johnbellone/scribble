---
layout: post
title: Web Development, Class loading in C++
tags: C++,Mvc,Observer,Programming,Rails,Ruby,Software,Web Development
---
On my way home from work I started to put some mind power towards
figuring out a solution to the issue of adequate class loading in
C++. A quick Google search for "[Classloading C++][1]" brings up a few
pages that are of quite an interest. You see for awhile now I have
been trying to grasp why I have not found any model view controller
frameworks written in C++ running on top of FastCGI, and one of the
reasons that I have been stuck on is the fact that people do not want
to modify, compile, start, execute in order to get through one series
of tests for Internet projects. Of course, there are many ways to
divide your project up appropriately to limit the compile time of
certain small pieces, but in the end, there is still that dependency
on the fact that we're still shit slow compared to Ruby development.

One of the features I love about Ruby on Rails is the fact that there
are long periods of time that I really never need to restart Mongrel
while developing. I have my Emacs buffer pointed to a couple of files,
save out my changes and click the refresh button on Chrome. That's how
easy it is. Could we achieve that development speed with a C++
framework? My my rain soaked walk home I went through it all in my
head, and I firmly believe that speedy Web development with a proper
C++ framework is achievable. But something core to this, at least as I
see it, would be a structured dynamic class loading architecture which
would allow on-the-fly loading and unloading of linked objects. In
"development" mode (which could merely be controlled by an environment
variable) we could even execute g++ each and every time we have a web
request as long as the dependencies for these plugins were small
enough to minimize compile/link time. A class loader could be pointed
to a directory similar to class path environment variables, setup to
look for a specific string through a regular expression, and
dynamically load object files based upon the timestamp of the
file. The core framework would need to be a shared library - so your
classes to handle the variety of software patterns you decide to use
(Observer, Singleton, MVC, etc) would be something that you'd need to
take down the whole server if updated. But once a framework is to a
certain point you rarely make changes to the core.

After I worked through these thoughts on the PATH ride into Harrison I
got to thinking: because we have access to literally _all_ the low
level libraries for Ruby, Python, PHP, what is stopping us from
building a framework that will allow simultaneous development in any
language that we can plug in easily? Of course, I do not see why
anyone would want to do this inside of a real development environment
when you could just as quickly (and easily) stick to a single
language, but the thought still piqued my interest.

Just something on my mind.

[1]: http://www.google.com/search?q=classloading+c%2B%2B
