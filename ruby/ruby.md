# Ruby Cheat Sheet
I decided to do create this as part of my ruby revision.  
Quick guide for me to keep track of ruby idioms and small how to examples.  
With help from the 'Eloquent Ruby' book.  
https://github.com/bbatsov/ruby-style-guide

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
### Ruby is Dynamically Typed
No need to specify instance types. Just make them.  
No need for complicated inheritance.  
```Ruby
class Thing1
  def do_something
    # something
  end
end

class Thing2
  def do_something
    # something
  end
end

def do_stuff(a_thing)
  a_thing.do_something # will work for both Thing1 and Thing2 classes
end

```
try to avoid type checking  
`raise 'not a string' unless obj.kind_of? String`  


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
def method_one(name, age = 18)
  # stuff
end
# n number of Args
def print_names(*names)
  names.each { |name| puts name }
end
```
asterisk referred to as splat
You can have only 1 * arg in a list.

### Map and Inject  
`map` takes a block and runs through the collection calling the block for each element.  
Will return an array of all the items returned by the block.  
Useful for transforms. e.g
```Ruby
strings = ['ONE', 'TWO', 'FOUR']
pp strings.map { |word| word.size }
# will print
# [3, 3, 4]

# transform
result = strings.map { |word| word.downcase }
pp result
# ['one', 'two', 'four']
```  

`inject` takes a block and calls the block with each element and the current result.  
When all the elements are iterated it will return the result as it's final value.  
```Ruby
total = words.inject(0.0){ |result, word| word.size + result }
```  
If you don't provide a starting value in the call, it will skip the first element and
use it as the starting value.  

### Bangs!  
`!` means that the method being called on the object is the 'dangerous' or 'surprising' version
of a pair of methods. eg `words.reverse` returns a copy `words.reverse!` will change the words
object to now be in reverse order.  

### Strings  
Single quote string = string literals. No interpolation.  
Ruby strings are mutable.  
```Ruby
a_string_with_a_quote = 'something\'s gone wrong'  
string_with_backslash = 'sting with backslash \\'
```  
With double quotes you can put characters like new lines and tabs etc..  
```Ruby
double_quoted = " something tab \t and a newline \n"
```  
You can also embed arbitrary expressions.  
```Ruby
name = 'Joe'
hello_string = "Hello my name is #{name}"
# If you had to mix and match quotes like this
string_eg = '"Stop", she said, "I can\'t live without \'s and "s.'
string_eq = %q{"Stop". she said, "I can't live without 's and "s."}
# or
time_string = %Q{The time is #{Time.now}}

# You can span lines
string_eg = %Q{hello spanning \
multiple lines with no new line character}
multi_line_string = <<EOF
Something backslash
blah backslash
end
EOF

```
Ruby string API http://ruby-doc.org/core-2.2.0/String.html  

### Regexp  
Works very similarly to other regexes.  
```Ruby  
puts /Joe/ =~ 'Hello Joe'
# Will print 6 (matched at the 6th character)
puts /Foo/ =~ 'Bar'  
# Will return nil  
```  
Global Substitution on strings.  
```Ruby
my_string = 'Hello Joe Whats going on Foo Bar'
my_string.gsub!( /Joe/, 'Ruby')
# String now = Hello Ruby Whats going on Foo Bar  
```

### Symbols  
There can only be one instance of any given symbol.  

```Ruby
a = :all
b = a
c = :all
```  
`a b c` are all refer to exactly the same object.  
** They make ideal hash keys **   
```Ruby
my_string = :all.to_s
the_symbol = my_string.to_sym
```  

### Classes / Instances / Methods  
Everything is an Object. Ruby is a OO language.  
Everything is can be traced back to `Object` class.  

```Ruby
require 'another_class'

class Document
  # ...
  attr_accessor :content
  attr_reader :name
  attr_writer :stuff

  def words
    @content.split
  end

  def word_count
    words.size
  end

  def a_private_method
    # something
  end

  # You can over write inherited methods
  def to_s
    'Overwritten to_s method'
  end

  private :a_private_method #list your private methods
  public :word_count, :words # etc
  protected
end
```  
Private methods are callable from subclasses, and also private to this object instance. (**Exception of [.send](#send)**)
Public is public.
Protected methods can be called by any instance of a class can call a protected method on any other instance of the class.  
It will call `self.` automatically. ie `words.size = self.words.size`  
If you don't specify a super class, it will be a sub class of `Object`.  
`require` is a method that takes in a file name and executes the ruby code, it wont parse files twice. (like importing)

```Ruby
class Novel < Document
  # more class stuff
end
```  

### Reflection  
You can reflect on a ruby object. There are many methods you can call eg..  
```Ruby
my_object.instance_methods  
my_object.instance_variables
# etc..
```  

### Operator Overloading
Can be done.  
Binary operator.  
my_something + other_something
```Ruby
class Something
  ...
  def +(other)
    # my definition
  end
end
```  
Unary operators. eg +my_something
```Ruby
class Something
  ...
  def +@
    # my definition
  end
end
```  

## Interesting Ruby stuff
### eval
`eval` method will execute ruby code.  
```Ruby
cmd = gets
puts( eval(cmd) )
```  
### ++ and --
Ruby does not use these i.e can't use `int_var++` to increment by one.  
http://stackoverflow.com/a/3717565   
``

### send
You can access a method by using `.send`. Even if its private.  
```Ruby
n = my_object.send(:my_private_method)
```  

### Overwriting []  
You can make an object look like a []. By overwriting it.  
```Ruby
class Something
  ...
  def [](index)
    string_words[index]
  end
end
```  
Add a size method too..  

### Equality =  
Rubys object class has 4 quality methods.  
`eql? equal? == ===`  
`.equal?` test for object identity. eg `x.equal? y` would be true if x and y refer to the exact same object.

`==` default with behave like `.equal?` can over wirte for own classes.  

Using objects as keys in hashes.  
The Ruby hash calls the `.hash` method to get the hash code for its keys.  
ensure that if you override `a.eql? b` then `a.hash == b.hash`. eg  
```Ruby
def hash
  a.hash ^ b.hash
end
def eql?(other)
  a == other.a && b == other.b
end
```  
`===` used more so for case statements.  
To get object equality right

### Singleton  
Singleton methods is a method that is defined for exactly one object instance.
Can add them to objects on the fly.  
```Ruby
some_stub_object = Object.new

def some_stub_object.hello
  "hi"
end
# or

class << some_stub_object
  def some_check?
    true
  end

  def another_method(blah)
    "hello #{blah}"
  end
end
```  

### Modules
Module is a container. Cannot instantiate a module.
Can hold methods, constants, classes and other modules.

Purpose to group related things, to avoid namespace conflicts.

```ruby
module Foo
  class Baz
  end
  module Bar
    SOME_CONSTANT = 'blah'
  end
end

Foo::Baz.new
Foo::BAR::SOME_CONSTANT

require 'foo'

```
use if you're creating classes with the same prefix eg FooBar FooBaz FooJoe.
Don't get carried away. Don't nest too deep.  

#### as mixins
* Mixing allows you to share common code amongst unrelated Classes

```ruby
module Stuff
  SOME_CONSTANT = "blah"

  def figure_out_stuff
    "done some stuff"
  end
end

class Something
  include Stuff
  # Something Class..
end

class SomeBaseThing < AnotherThing
  include Stuff
  # AnotherThing class..
end
```
* Including it means you have 'mixed it in'.
* Can mixin multiple Modules
* including a module puts it as a super of the class. see it in `instance_of_object.ancestors`.

#### Mixins as class methods
```ruby
class SomeThing
  class << self
    include Stuff
  end
end
```

Methods are not self but written as instance level.

#### Blocks..
```ruby
def do_something_with_block
  yield if block_given?
end

do_something_with_block { puts "Do this thing.." }

def with_x(thing)
  begin
    do_x
    return_value = yield
    do_x_again_or_y
    return_value
  rescue
    print_thing_failed(thing)
    raise
end

# Ensure stuff happens if things raise eg clean up handles.
def with_connection(connection_info)
  connection = Connect.new(connection_info)
  begin
    yield(connection)
  ensure
    connection.close
  end
end

with_connection(connection_string) do |c|
  do_stuff_with_connection(c)
end

```
Passing blocks as parameters and calling them on demand.

```ruby
def run_a_block(&a_block)
  a_block.call if a_block
end
#.call will execute the block if not nil.
```

TODO: difference between lambda / proc / Proc.new

### How to Comment Ruby Code
TODO  

## Stuff to fill out later
[Virtual Methods](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_classes.html#UC)   
.defined?  
gem 'some_lib', require: false  
Understand Rake and rake tasks  
Rack + Rack apps  
Quick Ref for reading and writing to files. (Esp note when file handles are left open) .  
