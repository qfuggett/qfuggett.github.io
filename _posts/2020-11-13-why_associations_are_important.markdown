---
layout: post
title:      "Why Associations Are Important"
date:       2020-11-13 19:10:50 +0000
permalink:  why_associations_are_important
---


As a Software Developer, I will probably spend most of my time fixing bugs and maintaining code that others have written. However, there may be moments where I will want to build something "from scratch" and create something entirely new. During this process, it's important for me to use design patterns that make the creation process as simple as possible. 

In Object-Oriented programming languages, we are able to organize our code into "objects" that focuses on handling and manipulating data. Therefore, I'm going to want to have easy access to where the data is stored (in a database) and will want to be able to structure the data in a way that is easy for other developers to understand - this is where Active Record (available in Rails) is helpful.

We also have SQL, a query language used for managing data in a database - it literally handles the data within the rows and columns of the database. ActiveRecord provides an interface between the database and the Ruby code that uses the data. In order to avoid manually writing tons of SQL operations to manage and manipulate the data, ActiveRecord does this for me! Thus, we create models (Ruby classes), that talk to the database and are able to store and validate data.

**ActiveRecord** has many different features, but I'll briefly cover Associations, which are really helpful! They save us time on writing code that creates connections between two models. There are six types of associations:

`belongs_to`   
`has_one`   
`has_many`   
`has_many :through`   
`has_one :through`   
`has_and_belongs_to_many`

Each association is a **macro** - which means that it writes code on our behalf to accomplish something. When declaring an association in a model, depending on the association, the class gains a number of different methods. For example the `has_many` association comes with 17 different methods that can now be used! Every instance of the model now has access to (collection representing the model):

`collection`   
`collection<<(object, ...)`   
`collection.delete(object, ...)`   
`collection.destroy(object, ...)`   
`collection=(objects)`   
`collection_singular_ids`   
`collection_singular_ids=(ids)`   
`collection.clear`   
`collection.empty?`    
`collection.size`   
`collection.find(...)`   
`collection.where(...)`   
`collection.exists?(...)`   
`collection.build(attributes = {}, ...)`   
`collection.create(attributes = {})`   
`collection.create!(attributes = {})`   
`collection.reload`   


Let's say I wanted to create a web-page for a soccer player that wanted to log their awards/accomplishments. I would create a model:

`class Player < Application Record`   
  `has_many :awards`   
`end`   


So, if I wanted to know how many awards my socer player has, I could do this:

`@awards_count = @player.awards.size`

Now, I can just call on `@awards_count` whenever I need to show this number!


***Remember***, ActiveRecord fires off the SQL needed to access the database on our behalf. So that looks something like this:

`SELECT COUNT(*) FROM "awards" WHERE "awards"."player_id" = ?  [["player_id", "3"]] => 4`

**I see that my soccer player has 4 awards! **

The `has_many` association created a connection between a specific player and the awards that belong to them by assigning a value to `player_id`. An example of an award would look something like this in the console:

`#<Award:0x00007fa28e2ba4c0  id: 2, name: "Fastest on Field", date_earned: "01022018", player_id: "3">`**

The award has it's own identifying id of 2, but also a player_id of 3 that associates it with my player. Therefore, my player would also have a corresponding id of 3. 

**Using `has_many`, this creates the association between the two!**

There are so many more associations that we can use in our code to make important connections between models in order to manipulate and handle their data. ActiveRecord helps us spend less time on the small things in order focus more on the more complex pieces of the application. 




