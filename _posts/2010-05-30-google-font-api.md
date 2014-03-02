---
layout: post
title: Google Font API
tags: Font,Google,Open Source,Programming,Programming,Technology,Web Design
---
I have finally begun my [five-years-in-a-making web project][1] and I
decided to throw a simple countdown splash screen to give myself a
little motivation to get it finished. Something that has always ticked
me off about the Internet is the fact that despite all the
standardization that we attempt to put forth with the W3C, Acid, and
the HTML 5 movement it is still fucking impossible to pick a decent
font that you can guarantee will be on (most) platforms. As a
programmer, I absolutely loathe web design, in fact that is usually
the barrier to entry for most of my web projects - I can not figure
out the damn design - but through trial and error I generally am able
to produce something which is at least a little pleasurable to look
at.

This brings me to the topic at hand. The Google Font API (and the
Google Font Directory) was announced at the Google I/O conference and
detailed in this [Google code blog post][2]. What Google has done is
created a repository that makes fonts freely available to web
designers (and programmers) with a simple HTML stylesheet
include. Before I even finished their blog post I was immediately
cursing Microsoft because Internet Explorer 6 is usually the reason
why technologies such as this do not get adopted quicker, but I was
amazed even more, Internet Explorer 6.0 and up are supported!

As you can see on [Type Aloud][1] it is really as simple as these two
lines of HTML/CSS.

```html
<pre lang="html4strict">
<link rel="stylesheet" type="text/css" href="http://fonts.googleapis.com/css?family=Reenie+Beanie">
<style>
h1 { font-family:'Reenie Beanie', serif; }
</style>
<h1>123 days until launch.</h1>
</pre>
```

Go take a look at Google's [blog post on the matter][2] and start
using the Font API in your own projects. Happy coding!

[1]: http://www.typealoud.com/
[2]: http://googlecode.blogspot.com/2010/05/introducing-google-font-api-google-font.html
