---
layout: post
title: Model Scopes in Rails 3

tags: Arel,Optimization,Pennies For Thought,Programming,Query,Rails,Technology,Type Aloud
---
<p>I am going through the <a href="http://typealoud.com">Type Aloud</a> code trying to improve queries, implement some fragment caching, and generally clean anything up that I can before flipping the proverbial switch on this bad boy. I came across something a few weeks ago that, combined with the awesomeness that is <a href="http://magicscalingsprinkles.wordpress.com/2010/01/28/why-i-wrote-arel/">Arel</a>, makes my life a hell of a lot easier writing queries.</p>
<p>These <a href="http://www.railsrocket.com/rails-21-named-scope">named scopes</a> have been around in Rails for awhile now, but as always I am coming late to the party. Because Type Aloud contains "draft mode" where stories and chapters can both be in an unpublished state I need to be able to call only the <em>chapters</em> and here is a quick, simple way to do that on the model.</p>
<pre lang="ruby">scope :published, lambda {
   joins(:story).where(:disabled => false, :stories => {:disabled => false}).includes(:story, :user)
}</pre>
<p>The named scope will filter out any chapters that are not published or any chapters in stories that are not published. This is very important when displaying, let's say, a random chapter for reading that may not have yet been published in an existing story. The last statement at the end there will eager load the story (and user) because there really is never an instance where I don't want the story (user) records associated with this. Here are the queries that are executed. 
And here and the queries that are executed from this little snippet.</p>
<pre lang="sql">SELECT `chapters`.* FROM `chapters` INNER JOIN `stories` ON `stories`.`id` = `chapters`.`story_id` WHERE (`chapters`.`disabled` = 0) AND (`stories`.`disabled` = 0)
SELECT `stories`.* FROM `stories` WHERE (`stories`.`id` = 1)
SELECT `users`.* FROM `users` WHERE (`users`.`id` = 2)</pre>
<p>And of course, this is what the signature looks like from the controller.</p>
<pre lang="ruby">@chapter = Chapter.published.limit(1).first</pre>
<p>For this particular operation it resulted in a 0.5ms improvement in time spent during the Active Record phase. That may not sound like a lot, but it actually is a 19 percent time optimization. Good stuff!</p>

