---
layout: post
title: The Difference Between Subscription and Being A 'Fan'

tags: Programming,Programming,Rails,Type Aloud,Writing,Writing Community
---
<p>I have arrived at one of the bullet points for <a href="http://typealoud.com">Type Aloud</a> where I must implement the ability for one user to <em>follow</em> another user, similar to being a friend on <a href="http://facebook.com">Facebook</a> or exactly the same as becoming a follower on <a href="http://twitter.com">Twitter</a>. But I came to a dilemma that needed to be solved: <strong>What if someone only wanted to follow one particular story from an author?</strong></p>
<p>The first thing that came to mind (and ultimately stuck) was to have two different type of subscription models - the first would allow you to physically subscribe to a story and be notified when a new chapter was posted by said author. This subscription would keep track of reading point on a particular chapter as well as what chapter was the last one that you read. This may seem very trivial for web browser users but when you plan on handling <a href="http://www.amazon.com/Kindle-Amazons-Original-Wireless-generation/dp/B000FI73MA">Amazon Kindle</a> traffic this becomes very important. The second subscription model would be a "Fan" and this is where you want to hear absolutely everything from the author - if they decide to post a new story, you hear about it, or if they decide to write a poem, the same deal.</p>
<p>When thinking through this I was trying to take into consideration user interaction. How would the button placement work for these two particular types of subscriptions? If someone wanted to cease being notified from said author, how exactly would that work? And finally, if someone subscribes to another author's story and <strong>then becomes a fan</strong> what happens if they eventually cease the fanship - do we maintain the original state of subscription?</p>
<p>I would be interested what you all have to think.</p>

