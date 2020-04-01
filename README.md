# Rails Review

For each of the following topics, please answer each of the questions. You can use links and images to support your answer. Once done please make a pull request.

## Has many Through

- [Rails Active Record Intro](https://github.com/sei-entropy/lesson-w11d02-rails-active-record#active-record-associations)
-[Hospital App](https://github.com/sei-entropy/hw-w11d02-rails-hospital)

### Questions

1. What is the role of a join table in a many-to-many relationship?
      Its purpose is to store a record for each of the combinations of these other two tables
2. What two columns must be present in a join table?
      foreign_key of the two columns

3. Given the example below, edit the code to define a has many :through relationship.

    ```ruby
    class Customer < ActiveRecord::Base
    has_many :purchases
    has_many :products, through: :purchases
    end

    class Product < ActiveRecord::Base
    belongs_to :customer
    belongs_to :purchase 
    end

    class Purchase < ActiveRecord::Base
     has_many :products
     has_many :customers, through: :products
    end
    ```


4. Based on #3, give an example of associating two instances via the join model.



## Devise

- [Devise Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-devise)

### Questions

1. What does the `current_user` method that the Devise gem provides?
returns the model class relating to the signed in user.
2. What does the `authenticate_user!` method that the Devise gem provides?
ensures a logged in user is available to all, or a specified set of controller actions.

3. Write a signout link using the `link_to` rails helper and a devise path.

<% if current_user %>
<%= link_to "sign in ", sign_in_path %>
4. How do I generate a devise model in the terminal?
rails generate devise User

5. What are the trade offs for using a gem for authentication over a handrolled solution? (no real right answer)

 It provides an easy-to-use authentication solution

## Validations

- [Validations Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-model-validations)

### Questions

1. Which component, of Rails MVC, is responsible for the business logic?
      Model

2. Assume the user's age is an optional field.  Write the validation to verify that a User's age is between 13 and 125 (inclusive).
    validates :age { in: 13..125 }

3. What would `user.errors.messages` return (for the above User), if you assigned `user.age = 12`?

not allowed less than  13

4. Assume you visit "/customers/new" and enter some invalid information.  Given this controller code, what url would your browser be on after pressing "Create Customer"?

``` ruby
class CustomersController < ApplicationController
  def new
    @customer = Customer.new
  end

  def create
    @customer = Customer.new(customer_params)
    if @customer.save
      redirect_to customer_path(@customer)
    else
      render :new
    end
  end
  ...
  private
  def customer_params
    params.require(:customer).permit(:first_name, :last_name, :age)
  end
end
```


5. Give one reason why we might have the similar validations in the browser, model, and database layer of our application.

to prevent unwanted data to store in our database
