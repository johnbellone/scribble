---
layout: post
title: Git and Emacs

tags: Emacs,Git,Github.Com,Programming,Shortcuts,Technology,Tricks
---
I have been a <a href="http://git-scm.org">Git</a> user now for many years. Over at <a href="http://zinkkinc.com">Zinkk</a> I got the boys to switch over from Subversion, and I am trying to do the same <a href="http://bloomberg.net">at my current employer</a> when possible. I have been using <a href="http://github.com/johnbellone">Github.com</a> now for over a year. I am a huge fan of this type of version control, this type of <em>development</em> and I am always looking for a way to streamline my work flow.

Streamlining my workflow. This is the precise reason why I am an <a href="http://www.gnu.org/software/emacs/">GNU Emacs</a>. I could go on, and on about why I believe Emacs is the best software development tool in the world, but I would be doing the package a huge disservice because I'm not an Emacs-guru. For awhile now I have not been able to use the version control bindings in Emacs because, for some reason, Emacs on the Mac was not picking up the <strong>PATH</strong> environment variable for executable lookup. After a little bit of googling I was able to find the answer on <a href="http://stackoverflow.com/questions/930439/using-git-with-emacs">Stack Overflow</a>. 

I am including the snippet below. You can put it in your Emacs configuration file which <em>should</em> be in your home directory. If you get a chance, have a gander over at my <a href="http://github.com/johnbellone/emacs">Emacs configuration</a> that I have been using for a bit now. Kudos goes out to <a href="https://github.com/defunkt">Chris Wanstrath</a> from Github for the layout. 

<pre lang="lisp">(when (equal system-type 'darwin)
  (setenv "PATH" (concat "/opt/local/bin:/usr/local/bin:" (getenv "PATH")))
  (push "/opt/local/bin" exec-path))></pre>

Execute <em>M-x eval-buffer</em> and you can now use <em>C-x v-v</em> to commit. Have fun! 
