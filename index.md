# Learning Ruby on Rail in 1 month
My attempt to learn ruby on rails in 1 month.

## 2018-07-25

* [Ruby on Rails official site](https://rubyonrails.org/)

Tour of the framework
<iframe width="560" height="315" src="https://www.youtube.com/embed/OaDhY_y8WTo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

* [The rails Doctrine](https://rubyonrails.org/doctrine/)

[tag 2018-07-25](https://github.com/marc-bouvier/learnin_ror_1_month/tree/2018-07-25)

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

[tag 2018-07-26](https://github.com/marc-bouvier/learnin_ror_1_month/tree/2018-07-26)

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
Problem, the submits points to the same page. Let's change it.
```
  <%= form_with scope: :article, url: articles_path, local: true do |form| %>
```

Now, fill the form and submit.

> Unknown action
> The action 'create' could not be found for ArticlesController

See you next time ! 

[tag 2018-07-27](https://github.com/marc-bouvier/learnin_ror_1_month/tree/2018-07-27)

## 2018-07-30

Goals : Why I want to learn ROR?
> I often have good ideas but I just stash them into notepads or trello and never begin to implement them
> ROR I think can help me prototype these ideas and show them to people that may be interested

Add "create" action in articles controller.
```
  def create
    render plain: params[:article].inspect
  end
```

`params` method allow to extract parameters from request.

Now let's create the model for articles. It will generate classes and migration script for a table.

```
> bin/rails generate model Article title:string text:text  
Running via Spring preloader in process 16005
    invoke  active_record
    create    db/migrate/20180730055636_create_articles.rb
    create    app/models/article.rb
    invoke    test_unit
    create      test/models/article_test.rb
    create      test/fixtures/articles.yml
```

You can now run the migration script.

```
> bin/rails db:migrate
== 20180730055636 CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0012s
== 20180730055636 CreateArticles: migrated (0.0013s) ==========================
```

Back in the articles controller we can now update the create action.
```
  def create
    @article = Article.new(params[:article])

    @article.save
    redirect_to @article
  end
```

Try to create an arcticle http://localhost:3000/articles/new

> ActiveModel::ForbiddenAttributesError in ArticlesController#create
> ActiveModel::ForbiddenAttributesError
> Extracted source (around line #6):
> ```
>   def create
>     @article = Article.new(params[:article])
>    
>     @article.save
>     redirect_to @article
> ```
> 
> Rails.root: /home/marco/learning/ruby_on_rails/learnin_ror_1_month/blog

A security feature called [strong parameters](https://guides.rubyonrails.org/action_controller_overview.html#strong-parameters) don't allow to map directly any values of parameters into the model. This is to avoid malicious parameter injection. We have to specify exactly which parameters are allowed.

We know we will wat to reuse the algorithm in the update action so we factor it in a private method.

```
  def create
    @article = Article.new(article_params)
   
    @article.save
    redirect_to @article
  end
   
  private
    def article_params
      params.require(:article).permit(:title, :text)
    end
```

Write show method

```
  def show
    @article = Article.find(params[:id])
  end
```

@article is an instance variable and all instances variables will be passed to the view.

Create "show" view `app/views/articles/show.html.erb`

```
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>
 
<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```

Now we want to list article. We can find action name for ̀`articles` using `bin/rails route`.
```
> bin/rails routes
...
  articles GET    /articles(.:format) articles#index
...
```

We then now that we need a template for the action `index`
```
  def index
    @articles = Article.all
  end
```

app/views/articles/index.html.erb
```

<h1>Listing articles</h1>
 
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th></th>
  </tr>
 
  <% @articles.each do |article| %>
    <tr>
      <td><%= article.title %></td>
      <td><%= article.text %></td>
      <td><%= link_to 'Show', article_path(article) %></td>
    </tr>
  <% end %>
</table>
```

We can now find the articles here : http://localhost:3000/articles

Let's add links in various pages for navigation.

Open app/views/welcome/index.html.erb
```
<h1>Hello, Rails!</h1>
<%= link_to 'My Blog', controller: 'articles' %>
```
app/views/articles/new.html.erb
```
  <%= link_to 'Back', articles_path %>
```
app/views/articles/index.html.erb
```
  <%= link_to 'New', new_articles_path %>
```

Let's stop here for now https://guides.rubyonrails.org/getting_started.html#adding-some-validation

## ????-??-??
