---
layout: post
title:      "RAILS API WITH JAVASCRIPT FRONTEND PROJECT"
date:       2020-04-19 05:04:51 +0000
permalink:  rails_api_with_javascript_frontend_project
---


After finishing the JavaScript module, we were expected to build our fourth project which is a single page application which constitutes a JavaScript frontend with a rails backend. All interactions between the client and the server must be handled asynchronously (AJAX) and use JSON as the communication format. AJAX is the shortened version of "asynchronous JavaScript and XML," and it's the general way we make requests to the server without reloading the web page, and then work with data we receive from the server. We can use the method called fetch() to accomplish this. The data that comes back from the server is not sent in HTML. While (once) sent back in XML, it's now most-often sent back in a format known as JSON ("Jay-Sawn"). JavaScript Object Notation (JSON) is a String that JavaScript knows how to turn into an Object.


I decided to build a simple app where users can add, edit, and delete riddles. So, a user has many riddles and a riddle belongs to a user.

Here are the steps I followed:

First foremost, I created a directory called rails-riddles-api and then created the backend using `rails new riddles-backend  - -api ` which will accomplish the following:
	
•	Configure your application to start with a more limited set of middleware than normal. Specifically, it will not include any middleware primarily useful for browser applications (like cookies support) by default.
•	Make ApplicationController inherit from ActionController::API instead of ActionController::Base. As with middleware, this will leave out any Action Controller modules that provide functionalities primarily used by browser applications.
•	Configure the generators to skip generating views, helpers, and assets when you generate a new resource.
	Then I ran `bundle install’ after uncommenting “gem rack-cors” which will provide  support for Cross-Origin Resource Sharing (CORS) for Rack compatible web applications. I accessed the cors.rb file located in config/initializers directory to uncommented the following:


```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

This will allow GET, POST or OPTIONS requests from any origin on any resource.


I removed .git using `rm -rf .git` from the backend as I wanted one repository for both my frontend and backend. I used the command `git init` in the main directory(rails-riddles-api) to create new Git repository.


	After changing back into backend directory(riddles-backend), I setup scaffold for user and riddle:
```
rails g scaffold user name email password_digest 
```

```
rails g scaffold riddle content:text answer:text user:belongs_to
```

This gave me models migration for that models and controllers to manipulate the models. I made sure I added has_many relationship to the User model. After which I added some validations:

```
class User < ApplicationRecord
    has_many :riddles

    validates :name, presence: true, uniqueness: true
end
```

```
class Riddle < ApplicationRecord
  belongs_to :user

  validates :content, presence: true
  validates :answer, presence: true
end
```



I created some riddles and a user in seed.rb and then ran `db:migrate` and `db:seed` and made sure that the seed data was properly created by using  rails console.

```
Rails.application.routes.draw do
  scope :api do
    resources :riddles
    resources :users
  end
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

This will change the resources path, for example:     riddles#index   =>riddles GET    /api/riddles(.:format)   


The next step was to create a frontend directory – “riddles-frontend” in which I created the following folders and files:
        
Riddles-frontend>    src>
                                                >models
                                                      >riddle.js
                                                 >services
                                                      >api.js(to make fetch()requests)
                                        >index.js
                                       >stylesheets
                                                    >main.css
                                      >index.js



As I added code to each of these files, I accessed the index.html in the browser to test out the code.

