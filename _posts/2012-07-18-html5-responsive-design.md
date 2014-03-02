---
categories: programming
tag: life development
nav: Blog
title: HTML5 Responsive Design
---
About every year I get an itch to re-design my [website][1] and blog
to keep my web designing skills up to snuff. You see, up until my
recent position at [Bloomberg Government][2] I have not been able to
professionally use my web developer (and design) skills for over two
years. In the programming world, especially web development, that's a
damn *eon*. But after renewed interest and vigor, I have been
investigating the world of [responsive web design][3] with [HTML5][4]
and [CSS3][5].

The ideal development platform for any software is _fixed_, that is,
we only have a single canvas that we need to paint for, and don't have
to worry about scores of other mediums that our masterpiece can be
viewed through. Unfortunately in reality we need to deal with
lackluster web browser support for emerging standards where it often
the case that a _majority of your core audience is *fragmented*_.

Back in the old days we were able to get away with separate
stylesheets for merely [IE6][6] and _everyone else_ which usually
amounted to some version of [Firefox][7] and [Opera][8]. But now the
browser market is being dominated by scores of devices running all
different kinds of browsers. This ranges from high resolution
monitors, older phones with crappy browsers, smaller, faster phones
with great browsers - the combinations go on and on.

[Responsive Web Design][3] or _RWD_ uses media queries, and a fluid
layout system, to mold the layout of the content for the device
viewing it. Many more elements can go into a responsive design, but
the ultimate goal is to achieve a web site which looks fantastic on
any resoluation device that you're viewing it on. Previously this was
achieved by building out a separate mobile website which had a
completely different backend. Using RWD principles you can build a
_single, flexible design_ which reduces the overhead of managing a
second, completely independent site.

After reading the [book by Ethan Marcottee][9] which illustrates all
of the components that go into a responsive web design, I decided to
completely re-imagine my blog and website. The design is still in
progress, but the site that you're seeing now is built on top of
[Twitter Bootstrap][10] with [CSS3 media queries][5] and new,
[HTML5 layout principles][4]. Along with all of that I decided to
throw out the disgusting installation that is [Wordpress][11], and
switch to a much more dynamic backend driven by the static site
generator that [GitHub Pages][12] uses called [Jekyll][13].

All in all I am pleased with my design, and it has been a great
experience getting up to speed with web standards and development
again. I'm hoping to continue my work and revive [Type Aloud][14], my
social reading and writing community, and dive deeper into the realm
of Ruby on Rails. Its going to be a fun time!

[1]: http://www.johnbellone.com "My website"
[2]: http://www.bgov.com "BGov"
[3]: http://en.wikipedia.org/wiki/Responsive_Web_Design "RWD"
[4]: http://en.wikipedia.org/wiki/HTML5 "HTML5"
[5]: http://en.wikipedia.org/wiki/CSS3#CSS_3 "CSS3"
[6]: http://en.wikipedia.org/wiki/Internet_Explorer_6 "Internet Explorer 6"
[7]: http://en.wikipedia.org/wiki/Firefox "Firefox"
[8]: http://en.wikipedia.org/wiki/Opera_browser "Opera"
[9]: http://www.abookapart.com/products/responsive-web-design "Responsive Web Design - Book"
[10]: http://twitter.github.com/bootstrap/ "Twitter Bootstrap"
[11]: http://www.wordpress.org "Wordpress"
[12]: http://pages.github.com "GitHub Pages"
[13]: http://jekyllrb.com/ "Jekyll"
[14]: http://www.typealoud.com "Type Aloud"
