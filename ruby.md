### What is the difference between proc and lambda? 

Lambda returns itself, Proc does not returns from the method body. 

Lambda does complain about arguments, Proc does not.  

```ruby
Proc.new { |n| puts '#{n}!' } 
```

```ruby
lambda (a) { a }.call 
```  

[Read more....](https://blog.appsignal.com/2018/09/04/ruby-magic-closures-in-ruby-blocks-procs-and-lambdas.html)
***

### What is the class method and object method? 

Class methods are bind to itself, we cannot call class methods using the object. 

Object methods are bind to a particular object of that class; we cannot call object method using Class directly.
***

### Difference between include and require in ruby?

It reads the file from the file system, parses it, saves to the memory and runs it in a given place. What does it mean? Simply, even if you change the required file when the script is running, those changes won't be applied - Ruby will use the file from memory, not from the file system. 

Include used to include or mix the module methods inside the class. So, we can use those methods from that module inside that particular class.
***

### How do we achieve multiple inheritance in ruby? 

Ruby does not have multiple inheritance. Ruby has something similar called mixins which can be implemented using Modules. 

Mixins are not multiple inheritance, but instead mostly eliminate the need for it. 

To answer your question, when you include two modules in a class and both of them has the method with same name (in your case, method a), in that case, a method from the 2nd (the last one) Module will be called. 

```ruby
module A 
  def a1   
    puts "I am defined in A"
  End 

  def a2 

  End 
end 

module B 
  def a1
    puts "I am defined in B"
  end
  
  def b2
  end
end
```
```ruby
class Sample
  include A
  include B
  
  def s1
  end
end

samp = Sample.new
puts samp.a1

# I am defined in B
```
****

### How to remove nil from an array? 
Returns a copy of self with all nil elements removed.

```ruby
[1, 2, 3, nil, nil].compact 
```
***

### Can you call a private method outside a Ruby class using its object? 

Yes, with the help of the send method. 

```ruby
class Foo
  def Foo.bar(my_instance, n) 
    my_instance.send:plus, n)
  end
end
```
***

### Given the class Test: 

```ruby
class A 
  def self.a(b) 
    if b > 0 
      b * b 
    end 
  end 
end 
```

What will be the values of: 

```ruby
var1 = A.a(0) 
var2 = A.a(2) 
```
```bash
Nil 
4
```
***

### What is meta programming? 

Metaprogramming is a dynamic nature of programming language. It allows you to define and redefine methods and classes at runtime which are not already exist. Means write a code that write code itself dynamically at runtime. 

Suppose you have a class Car and Car has a property like model, price and top speed. If we want to set these properties from outside class, then we need define getters and setters' methods with this approach the code become larger and larger. Ruby provides built in methods to generate getter and setter methods like ```attr_writer```, ```attr_reader``` and ```attr_accessor``` with the help of these methods we can easily set the properties of class. Here is the concept of metaprogramming comes in. The ```attr_writter```,  ```attr_reader``` and ```attr_accessor``` methods generate getters and setter methods for us dynamically. 

[Read More...](http://rubylearning.com/blog/2010/11/23/dont-know-metaprogramming-in-ruby/)
***

### What is multithreading in ruby? 

Traditional programs have a single thread to execute the statement of program sequentially, one statement at a time. A multithreaded program has more than one thread of execution. Within each thread, statement executed sequentially but the thread executed in parallel. A thread is like a lightweight sub-process to divide the one large process in small units.  

In Ruby we have a Thread class to write multithreaded programs. Ruby threads are lightweight. To write the multithread program we need to create the instance of Thread class and associate the block with it. 

**What is multithreading?**

The process of executing multiple threads simultaneously. 

**What is a Thread?**

A lightweight sub-process which handles the smallest unit of processing. 

**Advantages of Multithreading:**

* Threads are independent so it won’t block users. 

* Many operations can be performed so it saves more time. 

* It shares the same memory
***

### Mention what the difference is between false and nil in Ruby?

In Ruby False indicates a Boolean datatype, while Nil is not a data type, it has an object id 4. 
***

### Mention what is the naming convention in ruby? 

* Class names are CamelCase.
* Methods and variables are snake_case. 

### Explain what is "yield" in ruby? 

A Ruby method that receives a code block executes it by calling it with the “Yield”. 
***



