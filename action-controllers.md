### What is an action controller in rails? 

Action Controllers are the core of a web request in Rails. They are made up of one or more actions that are executed on request and then either it renders a template or redirects to another action. An action is defined as a public method on the controller, which will automatically be made accessible to the web-server through Rails Routes. 

By default, only the ```ruby ApplicationController ``` in a Rails application inherits from ActionController::Base. All other controllers inherit from ApplicationController. This gives you one class to configure things such as request forgery protection and filtering of sensitive request parameters. 
