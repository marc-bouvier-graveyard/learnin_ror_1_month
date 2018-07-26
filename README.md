# Learning Ruby on Rail in 1 month
My attempt to learn ruby on rails in 1 month

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
