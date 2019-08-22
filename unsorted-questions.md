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
