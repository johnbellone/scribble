---
layout: post
title: Solving N+1 Query Problem In C++

tags: C++,N+1 Query,Programming,Ruby On Rails,Software,Sql
---
<p>The past couple of weeks I have been doing some research because I am planning on working on a <a href="http://www.fastcgi.com/drupal/">FastCGI</a> <a href="http://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller">Model-View-Controller</a> framework for developing web application services in C++. I am a <a href="http://bloomberg.com">C++ engineer by day</a> and have been working with the language for nigh on a decade. The brief research I was able to do has shown me that there are no <em>DataMapper</em> or <em>Active Record</em> open source libraries available.</p>
<strong>What Exactly Is The N+1 Query Problem?</strong>
<p>When using an abstract framework to build a data model for use with an SQL-esque language you generally need to build a set of classes to model the schema in said language. For <a href="http://typealoud.com">Type Aloud</a>, lets say that I want to display all of the stories in a set of categories after you get them back based upon two slugs taken from the site's URL.</p>
<pre lang="sql">
SELECT id FROM categories WHERE slug='sci-fi' OR slug='fantasy'
SELECT id, name FROM stories WHERE category_id = 0 OR category_id = 1 
</pre>
<p>How many queries will be run? At most there will be two queries, but what about if none of the categories match the two slugs provided? That first dangling select query will be executed each and every time even if there are no matches to search against. How can we fix this?</p>
<pre lang="sql">
SELECT * FROM stories 
INNER JOIN categories ON stories.category_id = categories.id 
AND (categories.slug = 'sci-fi' OR categories.slug = 'fantasy')
</pre>
<p>This type of explicit join will allow you to execute a single SQL query and, in the long run, will save you thousands of CPU cycles with your web applications. This type of data mapper already exists in <a href="http://rubyonrails.org/">Ruby on Rails</a> using the <a href="http://datamapper.org/">Data Mapper gem</a> which is freely available. But as of right now there is no such framework available (unless I am mistaken) in C++ which gives you the power and flexibility to build your data models and eat your cake too. My first plan in developing an MVC framework is to work on architecting a proper data mapper library for C++.</p>
<p>Anyone else game?</p>

