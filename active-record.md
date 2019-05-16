# Active Record Associations
https://www.railstutorial.org/book/following_users

https://insiders.liveshare.vsengsaas.visualstudio.com/join?5E234E7217020B2DE143F8444563D60A6F26

***

### **- has_one**
One of the models in the given relation will have has_one method invocation and another one will have belongs_to. It is used to describe which model contains a foreign key reference to the other one, in your case, it is the profiles model.

```ruby
class User < ApplicationRecord       class Profile < ApplicationRecord
  has_one :profile                     belongs_to :user
end                                  end
```  
**has_one accociation manipulation.**

```ruby
# Create user record
user = User.create(name: "last thing")
# Create one profile for user
user.create_profile(name: "asdaS")
# Access users profile
user = User.last
user.profile
```

***

### **- has_one through**
**Logic**, OK it might sound a bit weak for this but it would be logical to say that "I have a supplier who has an account with me, I want to see the entire account history of this supplier", so it makes sense for me to be able to access account history from supplier directly.

**Efficiency**, this for me is the main reason I would use :through, simply because this issues a join statement rather than calling supplier, and then account, and then account_history. noticed the number of database calls?

using :through, 1 call to get the supplier, 1 call to get account_history (rails automatically uses :join to retrieve through account)

using normal association, 1 call to get supplier, 1 call to get account, and 1 call to get account_history

***

### **- has_many**
A one-to-many association is the most common used relation. This association indicates that each instance of the model A can have zero or more instances of another model B and model B belongs to only one model A.

```ruby
class User < ApplicationRecord       class Story < ApplicationRecord
  has_many :stories                     belongs_to :user
end                                  end
```
**has_many accociation manipulation.**

```ruby
# Create new user
user = User.create(name: "Pavan")

# To create story we have two options
user.stories.create(title: "Hello", body: "this is story")

# The below option just initiate the object of stories and we need to run user.save to save the record.
user.stories.build(title: "Hello1", body: "this is story")

# Get all the stories
user.stories

# Get all the ids of associated records
user.storie_ids

# Check if the collection contains any associated objects
user.stories.empty

# Get number of objects in collection.
user.stories.size

# Find objects within the collection, it finds the object by id.
user.stories.find(1)

# Checks whether an object meeting the supplied conditions exists in the collection.
user.stories.exists?(['name LIKE ?', "abc"])
```

***

### **- has_many through**
A has_many :through association is often used to set up a many-to-many connection with another model. This association indicates that the declaring model can be matched with zero or more instances of another model by proceeding through a third model. For example, consider a medical practice where patients make appointments to see physicians.

```ruby
class Physician < ApplicationRecord
  has_many :appointments
  has_many :patients, through: :appointments
end
 
class Appointment < ApplicationRecord
  belongs_to :physician
  belongs_to :patient
end
 
class Patient < ApplicationRecord
  has_many :appointments
  has_many :physicians, through: :appointments
end
```

**Manipulate has many through assocatiation**

```ruby
# Create physician with patient
physician = Physician.new(name: "ph1")
patient = Patient.new(name: "pt1")

# Create new patient for physician
physician.patients << Patient.find(params[:patient_id])

# When creating a new patient for a physicians:
physician.patients.create(params[:patient])

#You can also add via ids:
physician.patient_id << Patient.find(params[:patient_id])
```

***

### **- has_and_belongs_to_many**
We have two models in this app: a User model, and a Forum model. We want a user to be able to join many forums so they can participate in discussions, but each forum is also going to have many users, because you can't really have discussions in a forum that has just one user.  

**Create Join Table between Users and Forums**

```ruby
rails g migration CreateJoinTableUsersForums users forums
```

```ruby
class CreateJoinTableUsersForums < ActiveRecord::Migration[5.0]
  def change
    create_join_table :users, :forums do |t|
      t.index [:user_id, :forum_id]
      t.index [:forum_id, :user_id]
    end
  end
end
```

```ruby
class User < ApplicationRecord
  has_and_belongs_to_many :forums
end

class Forum < ApplicationRecord
  has_and_belongs_to_many :users
end
```

**Manipulate has_and_belongs_to_many association**

```ruby
# Find existing user
user = User.find_by(name: "Pavan")
# Add user to fourm
user.forums << Forum.find_by(name: "Ruby")
user.forums << Forum.find_by(name: "SQL")
# See result
pp user.forums
```
***Note: You should use has_many :through if you need validations, callbacks or extra attributes on the join model.***  

***

### **- Polymorphic Association**

A model can belong to more than one other model, on a single association

[# Rnderstanding Polymorphic Associations in Rails](https://launchschool.com/blog/understanding-polymorphic-associations-in-rails)
[# Rails Techniques: Using Polymorphic Associations](https://semaphoreci.com/blog/2017/08/16/polymorphic-associations-in-rails.html)
[# 4 Ways to Model Polymorphic Associations in Rails 5](https://medium.com/@adamlangsner/4-ways-to-model-polymorphic-relationships-in-rails-5-4c98101ed900)

**Example**
Create models required to simulate the polymorphic association.
```bash
$ rails g model Event name:string
$ rails g model Restaurant name:string
$ rails g model Review review:text
$ rails g migration AddReviewableToReview reviewable:references{p
olymorphic}
```
app\models\review.rb
```ruby
class Review < ApplicationRecord
  belongs_to :reviewable, polymorphic:  true
end
```
app\models\concerns\reviewable.rb
```ruby
module Reviewable
  extend  ActiveSupport::Concern

  included do
    has_many :reviews, as:  :reviewable
  end
end
```
app\models\event.rb
```ruby
class Event < ApplicationRecord
  include  Reviewable
end
```
app\models\restaurant.rb
```ruby
class Restaurant < ApplicationRecord
  include  Reviewable
end
```    
**Try It**
```console
> event = Event.create(name: "Event_1")
> restaurant = Restaurant.create!(name: "Restaurant_1")
> r1 = Review.create!(review: "Review 1", reviewable: event)
> r2 = Review.create!(review: "Review 2", reviewable: restaurant)
> event.reviews
> restaurant.reviews
```
***  
### **- STI( Single Table Inheritance )**
Sometimes, you may want to share fields and behaviour between different models. Let's say we have Car, Motorcycle and Bicycle models. We will want to share the `color` and `price` fields and some methods for all of them, but having some specific behaviour for each, and separated controllers too.

```console
// Generate model with fields, make sure the type column is present in parent table otherwise STI will not work.
$ rails generate model vehicle type:string color:string price:decimal{10.2}

// Create child model which inherited from parent.
$ rails generate model car --parent=Vehicle`
```
```ruby
class Car < Vehicle
end
```

```console
// Access car objects

Car.create(color: 'Red', price: 10000)
Car.all
```

