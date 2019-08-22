# Class and Modules

A class is a blueprint from which objects are created. The object is also called as an instance of a class.

# Validation helpers

- acceptance
- validates_associated
- confirmation
  Used when two fields received same value
- exclusion
  Exclude the values given in array
- format
  Used with regex
- inclusion
  Check the value in array and respond with array, like size is not valid size
- length
- numericality
- uniqueness
- presence

# Active record callbacks

- Creating an Object

before_validation
after_validation
before_save
around_save
before_create
around_create
after_create
after_save
after_commit/after_rollback

- Updating an Object

before_validation
after_validation
before_save
around_save
before_update
around_update
after_update
after_save
after_commit/after_rollback

- Destroying an Object

before_destroy
around_destroy
after_destroy
after_commit/after_rollback


# Design pattern in ruby
In software engineering, a software design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. Design patterns are formalized best practices that the programmer can use to solve common problems when designing an application or system.

It is basically used to structure the code.

It is also called as GoF in ruby.

Examples are:

# API application

rails new todos-api --api -T

- Create directory in app/controller/api
  All controllers goes inside this directory

- Define routes like
```ruby
namespace :api do
  namespace :v1 do
    resources :people
  end
end
```

- Controller
```ruby
class API::V1::PeopleController < ApplicationController

end
```

- Respond
```ruby
respond_to do |format|
  format.json { render :json => @people }
end
```
