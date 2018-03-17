# Rails
Always check out http://guides.rubyonrails.org/ first...

http://rubyonrails.org/
Rails is a MVC framework.  
`gem install rails --version=5.0.0.1 --no-ri --no-rdoc`  
Comes with a CLI `rails`.  
To get info about the rails project run `bin/rails about`.(the `$> bin/rails` script is a wrapper can do `bundle exec rails about`)  
Works on **Convention** over configuration philosophy. Do things this way and the rails magic will make it work.

Start rails server
`bin/rails server -b 0.0.0.0`  

#### Generate Controllers
Run `bin/rails generate controller Say hello goodbye`  
Generates..  
* `app/controllers/say_controller.rb`  
* `app/views/say/goodbye.html.erb`  
* `app/views/say/hello.html.erb`  


### Views
Default Views use ERB [Embedded RuBy](http://www.stuartellis.eu/articles/erb/) templates.
