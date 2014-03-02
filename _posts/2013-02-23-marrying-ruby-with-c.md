---
layout: post
title: Marrying Ruby with C
tags: ruby, embedded, c
nav: Blog
---
For a few weeks now I've spent some time working on embedding the Ruby
virtual machine into an application service for a [Celluloid][1]
server spike. Specifically we took the trunk release of Ruby 1.9.3 and
started integrating our service framework utilizing some of our
[tried and true libraries][4] inside of our server code. This is a
similar approach that you would take when developing a native
extension - the commonly used [mysql2][2] gem is an example of this -
where an interface API is written to expose functionality into the
virtual machine.

We took a similar approach. The beauty of the [Ruby language][5] is
that it is very easy to digest, and even easier to interface
with. I've written up a [small example gist][6] which I have included
below that illustrates how easily you can embed the virtual machine
into an existing C application with very little effort.

<script src="https://gist.github.com/johnbellone/5020125.js">
</script>

[1]: http://github.com/celluloid/celluloid "Celluloid"
[2]: https://rubygems.org/gems/mysql2 "Mysql2 gem"
[3]: https://rubygems.org/gems/bundler "Bundler gem"
[4]: http://github.com/bloomberg "Bloomberg on Github"
[5]: http://ruby-lang.org "Ruby the Language"
[6]: https://gist.github.com/5020125 "Ruby gist"
