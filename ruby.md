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





