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

### 
