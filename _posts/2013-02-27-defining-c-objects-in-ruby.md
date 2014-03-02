---
layout: post
title: Defining C Objects in Ruby
tags: ruby, embedded, c, api
nav: Blog
---
A few days ago [I wrote a post about marrying Ruby and C][1] and
provided an easy to follow [example gist][2]. After spending some more
days hacking on C/C++ integration with the Ruby virtual machine I
decided that finding some quality examples was surely a real big
pain. Many of the problems that we are facing are directly related to
[objects being accessed from multiple threads at the same time][3] in
the Ruby virtual machine.

While learning I found writing some example code definitely
helps. This [new example][4] is a little more complex, but pretty much
covers most of the bases in regards to basic object functionality. I
decided to leave out inheritance in this example as it was getting to
be pretty big. My goal was to be able to sit down and write the
example, plus a blog post, in a single night. If it took me longer
than a few hours its probably too complex of an example.

I am going to continue diving into embedding the virtual machine, and
with that I hope to be able to continue to document examples here and
on my [github account][5]. Feel free to drop me some patches if you
find errors in the code. Or [leave a few comments][4].

[My previous example][1] takes some time and shows very basic Ruby
virtual machine integration with a C application. This example expands
on this and includes how you might wrap a C structure and integrate it
with normal functionality inside of Ruby. Some examples that you'll
see here include: instance and class variables, instance and class
methods, using the initialize method and yielding to the calling
iterator function.

Be sure to [take some time and read the basic example][1] so that
you're sure to understand how it all works. The script can easily be
changed in the main.c file if you want to ``puts`` some information.

<script src="https://gist.github.com/johnbellone/5044723.js">
</script>

[1]: http://www.thoughtlessbanter.com/blog/2013-02-23-marrying-ruby-with-c/ "Marrying Ruby with C"
[2]: https://gist.github.com/5020125 "First example Gist"
[3]: http://blog.phusion.nl/2010/06/10/making-ruby-threadable-properly-handling-context-switching-in-native-extensions/
[4]: https://gist.github.com/johnbellone/5044723 "New example"
[5]: https://github.com/johnbellone
