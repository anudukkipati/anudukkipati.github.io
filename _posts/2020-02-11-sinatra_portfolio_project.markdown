---
layout: post
title:      "Sinatra Portfolio Project"
date:       2020-02-11 18:45:28 +0000
permalink:  sinatra_portfolio_project
---

As we reach the end of Sinatra module, we were expected to build a Sinatra project which will be a CRUD(create, read, update, delete), MVC(models, views, controllers) app. I decided to build a Book Reviews app that allows a user to sign up, login, logout, add book reviews and allows a user to edit and delete their own book reviews. So I would have two models, a user model and a book_review model. 

*Object Relational Mapping*, commonly referred to as its abbreviation ORM, is a technique that connects the rich objects of an application to tables in a relational database management system. Using ORM, the properties and relationships of the objects in an application can be easily stored and retrieved from a database without writing SQL statements directly and with less overall database access code. I used *Active Record* to achieve all the above.

*Here are the steps I followed*:
* First and foremost, I needed a file structure that I needed to start building this project and I could accomplish this by running `gem install corneal` (which is a Sinatra App generator - https://github.com/thebrianemory/corneal) and then ran `corneal new Sinatra-book-review`. This not only gave the file structure, but also config file, gemfile, config.ru files with code already written for me.

* Then I installed all the gems needed by running `bundle install`.

* The next step is to create tables for my database, so I ran `rake db:create_migration NAME=` to create two tables, namely, create_users and create_book_reviews. I defined the “change” method in both the files to create the tables.

```
def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.string :password_digest
      t.timestamps null: false
    end
  end
end
                  
def change
    create_table :book_reviews do |t|
      t.string :title
      t.string :content
      t.string :image
      t.string :user_id
      t.timestamps null: false
    end
  end
end

```



* Then I ran migrations by running `rake db:migrate`.

* I added the corresponding models and associated them using active record associations belongs_to and has_many.

* Next was to set up controllers and views part of MVC. I created 3 controller files, namely, application_controller, user_controller, and book_reviews controller to set up the routes for my app. I followed the* RESTful routes convention*( A RESTful route is a route that provides mapping between HTTP verbs (get, post, put, delete, patch) to controller CRUD actions (create, read, update, delete)). As HTML Forms only support GET and POST requests, to perform other actions such as PUT, PATCH or DELETE, I had to use *Rack::MethodOverride middleware *which is included in Rack.

* I created views to display forms, book_reviews etc.

* And I made sure my app validates user input. I included has_secure_password method in user model which will authenticate against a Bcrypt password. I used the active record helper method “presence” to ensure the specified attributes are not empty. 

As I added my routes, I tested the routes by running shotgun to start up my server.

I used Sinatra-Flash to display success or failure messages when a user logs in or signs up or tries to add a book review.

Finally, I used bootstrap to style my app.

References: https://guides.rubyonrails.org/active_record_basics.html

