---
layout: post
title: Why I Love Rails 3

tags: Pennies For Thought
---
<pre lang="ruby">@category = Category.where(:slug => params[:category]).select(:id).first.id if params[:category]</pre>

Enough said.
