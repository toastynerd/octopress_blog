---
layout: post
title: "MongoDB and Rails"
date: 2013-06-10 11:06
comments: true
categories: RoR
---
Today we're trying to use a trendy database(MongoDB) with a trendy framework(Ruby on Rails) and we seemed to have left our skinny jeans at home. Cheap shots at hipsters aside. let's talk about how we can put these two together and why we should care and maybe your humble author will stop using the "royal we" as we take this journey. Damn, I did it again, didn't I?

I'm going to assume that you are somewhat familiar with Ruby on Rails. By that, I mean, you know how to get an application up and running. You're familiar with MVC architecture and how the basic parts of Rails fit together. I also assume that you have some reason to be interested in MongoDB but aren't really sure how it fits into Rails or why you would want it to fit into Rails.

MongoDB, you've heard about it, you know it's beginning to get popular, but wtf is it? MongoDB is one of many up and coming nonrelational or noSQL databases. MongoDB differs from a traditional SQL database in two major ways. First, it's slightly faster and second, it provides a much more flexible way to store and retrieve your data.

These two benefits both stem from the way in which MongoDB stores data. MongoDB stores all its data in the form of BSON documents, which are like JSON documents but faster and bigger. They consist of key-value pairs and those values can be anything from an integer, to a string, to an object, to another BSON document. SQL stores it's data in tables that are consistent, organized and capable of being rolled back, or reverted to a previous state. When you insert a new piece of data into a MongoDB database it throws it wherever it can find room and indexes it if you have an index, when you perform an insert on an SQL database you have to, at the very least, find the end of the current data and append the new data onto it. Or find a spot for it in the current data set. The difference in speed is only dramatic when manipulating documents that number in the 1000 plus range, which is one of the reasons that MongoDB falls under the category of "Big Data". If you want more information about MongoDB I would suggest checking out their site <a href="http://mongodb.org">here</a> or taking one of their free online classes <a href="&quot;http://education/10gen.com">here</a>.

So why would you want to to use it with Rails besides the performance increase? Well, one bonus, it gets rid of the need for migrations. That's right, never again will you spend hours slamming your head against a wall trying to figure out why your tests aren't passing only to find out you never ran rake db:migrate &amp;&amp; rake db:test:prepare. The flexible way in which Mongo stores data means that new schemas are created on the fly(MongoDB itself is schema-less but Rails creates a schema for you). A downside to this is that your old data won't contain your new schema so you can't just assume that it will be there. The other upside is really only relevant in a production piece of software, Mongo database administration feels a lot more writing code than dba. All commands for Mongo can be administered through javascript so it's easier for someone who comes from a development background to get some dba taken care of. I guess this is more of a preference thing than an actual, tangible benefit but hey, it's my preference so you get to hear about it. Enough of the why, let's get to the how.

First, you'll need to install MongoDB. I'm not going to give instructions on how to install the Mongo server on every platform but you can find the install docs <a href="http://docs.mongodb.org/manual/installation/">here.</a> Just a quick security tip, if you're running the Mongo server on your dev machine and don't intend to use it elsewhere, add the following line to your mongo config file.
<pre>bind 127.0.0.1</pre>
This will ensure that your mongo server is only accessible through your machine, so the next time you're working from a coffee shop you don't have to worry about someone pushing 100 gigs of data to your mongo server. To ensure your server is up and running just run the command "mongo" if you get a prompt, you're good to go.

Next, you need to create a new rails app. MongoDB doesn't use active record as active record is based on SQL databases, so make sure to create your new rails app as follows:
<pre>rails new  --skip-active-record</pre>
This will get rid of most of the active record that a new Rails application contains. Make sure to go into config/application.rb and remove or comment out all the lines that being with config.active_record, there will probably be two or three.

Next up is getting the right gem to interact with mongo through rails. In my research, I've only found two viable candidates, <a href="http://mongomapper.com/">mongo_mapper</a> and <a href="http://mongoid.org/en/mongoid/index.html">mongoid</a>. They both have great documentation, work well with rails and do a decent job of replicating the same functionality as active record but I like Mongoid better because it requires little to no additional configuration to work with rspec and devise. Just add
<pre>gem 'mongoid', '~&gt;3.0.0'</pre>
Then run bundle install. Next, you'll need to create a configuration file for the MongoDB database.
<pre>rails generate mongoid:config</pre>
This will create the mongoid version of database.yml, config/mongoid.yml. If you're running the mogno database off of your development machine the default configuration should work but this is the file to edit when that changes.

Now mongoid is set up and ready to go. You can start generating models with the same commands you normally would but if you're trying to create them from scratch, or if you're like me and you frequently have typos in your generate commands you'll notice some differences in you model files.
<pre>class MyModel
  include Mongoid::Document
  field :name, type: string

  validates_presence_of :name
end</pre>
The first noticeable difference, and one you probably could have predicted is that the model class doesn't inherit from active record. Instead, you include Mongoid::Document within the model class.

The contents of the model itself are also different. Instead of the usual syntax which corresponds to SQL table columns we have what translates into key/value pairs. On the third line we have field :name, type: string. The field :name corresponds to a key of "name" and value that will be of type string. You can read about all the different variable types included with Mongoid in their documentation but it does include all of the types included with active record. You can also embed other models within models but that is a little beyond the scope of this blog post. The other thing to notice is that the validation syntax is slightly different, once again, you can read all about the different validation types in the Mongoid documentation but they're essentially the same.

Now that we've taken a look at the models lets take a look at something equally important, testing with rspec. You can install rspec in the same manner, put the gem in your gemfile then bundle install and rails g rspec:install. But it requires a little bit more configuration afterwards. First off, there are a few lines you have to change in spec_helper.rb, read through the comments in that file and comment out the the lines that rspec tells you to comment out if you're not using active record. These should be the two lines that mention fixture and transitional_fixtures.

Next there are a few lines you will want to add in your spec_helper in order to keep from getting weird errors due to duplicate data, add the following to the end of your spec_helper file.
<pre>Mongoid.purge!
Mongoid::IdentityMap.clear</pre>
These two lines will clear out your test database before running your tests. Normally when you run rspec tests it rolls back the database before running the tests but MongoDB doesn't support rollbacks. Without these two lines, every test you run will fill your database with unwanted entries.

That's essentially it, from here you can develop your rails app as if nothing were different, and when you want more control over your data or want to embed a document within a document you have that ability. Quick side note, if you're using devise, make sure you use rails generate mongoid:devise user instead of rails generate devise user. Have fun experimenting with mongo and rails!

-Tyler Morgan

@toastynerd