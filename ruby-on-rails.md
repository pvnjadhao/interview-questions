### How to scale rails application? 

Application scalability is how many user requests application handles per minute. There are two types of scalabilities. Vertical Scalability and Horizontal Scalability. 

**Vertical Scalability with Ruby on Rails**

Vertical scaling means adding more RAM, upgrading the server’s processor, etc. You can give your servers computer more power. 

**Horizontal Scalability with Ruby on Rails**

Horizontal scaling means converting the single server architecture of your app to a three-tier architecture, where the server and load balancer (Nginx), app instances, and database instances are located on different servers. In such a way, we allocate equal and smaller loads among machines.
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

### 
