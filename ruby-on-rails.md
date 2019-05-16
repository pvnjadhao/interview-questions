### How to scale rails application? 

Application scalability is how many user requests application handles per minute. There are two types of scalabilities. Vertical Scalability and Horizontal Scalability. 

**Vertical Scalability with Ruby on Rails**

Vertical scaling means adding more RAM, upgrading the server’s processor, etc. You can give your servers computer more power. 

**Horizontal Scalability with Ruby on Rails**

Horizontal scaling means converting the single server architecture of your app to a three-tier architecture, where the server and load balancer (Nginx), app instances, and database instances are located on different servers. In such a way, we allocate equal and smaller loads among machines.
***

### Server-side caching and Client-side caching 

Caching means storing the result of complex computation in some storage and later returning them without re-computing everything. We can achieve caching in rails using five ways. 

**Model or Low-level caching**

The idea behind the low-level caching is we can catch the result of complex query and return without re-running the same query over and over again. Rails automatically uses this type of caching but only for the same queries performed in the same controller action. After action finishes its job the cached data is no longer available. So, to get advantage to this caching method we need long-term storage. Rails core has necessary methods to read and write cached data. There are three methods to do that.  

```ruby
Rails.cache.write 'some_key', 5 # => true 

Rails.cache.read 'some_key' # => 5 

Rails.cache.fetch('some_other_key') { 50 + 50 } #=> 100 (saved to cache) 

Rails.cache.fetch('some_other_key') { 50 + 50 } #=> 100 (fetched from cache)
```

The read and write methods are simple to use. The fetch method complex it tries to find value with the key if it doesn’t it will write the data and return that data as a result. 

In this method if the record is changed or modified, we need to flush the cache manually.  

```ruby
Rails.cache.delete 'all_employees' 
```
 

**Fragment caching**

The fragment caching used to cache only the part of page. It is pretty popular and handy. Using it can be very simple just wrap code of view inside the catch method. 

```irb
<% cache employee do %> 

<% end %> 
```

**Action caching**

**Page caching**

**HTTP caching**

***

### What is cucumber? 

Cucumber is a tool used for testing application. It runs automated tests written in a behavior-driven development (BDD) style. I automatically launch the browser and perform actions provided in script like user.
***

### What is static and dynamic scaffolding? 

Dynamic Scaffolding is used to give the model name that is being used with the function like ```scaffold: model_name```. It automatically generates the entire content and user interface at runtime. It doesn’t require the database to be integrated as it gets created in runtime. It allows the generation of new, edit and deletes methods for the use in application. 

Static Scaffolding requires manual entry in the command. 
```bash 
$ rails generate scaffold Post title: string content:text category_id: integer 
```

It requires the insertion of the command to, generate the data with their fields. It requires the database to, be migrated.  
***

### Mention what are the positive aspects of Rails? 

Rails provides many features like 

**Meta-programming:**
Rails uses code generation but for heavy lifting it relies on meta-programming. Ruby is considered as one of the best programming languages for Meta-programming. 

**Active Record:**
It saves object to the database through Active Record Framework. The Rails version of Active Record identifies the column in a schema and automatically binds them to your domain objects using metaprogramming. 

**Scaffolding:**
Rails have an ability to create scaffolding or temporary code automatically 

**Convention over configuration:**
Rails does not require much configuration like other development framework, if you follow the naming convention carefully. 

**Three environments:**
Rails comes with three default environment testing, development, and production. So, we can test the application in three different environments while development. 

**Built-in-testing:**
Rails comes with build-in testing suit which help us to write TDD tests.
***

### Explain what is ORM (Object-Relationship-Model) in Rails? 

ORM or Object Relationship Mapper it helps to map classes to the table in the database, and objects are directly mapped to the rows in the table. It’s a DSL (Domain Specific Language) designed to work with the database directly from rails application. We don’t need write SQL queries manually on database level. ORM handles it out of the box.
***

### List out what can Rails Migration do? 

Rails Migration can do following things 

* Create table
* Drop table
* Rename table 
* Add column
* Rename column 
* Change column
* Remove column and so on 
***

### What is callbacks in rails? 

Callbacks are methods that get called at certain moments of an object's life cycle. With callbacks it is possible to write code that will run whenever an Active Record object is created, saved, updated, deleted, validated, or loaded from the database. 

* before_validation 
* after_validation 
* before_save 
* around_save 
* before_create 
* around_create 
* after_create 
* after_save 
* after_commit/after_rollback 
***

### What are filters?

Filters are methods that are run before, after or “around” a controller action. 

Filters are inherited, so if you set a filter on ApplicationController, it will be run on every controller in your application. 

[Read More...](https://railskey.wordpress.com/2011/09/03/rails-filters-before-after-and-around-filters/)

***

### What is an active Record? 

Rails Active Record is the Object/Relational Mapping (ORM) layer provided by Rails. It follows the standard ORM model, like 

* Tables map to classes, 

* Rows map to objects and 

* Columns map to object attributes. 

Rails Active Records provide an interface and binding between the tables in a relational database and the Ruby program code that manipulates database records. Ruby method names are automatically generated from the field names of database tables. 

Each Active Record object has CRUD (Create, Read, Update, and Delete) methods for database access. This strategy allows simple designs and straight forward mappings between database tables and application objects.

```bash
$ rails generate model <model name> fields <name: datatype>
```

```ruby
class Book < ApplicationRecord
  # Data manipulation code
end
```

### What is Observer and Callback in rails?

**Rails Callback**
Callbacks are methods that get called at certain moments of an object’s life cycle. That means that it can be called when an object is created, saved, updated, deleted, validated, or loaded from the database.

A callback is more short lived. And you pass it into a function to be called once. 

**Rails Observers**
Observer is similer to Callback but it is used when method is not directly related to object lifecycle. The other difference is an observer lives longer and it can be attached/detached at any time. There can be many observers for the same thing and they can have different lifetimes. 
The best example of Observer is that it could be “send registration confirmation emails” As we can argued that a User model should not include code to send registration confirmation emails so we will create observer for this.

