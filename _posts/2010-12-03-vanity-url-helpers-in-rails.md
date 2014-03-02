---
layout: post
title: Vanity URL Helpers in Rails

tags: Code,Programming,Ruby On Rails,Snippet,Software,Vanity Url
---
<p>I have been doing some hacking on <a href="http://typealoud.com">Type Aloud</a> and I was looking for an answer to a question that was bugging me: what is the best way to use <a href="http://api.rubyonrails.org/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to">link_to</a> with a vanity URL setup? I asked my question over at <a href="http://stackoverflow.com">Stack Overflow</a> and I figured I would post the answer to the question here in case anyone was looking as I was.</p>
<p>Inside of my application the route setup is quite simple. 
<pre lang="ruby">
match '/:id', :to => "users#show"
match '/:user_id/:id', :to => "stories#display"
</pre></p>
<p>Now I want to be able to make a very simple call inside of my view logic which will print out a pretty URL. Since I am using resource definitions for several controllers I cannot use the normal Rails URL helpers. The answer to my question is actually quite simple, and I already have used it before, but what I wasn't doing was correctly passing through the objects into the helper. Here are the changes that you need to make to those routes above.
<pre lang="ruby">
match '/:id', :to => "users#show", :as => "vanity_show_user"
match '/:user_id/:id', :to => "stories#display", :as => "vanity_show_users_story"
</pre>
And finally inside of your view you would build both links like the following.
<pre lang="ruby">
<%= link_to @story.name, vanity_show_users_story_path(@user, @story) %>
<%= link_to @user.name, vanity_show_user_path(@user) %>
</pre></p>
<p>I hope that this helped you out as much as it helped me! Kudos to the amazing <a href="http://ryanbigg.com/2010/04/want-it-give/">Ryan Bigg</a> for the <a href="http://stackoverflow.com/questions/4295419/what-is-the-best-way-to-deal-with-vanity-url-helpers-in-rails-3">original answer</a>.</p>
