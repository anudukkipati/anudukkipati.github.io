---
layout: post
title:      "Rails Portfolio Project"
date:       2020-03-21 17:01:01 +0000
permalink:  rails_portfolio_project
---


For the rails portfolio project, I was required to build a project using Ruby on Rails framework. Our models had to include belongs_to, has_many, and has_many through relationships. And I was required to implement an authentication system which allows users to login from some other service like Facebook or Google etc. I decided to make an app where users can add their favorite poems or their own poems and have a conversation about the poems.

Here are the steps that I followed:

I used the rails new generator `rails new FavoritePoems` which gave a file structure that I could work with.

I added the omniauth, dotenv-rails and omniauth-google-oauth2 gems to the gem file as I needed to implement authentication system so that users can login using another service like google. I made sure Bcrypt gem is available for password authentication. I ran `bundle install` to install all the gems.

I decided to use the resource generator as it doesn’t create too much of a code bloat. I used it create Poem, User and Comment resources. Then I checked to see if my tables and models were created the way I wanted.
```
ActiveRecord::Schema.define(version: 2020_03_16_055610) do

  create_table "comments", force: :cascade do |t|
    t.text "content"
    t.integer "user_id", null: false
    t.integer "poem_id", null: false
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["poem_id"], name: "index_comments_on_poem_id"
    t.index ["user_id"], name: "index_comments_on_user_id"
  end

  create_table "poems", force: :cascade do |t|
    t.string "title"
    t.text "content"
    t.integer "user_id", null: false
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["user_id"], name: "index_poems_on_user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "email"
    t.string "password_digest"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.string "name"
  end

  add_foreign_key "comments", "poems"
  add_foreign_key "comments", "users"
  add_foreign_key "poems", "users"
end

```

Then I ran rails db:migrate and added validations to my models.

```
class Poem < ApplicationRecord
  belongs_to :user
  has_many :comments, dependent: :destroy
  has_many :users, through: :comments
  validates :content, :title, presence: true

end

```

After which I set up the root route and the signup, login & logout routes. And set up the controllers (users, sessions, poems, comments controllers). As I was building the controllers, I created the views as needed. 

Finally, I configured omniauth so that users can sign in using google.

And I used Bootstrap to style my project.

