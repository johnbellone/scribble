---
layout: post
title: Unique Composite Keys With Mongoid

tags: Database,Mongodb,Mongoid,Nosql,Programming,Rails,Ruby,Software
---
For awhile now my pet project has been running on top of the "noSQL" document database technology, <a href="http://mongodb.org/">MongoDB</a>, that the folks over at <a href="http://10gen.com">10Gen</a> have developed. After testing the tech and going to a couple of the New York City meetups, I immediately decided to push myself to utilize this in <a href="http://typealoud.com">Type Aloud</a>. But, along with the Rails 3.0 release and <a href="http://mongoid.org/">Mongoid</a> 2 (the Active Record wrapper that I am using for Mongo) I have had a hard time finding accurate up-to-date information on some less used features. One particular problem has been referencial (foreign) associations and the use of composite keys. 

Because the user's poems and stories in Type Aloud and only unique on the user level I have been unable to use a simple uniqueness validation on the document identifier which up until this point was just the default hash provided by the database. I need the composite, the user identifier and the story identifier, to be unique; I only want the user to only have one story named "Winnie the Pooh." It may be easier to understand some code.

A standard Story model in Rails (using Mongoid) might look something like this. Notice how I do not need to explicitly provide the key because it is assumed, by default, we will use the database standard hash provided as our primary key for the document. As you see I explicitly specify the slug field as being an index as this is what will most commonly be queried. In this case, the "id" field may contain something along the lines of <em>4c897698cd44a10f8b000006</em>.  
<pre lang="ruby">class Story
  include Mongoid::Document
  include Mongoid::Timestamps
  include Mongoid::Paranoia
  include Mongoid::Versioning

  # Document fields
  field :title, :type => String
  field :slug, :type => String
  field :description, :type => String
  field :disabled, :type => Boolean, :default => true

  # Document associations
  embeds_many :chapters
  referenced_in :user

  # Document indicies and keys
  index :slug, :background => true, :unique => false

  # Document validators
  validates_presence_of :title, :description
end
</pre>

The problem here, and the exact reason why I merely cannot validate uniqueness on the title, is because multiple users can have the same title for a story or poem. The submissions will be presented in a vanity URL format, e.g. <em>http://typealoud.com/johnbellone/the-darwin-prospect/chapter/1</em>, and thus will <strong><em>almost</em> always</strong> be queried with the user's name. My solution to making this unique is quite simple. So now the story identifier will be in the format of <em>the-darwin-prospect-4c892963cd44a108a2000008</em> where that hash at the end is the user's identifier. 
<pre lang="ruby">class Story
  include Mongoid::Document
  include Mongoid::Timestamps
  include Mongoid::Paranoia
  include Mongoid::Versioning

  # Document fields
  field :title, :type => String
  field :slug, :type => String
  field :description, :type => String
  field :disabled, :type => Boolean, :default => true

  # Document associations
  embeds_many :chapters
  referenced_in :user
  
  # Document indicies and keys
  key :title, :user_id

  # Document validators
  validates_presence_of :title, :description
end
</pre>

This works as expected and I no longer get duplicate documents. The only issue that I am having right now is Mongoid does not seem to be correctly throwing for a second save which seemingly just creates another version with a timestamp in the future. Merely adding an explicit validator does not seem to help either. Other than that this solution seems to be up to snuff, but as always, I am sure there may be a more elegant way to handle this. Any thoughts? 
