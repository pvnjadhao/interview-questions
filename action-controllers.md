### What is an action controller in rails? 

Action Controllers are the core of a web request in Rails. They are made up of one or more actions that are executed on request and then either it renders a template or redirects to another action. An action is defined as a public method on the controller, which will automatically be made accessible to the web-server through Rails Routes. 

By default, only the ```ApplicationController``` in a Rails application inherits from ```ActionController::Base```. All other controllers inherit from ```ApplicationController```. This gives you one class to configure things such as request forgery protection and filtering of sensitive request parameters on place. 

```bash
$ rails generate controller <controller name> <actions>
```

```ruby
class HomeController < ApplicationController
  def index; end
end
```

### Mention what is the role of Rails Controller? 

The Rails controller is the logical center of the application. It facilitates the interaction between the users, views, and the model. It also performs other activities like 

* It is capable of routing external requests to internal actions. It handles a URL extremely well 

* It regulates helper modules, which extend the capabilities of the view templates without bulking of their code 

* It regulates sessions; that gives users the impression of an ongoing interaction with our applications 
