---
layout: post
title: Towards A Better Code Editor
tags: Development,Dreams And Thoughts,Programming,Programming,Technology,Text Editor
---
Most of my day is spent staring at the blinking cursor of my text
editor. This is true for many people nowadays as most office work
happens on the computer, but for programmers - the very same
individuals whose creativeness are the building blocks for software -
can't seem to find a workflow that feels right. As a developer I find
myself getting frustrated every time that I have to reach across my
desk for a mouse, switch to a separate application to look up some
documentation, or drop into a terminal window for some quick bash
kung-fu. I am a firm believer of using the proper tool for the job,
but I have been writing code for over ten years now and have yet to
find something that fits the purpose.

Most web and application developers that I know are using proficient
in many text editors. The editor that they are using is either a
result of the product that they are working on, or past experience
using a particular piece of technology (extension, script, plugin,
etc) that makes the daily grind a little better. I rarely find a
developer who doesn't have a problem with some facet of the text
editor that they are using, and many of which feel that they are stuck
for one reason or another with a particular editor because of the
feature set it offers.

One thing that seems to be a common theme among these editors is that
they sit somewhere between a simple text editor, providing only basic
functionality of text formatting, and a full-blown suite of tools
which is offered by enterprise packages such as Microsoft's Visual
Studio which costs thousands of dollars and only works on the Windows
platform. Each has its specific use case, and I would never suggest
creating a Visual Studio project file to edit a<em> README</em> file
using the Markdown syntax, but every time that I have the opportunity
to use Visual Studio I always walk away feeling let down the next time
I drop into Emacs.

A key feature that I think is necessary in a development environment
is the ability for the software package to support live
documentation. This means that I want to be able pull up a quick blurb
about a particular API call that I am about to make, either be it in a
standard library that ships with the language of my choice, or the
application project that I am working on. The discoverability of
documentation needs to be in depth, but not something which clutters
my code window.

The editor software needs to be able to be extended on a per project
basis. There are often cases where a particular set of tools is
necessary for one web project, let's say something like
[CodeIgniter][1] which uses the [Sparks package management system][2],
and another application that is written with [Ruby on Rails][3] and
using the [RubyGems][4] system for extensions. And it is not merely
easy just to say that all PHP applications will use the _mode for
PHP_, and all the Rails projects will use the _mode for Ruby_, because
often there is a frontend component which shares context between the
two and is written in a language such as JavaScript (or more recently,
[Clojure][5]).

Testing each project now becomes an absolute pain in the ass. I may
need to manage the version of Ruby that I am running, or perhaps
bounce the Apache instances so that my new configuration is picked up,
or even worse the web application needs to be executed from a browser,
I need to tail a log file, and pray that the browser debugging
software is updated. That's way too many context switches.

I believe that there can be a much better way of handling the day to
day workflow of software development. There is a simple solution to
this problem that seems to have been overlooked with fancy editors
designed to be visually pleasing on the Mac. What do you think your
ideal development environment would be? All developers hate writing
documentation, but it is the first that we reach for when we want to
understand how to work with a library or call a standard API. We cry
out aloud when our text editor doesn't index the code that I am
writing and provide autocomplete. And we bitch when extending the
editor becomes a chore which sometimes rivals the problems we're
trying to solve.

There is a better way to handle this.

[1]: http://codeigniter.com/
[2]: http://getsparks.org/
[3]: http://rubyonrails.org/
[4]: http://rubygems.org/
[5]: http://clojure.org/
