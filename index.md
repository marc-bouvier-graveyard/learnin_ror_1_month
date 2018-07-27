# Learning Ruby on Rail in 1 month
My attempt to learn ruby on rails in 1 month.

## 2018-07-25

* [Ruby on Rails official site](https://rubyonrails.org/)

Tour of the framework
<iframe width="560" height="315" src="https://www.youtube.com/embed/OaDhY_y8WTo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

* [The rails Doctrine](https://rubyonrails.org/doctrine/)

## 2018-07-26
Todo Next : explicit why I want to learn ruby on rails and what I want to do with it.
### What do I want? 

I want to be able to create working applications fast that I can use at home to control several scripts.
I want to be able to create MVP fast when I have an interesting idea.

Deconstruct learning
* Bootstrap
* be able to update and customize
* learn conventions
* deploy
* scale

### Starting up

* [Getting started](https://guides.rubyonrails.org/getting_started.html)

Rails requires Ruby version 2.2.2 or later
```
> ruby -v
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-gnu]
```

Check sqlite3 version
``` 
> sqlite3 --version
3.22.0 2018-01-22 18:45:57 0c55d179733b46d8d0ba4d88e01a25e10677046ee3da1d5b1581e86726f2alt1
```

Install rails
```
sudo gem install rails
```

Check Rails is installed
```
> rails --version
Rails 5.2.0
```

Can ruby on rails be used with neo4j? [Yes ! ](https://neo4j.com/developer/ruby-course/)

Start the server
```
bin/rails server
```

The site can be found at [http://localhost:3000](http://localhost:3000).

## 2018-07-27

Continuing blog tuto...

Generate a controller called "Welcome" with an action "index"
```
> bin/rails generate controller Welcome index
Running via Spring preloader in process 9031
      create  app/controllers/welcome_controller.rb
       route  get 'welcome/index'
      invoke  erb
      create    app/views/welcome
      create    app/views/welcome/index.html.erb
      invoke  test_unit
      create    test/controllers/welcome_controller_test.rb
      invoke  helper
      create    app/helpers/welcome_helper.rb
      invoke    test_unit
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/welcome.coffee
      invoke    scss
      create      app/assets/stylesheets/welcome.scss
```

Define where the home page is located in the router (`config/routes.rb`)

```ruby
   root 'welcome#index'
```

Add ressource "articles" in routes. It represents a shared resource with CRUD operations.

```ruby
  resources :articles
```

To list routes
```
> bin/rails routes
                   Prefix Verb   URI Pattern         Controller#Action
            welcome_index GET    /welcome/index(.:format)         welcome#index
                 articles GET    /articles(.:format)         articles#index
                          POST   /articles(.:format)         articles#create
              new_article GET    /articles/new(.:format)         articles#new
             edit_article GET    /articles/:id/edit(.:format)         articles#edit
                  article GET    /articles/:id(.:format)         articles#show
                          PATCH  /articles/:id(.:format)         articles#update
                          PUT    /articles/:id(.:format)         articles#update
                          DELETE /articles/:id(.:format)         articles#destroy
                     root GET    /         welcome#index
       rails_service_blob GET    /rails/active_storage/blobs/:signed_id/*filename(.:format)         active_storage/blobs#show
rails_blob_representation GET    /rails/active_storage/representations/:signed_blob_id/:variation_key/*filename(.:format) active_storage/representations#show
       rails_disk_service GET    /rails/active_storage/disk/:encoded_key/*filename(.:format)         active_storage/disk#show
update_rails_disk_service PUT    /rails/active_storage/disk/:encoded_token(.:format)         active_storage/disk#update
     rails_direct_uploads POST   /rails/active_storage/direct_uploads(.:format)         active_storage/direct_uploads#create
```

Generate controller associated with the route.
```
> bin/rails generate controller Articles
Running via Spring preloader in process 10816      create  app/controllers/articles_controller.rb
      invoke  erb      create    app/views/articles
      invoke  test_unit      create    test/controllers/articles_controller_test.rb
      invoke  helper      create    app/helpers/articles_helper.rb
      invoke    test_unit      invoke  assets
      invoke    coffee      create      app/assets/javascripts/articles.coffee
      invoke    scss
      create      app/assets/stylesheets/articles.scss
```

Browse to `http://localhost:3000/articles/new`

> Unknown action
> The action 'new' could not be found for ArticlesController

In `app/controllers/articles_controller.rb` add `new` public method.
```ruby
class ArticlesController < ApplicationController
  def new
  end
end
```

Refresh the page and you will se a new error

> ActionController::UnknownFormat in ArticlesController#new

We need to associate a view to the action.

Create the missing template `app/views/articles/new.html.erb`

Refresh http://localhost:3000/articles/new

The content is visible.

Edit the template and create a form using the form builder.
```
<%= form_with scope: :article, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
<% end %>
```
