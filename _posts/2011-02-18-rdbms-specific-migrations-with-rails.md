---
layout: post
title: RDBMS Specific Migrations With Rails

tags: Migration,Mysql,Postgresql,Programming,Rdbms,Ruby On Rails,Technology
---
I have been running into a problem recently with my development over at <a href="http://typealoud.com">Type Aloud</a>; some of my column data types differ from MySQL (my development database) and PostgreSQL (my production database). I store two copies of the story in the database: the first is the "human readable" version that uses the <a href="http://daringfireball.net/projects/markdown/">Markdown</a> syntax and the second is the HTML version of that syntax so it is easier to fragment cache and display when someone is viewing the chapter. This problem is particularly irritating because when it first happened in MySQL the text was merely truncated, but in PostgreSQL it correctly does not allow the insertion into the table if the text is too long. 

For the past couple of days I have been doing some light searching trying to figure out a way to have a RDBMS specific database migration, and I once I did some pecking in the <a href="http://api.rubyonrails.org/classes/ActiveRecord/Migration.html">ActiveRecord::Migration class</a> I was able to figure this out pretty easily. I figured that I would share it below since it took me a little while to find it. Now normally I do not believe in migrations being platform specific, but in this case because I wanted to actually have the application work on two types of platforms (in this case, two RDBMS).

<pre lang="ruby">class AddLongtextToPostgresql < ActiveRecord::Migration
  def self.up
    case ActiveRecord::Base.connection.adapter_name
    when 'PostgreSQL'
      execute "CREATE DOMAIN longtext as text"
      execute "ALTER TABLE chapters ALTER COLUMN html TYPE longtext"
      execute "ALTER TABLE chapters ALTER COLUMN body TYPE longtext"
    else
      puts "This migration is not supported on this platform."
    end
  end

  def self.down
  end
end
</pre>
