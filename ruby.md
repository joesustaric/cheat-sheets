# Ruby Cheat Sheet
I decided to do create this as part of my ruby revision.  
Quick guide for me to keep track of ruby idioms and small how to examples.  
With help from the 'Eloquent Ruby' book.  

### Basic Stuff
Code indentation **2 Spaces**.  
Don't use tabs to indent.  
**Camel Case** for classes.  
**Snake Case** everywhere else.
**Caps Snake Case** for constants.  

``` Ruby
class ThisIsCamelCase

  A_SNAKE_CASE_CONSTANT = 'snakes on a plane'

  def this_is_snake_case( cobras )
    # function stuff in there
  end

end
```  
**Parentheses are Optional** occasionally forbidden.  

``` Ruby
def what_is_the_answer( question, person )
  # Return the determined answer
end

# You can call it like so  
what_is_the_answer('What is the meaning of life?', 'Joe' )  

# or
def what_is_the_answer question
  # Return the determined answer
end

# You can call it like so  
what_is_the_answer 'What is the meaning of life?', 'Joe'

```  
**Generally better to have them** than not having them.  
Don't need them with familiar methods like `puts 'Hello World'`  
Don't use them when they're empty, eg  
```Ruby
# No
def a_function()
  # do stuff
end
# Yes
def a_function
  # do stuff
end

#same with method invocations  
@object_thing.a_function() # No
@object_thing.a_function   # Yes
```  

Same with conditionals.  
```Ruby
# No
if ( this_variable_is_true )
  # do something
end

# Yes
if this_variable_is_true
  # do stuff
end
```
#### Folding Up Blocks  
Do it if the line is **not too long and easy to read** usually a single statement.  
```Ruby
# This
10.times do |n|
  puts "The number is #{n}"
end

# To this
10.times { |n| puts "The number is #{n}" } # Good
```  

#### Control Structures
The `unless` usually reads better in most situations. eg  
```Ruby
# You can write something like this
if not @read_only
  # write stuff
end
# using unless to read better
unless @read_only
  # write stuff
end
```  
**`Unless`** block will execute if the condition is false.  

Similarly `while` has `until`.  
```Ruby
# This is harder to read  
while ! document.is_printed?
  document.print_next_page
end
# Than this
until document.printed?
  document.print_next_page
end
```  
**These can be folded up** because they are simple one liners.  
```Ruby
# EG
@page_text = new_text unless @read_only  
# and
document.print_next_page until document.printed?
document.parint_next_page while document.has_pages_left?
```  
If they are a few line probably leave them in the block.  

#### Use Each
```Ruby  
for thing in things
  puts things
end

# Use Each instead
things.each do |thing|
  puts thing
end
```  
Same rules for folding this down apply here.  

### Write a better case statement  
```Ruby
# Meh case statement
case movie
when 'Top Gun'
  puts 'Tom Cruise'
when 'Terminator 2'
  puts 'Arnold Schwartzenegger'
else
  puts 'Samuel L Jackson'
end

# Better one
actor = case movie
        when 'Top Gun'
          'Tom Cruise'
        when 'Terminator 2'
          'Arnold Schwartzenegger'
        else
          'Samuel L Jackson'
        end
# Even better
actor = case movie
        when 'Top Gun' then 'Tom Cruise'
        when 'Terminator 2' then 'Arnold Schwartzenegger'
        else 'Samuel L Jackson' # if no else specified the else will default to returning nil
```
**Only `false` and `nil` are treated as false. Everything else is true.**  

### Init Vars  
The ruby way is generally..
```Ruby
@some_var ||= ''
# same as
@some_var = @some_var || ''
```  
Don't use this for Booleans though.  

### Collections  
Array [API doco v2.2.0](http://ruby-doc.org/core-2.2.0/Array.html)
```Ruby
words = %w{ Here are some words to split into an array }
```  
Hashes [API doco v2.2.0](http://ruby-doc.org/core-2.2.0/Hash.html)
```Ruby
# Can use the Rocket =>
my_hash = { "string key" => 5, "something else" => 99}
# Use symbols more common
my_hash = { :first_key => 'first value', :second_key => 'second value' }
# simpler with symbols
my_hash = { first_key: 'first value', second_key: 'second value' }

#printing
my_hash.each { |key,value| puts "#{key} = #{value}" }
```

### Method Args
You can specify defaults, or variable arguments
```Ruby
# defaults
def methos_one( name, age = 18)
  # stuff
end
# n number of Args
def print_names( *names )
  names.each { |name| puts name }
end
```
asterisk referred to as splat
You can have only 1 * arg in a list.



### How to Comment Ruby Code
TODO  

## Stuff to fill out later
[Virtual Methods](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_classes.html#UC)   
.defined?  
gem 'some_lib', require: false  

