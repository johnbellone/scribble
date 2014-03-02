---
layout: post
title: Bouncing A Database With Rails

tags: Database,Mysql,Programming,Rails,Ruby
---
After work each night for the past couple of months I have been getting my hands dirty with Ruby/Rails development. I can imagine that most developers out there grow to love rake, but for the life of me I literally hate executing a series of commands on a regular basis. The programmer in me loves automation, and while in development I find myself dropping, re-creating and migrating the database constantly. Why should I have to issue <em>three</em> commands?
<pre language="bash">rake db:drop
rake db:create
rake db:migrate
</pre>
After a little bit of searching I found that this can be accomplished in two commands.
<pre language="bash">rake db:reset
rake db:migrate
</pre>
Welp, that's not enough for me because I am just that damn lazy. So, a simple rake task to bounce a database.
<pre language="ruby">namespace :db do
  desc "Drop, create and migrate the current database"
  task :bounce => :environment do
    Rake::Task['db:reset'].invoke
    Rake::Task['db:migrate'].invoke
  end
end
</pre>
I hope you enjoy it as much as I do.
<pre>rake db:bounce</pre>
