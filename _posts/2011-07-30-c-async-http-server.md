---
layout: post
title: C++ Async HTTP Server

tags: Asio,C++,Programming,Technology,Web
---
<p>A few days ago to the sweet, sweet melodies of Billy Joel, I woke up in the wee hours of the morning to code up a <a href="http://thoughtlessbanter.com/2011/07/21/c-web-server/">very crude C web server</a>. Of course, I tried to pass it off as a C++ implementation, but in reality I was pulling the wool over your eyes - the only C++  was used to build error messages, and the actual message to send down to the client. Not to mention it was a very crude, basic, implementation of socket handling in C. Nothing fancy.</p>
<p>Yesterday I was talking with some kind folks at the <a href="http://rebuildconf.com">re:build 2011 conference</a> in Indianapolis, and it got me to thinking that there aren't enough examples of C++ applications talking to the web. You know, actual C++, using the boost libraries and what not. So this morning, after grabbing <a href="http://gowalla.com/spots/230493">my amazing breakfast burrito at Henry's in downtown Indianapolis</a> I scoured the Internet and re-wrote my example application in Boost.Asio.</p>
<p>The code is much simpler, straight forward, and just damned better to look at. As always it is up and available at my <a href="https://github.com/johnbellone/cpphttp">Github account</a> for consumption. If you're interested in seeing the actual difference in implementations than <a href="https://github.com/johnbellone/cpphttp/commit/7f95cac9b96a45461af6b5b6c9566d2b1562c504">go no further than right here</a>.</p>
<p>I have a few more ideas on web services written in C++, but that's for another day. Let me know if you have any questions. As always, enjoy the code and report any bugs.</p>
