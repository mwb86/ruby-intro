# Ruby Basics

## Learning Objectives

* Compare/contrast Ruby and Javascript as programming languages.
* Run Ruby code by REPL (Pry/Irb) and file.
* Identify specific differences between Ruby and Javascript in the following areas...
  - Syntax
  - Variables
  - Fundamental Data Types
  - Data Collections
  - Conditionals
  - Methods (Functions)
* Examine Ruby symbols and data immutability.
* List three useful methods for arrays and hashes.
* Demonstrate how variables are stored in memory using Ruby.
* Use "!" to modify values in memory.


## Intro

HEADS UP: We are covering a lot of ground today. It's going to be a fast-paced class, so please raise your hand if I breeze over something quickly.
* For technical questions, please use Slack and one of the other instructors will help you out.

## What is Ruby? (5 minutes / 0:05)

Ruby is a **server-side** programming language.  

![Client-Server Model](http://i.imgur.com/AfiaMQP.png)  

Ruby resides in and is processed by a webpage's server.
* What is a server?
* It gathers information from the database, filters it using logic and from that generates HTML.
* That means you **cannot** look at or mess with a site's Ruby code as you did with Javascript via the browser console.
* We won't be including Ruby files in our HTML documents. You'll learn more about back-end development and how to connect everything together next week.

## What's Ruby like? (5 minutes / 0:10)

### M.I.N.A.S.W.A.N.

* "Matz Is Nice And So We Are Nice"
* Mentality not only applies to how you should treat your fellow developers, but also the philosophy behind Ruby itself.
* Yukihiro Matsumoto ("Matz") created Ruby to increase developer happiness.

> "Programmers often feel joy when they can concentrate on the creative side of programming, so Ruby is designed to make programmers happy." — Yukihiro "Matz" Matsumoto  

![He really is quite nice.](matz-n-park.png)

### A **Natural** Language

* While it isn't exactly simple, a lot of its features are going to feel intuitive.  

> "Ruby is simple in appearance, but is very complex inside, just like our human body." — Yukihiro "Matz" Matsumoto  

## Tools We'll Be Using (5 minutes / 0:15)

We will be running Ruby code via the Terminal in two different ways. But first, let's make sure you're all set up...

### Setting Up Ruby

Check to make sure you have Ruby installed: `$ ruby -v`
* Should get back something like: `ruby 2.2.1p85 (2015-02-26 revision 49769) [x86_64-darwin14]`
* If you need to install: `$ rvm install 2.2`
* Run a Ruby file: `$ ruby file_name.rb`

### PRY (REPL)

Allows us to run Ruby code one line at a time.
* Install: `$ gem install pry`
* Run REPL: `$ pry`
* Quit from REPL: `exit`
* Alternative: `$ irb`

> What is `gem`?

### Ruby vs. Javascript: Differences in Syntax (10 minutes / 0:25)

**BOARD:** What are some differences in syntax, "nice" or otherwise, you noticed between Ruby and Javascript?

#### Variables

No longer need to precede new variables with `var`. Just use the name of the variable!
* Variables are instantiated as they are used.
* Snakecase: all lower case, words separated by underscores.
* You should still keep names semantic!

Variables are still assigned using a single equals sign ( `=` )

```rb
my_favorite_animal = "flying squirrel"
# => "flying squirrel"
```

Although we don't use `var`, there is still syntax to designate whether a variable is local or global.
* nothing implies `local` (e.g., `my_number`)
* $ makes it global (e.g., `$my_number`)
* all-caps makes it a constant (e.g., `PI = 3.14`)


#### No Semicolons!

While your code will work if you close a line with `;`, common practice is not to use them.

#### Parentheses Optional

Since I'm in a Javascript state of mind, you will notice me using them pretty often.

```rb
number = 3
# => 3

if( number == 3 ) # with parens
  puts( "It's a 3!" )  
end  
# It's a 3!
# => nil

if number == 3 # without parens
  puts "It's a 3!"  
end  
# It's a 3!
# => nil
```

#### `puts` and `gets`

`puts` is the equivalent of Javascripts `console.log()`.

```rb
puts "Hello, Ruby!"
# Hello, Ruby!
# => nil
```

Ruby also allows us to easily accept inputs from the command line using `gets`.

```rb
user_input = gets
# => "My input\n" (Note that this line was typed by the user in the terminal)

user_input
# => "My input\n"
```

* Usually `gets` is followed by `.chomp`, which removes the new line generated by the user hitting return.
* If you need to convert your value to a number, add `.to_i` to the end of the method.
* To demonstrate `gets` we will write our ruby in a .rb file and run it as described above.

```rb
# Run this code in app.rb

# Asks for and stores a command line input into the variable as a string.
puts "How old are you?: "
user_input = gets.chomp.to_i
if user_input > 10
  puts "You are older than ten"
end
```

```bash
# In the terminal from in the same directory as app.rb

$ ruby app.rb
How old are you?:
20
You are older than ten
$ ruby app.rb
How old are you?:
8
$
```

### Data Types (15 minutes / 0:40)

Spend 15 minutes reading through everything up until the `In-Class Quiz`.  

**We have to read all this ourselves? Why?**
* While we could re-teach you what numbers, strings, conditionals, etc. are like in Ruby, you know enough about programming languages from your experience with Javascript to pick up on this information yourself pretty quickly.
* Because of this, the peculiarities of Ruby will be apparent. These are the things you need to be aware of in the next few classes.

#### Everything Is An Object!

Everything in Ruby is an **object**.
* By "object" we mean that everything has its own set of properties and methods.
  * Not a new concept. Some data types in Javascript had their own properties and methods (e.g., `string.length`).
* You will learn more about this when you dive into Ruby OOP...

#### Numbers

Ruby uses same arithmetic operators as Javascript
* `+`, `-`, `*`, `/`, `%`
* Same order of operations too: P.E.M.D.A.S.  

```rb
1 + 2 # Addition
# => 3

6 - 5 # Subtraction
# => 1

5 * 2 # Multiplication
# => 10

30 / 5 # Division
# => 6

31 / 5 # Note: integer division
# => 6

30 % 5 # Modulo (remainder)
# => 0

31 % 5
# => 1

3 ** 2 # Exponentiation
# => 9
```

#### Strings

Words, just like in Javascript.
* Surrounded by single or double-quotes
* Ruby uses similar escape characters
  - [List](http://www.java2s.com/Code/Ruby/String/EscapeCharacterslist.htm)
  - Must instantiate string with double-quotes for escape characters to work.

```rb
name = "John"
# => "John"

full_name = "John\nDoe"
# => "John\nDoe"

puts full_name
# John
# Doe
# => nil
```

Not only can you concatenate strings, now you can multiply them too!

```rb
# Concatenation
"Hello " + "there!"
# => "Hello there!"

# Multiplication
"Hello there! " * 3
# => "Hello there! Hello there! Hello there! "
```

##### String Interpolation

Sometimes you will want to print out a string that incorporates a variable. For example...

```rb
my_name = "Adrian"
# => "Adrian"

puts "Hi my name is: " + my_name
# Hi my name is: Adrian
# => nil
```

This works fine. Things aren't so simple when that variable is of a different data type. Like a number...
* Q: What's going to happen when we run this line of code?

```rb
class_number = 984
# => 984

puts "I am teaching WDI " + class_number
# TypeError: no implicit conversion of Fixnum into String from (pry):26:in `+'
```

In cases like the above, you either need to convert the variable to a string using `.to_s` OR use something called "interpolation."
* Surround the non-string variable with a hashtag and curly brackets: `#{variable}`

```rb
class_number = 984
# => 984

puts "I am teaching WDI #{class_number}"
# I am teaching WDI 984
# => nil
```

#### Booleans

Still `true` and `false`.
* We'll be using them in conditionals and comparisons just like in Javascript.

Comparisons in Ruby are nearly identical to Javascript
* `!=`, `&&`, `||`
* `<`, `>`, `<=`, `>=`, `==`

> Don't worry about `===` in Ruby for now. It [does not](http://mauricio.github.io/2011/05/30/ruby-basics-equality-operators-ruby.html) have the same application as in Javascript.  

"Truthiness" and "falsiness" are a lot less complicated in Ruby.
* **BOARD:** What values were "falsey" in Javascript?
* The only falsey values in Ruby are `nil` and `false`.

#### Nil

Ruby's "nothing".
* The equivalent of Javascript's `null`.
* You will usually see it when something does not have a return value (e.g., a `puts` statement).
* Like in Javascript, `nil` is falsey.

Need to check if something is `nil`? Use `.nil?`  
> **NOTE:** Any method that ends with a `?` means it will return a boolean value.  

```rb
something = "A thing"
# => "A thing"

something.nil?
# => false

something = nil
# => nil

something.nil?
# => true
```

### Conditionals

Pretty similar to Javascript, with some differences.
* No parentheses or curly brackets required.
* Begin blocks using `if`, `elsif` **(no second "e"!)** and `else`
* We close the whole loop using `end`.
  - This will be used throughout Ruby when dealing with code blocks (e.g., method/function).

Here's an example where we check for height at a roller coaster...

```rb
# In app.rb

puts "Welcome to the Iron Rattler! How tall are you (in feet)?"
height = gets.chomp

if height < 4
  puts "Sorry, you'll fly out of your seat if we let you on."
elsif height < 7
  puts "All aboard!"
else
  puts "If you value your head, you should not get on this ride."
end
```

> Ruby also has `case`, the equivalent to Javascript's `switch` statement. If that's more your style, read about it [here](http://www.skorks.com/2009/08/how-a-ruby-case-statement-works-and-what-you-can-do-with-it/).  

## In-Class Quiz: Ruby Data Types & Conditionals (15 minutes / 0:55)

If you finish Data Types and the Quiz early, feel free to try out one of the [Additional Exercises](https://github.com/ga-wdi-lessons/ruby-intro#additional-practice) located at the bottom of the lesson plan.

### Quiz Review (10 minutes / 1:05)

## BREAK (10 minutes / 1:15)

### Symbols and (Im)mutability (10 minutes / 1:25)

Symbols are immutable values. That means they contain the same value through the entirety of a program and cannot be changed.
* Kind of like a string that never changes.
* Syntax: `variable_name = :symbol_name`
* No Javascript equivalent ([until ES6 came along!](http://www.2ality.com/2014/12/es6-symbols.html)).

```rb
favorite_animal = :dog
# => :dog

puts favorite_animal
# dog
# => nil

other_favorite_animal = :killer_whale
# => :killer_whale

another_favorite_animal = :"flying squirrel"
# => :"flying squirrel"
```

You can convert symbols to -- but not replace them with -- other data types.

```rb
favorite_animal = :dog
# => :dog

favorite_animal.to_s
# => "dog"

favorite_animal = :dog
# => :dog
```

When/why would you use symbols?
* Most common use is as keys in hashes (the Ruby equivalent of objects -- more on that later).
* Make sure values that need to be constant stay constant.
* Enhance performance. Use less memory.

## Data Collections (15 minutes / 1:30)

### Arrays

An ordered collection of related values. Same syntax as Javascript arrays.
* Square brackets.
* Values separated by commas.
* Zero-indexed.

```rb
numbers = [ 1, 2, 3 ]
# => [1, 2, 3]

animals = [ "dog", "cat", "horse" ]
# => ["dog", "cat", "horse"]

animals[0]
# => "dog"

animals[1] = "elephant"
# => "elephant"

animals
# => ["dog", "elephant", "horse"]
```

Another super cool Ruby feature is that you can perform arithmetic operations -- addition, subtraction, multiplication -- on arrays!

```rb
numbers = [ 1, 2, 3 ]
# => [1, 2, 3]

more_numbers = [ 4, 5, 6, ]
# => [4, 5, 6]

lots_of_numbers = numbers + more_numbers
# => [1, 2, 3, 4, 5, 6]

lots_of_numbers - [ 4, 5, 6 ]
# => [1, 2, 3]

numbers * 3
# => [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

#### Array Methods

Ruby is very nice. It provides us with an extensive library of array methods we can use to traverse and manipulate arrays.
* [Documentation](http://ruby-doc.org/core-2.2.0/Array.html)
* Can't go over them all, but chances are if you could do it in Javascript then you can do it in Ruby.

**IMPORTANT:** You DO NOT need to memorize these. The following is just a sample of array methods available to you. You'll come to be more familiar with these as you need them and look them up in documentation.  

> **tl;dr:** The more you Google them, the better you'll remember them.  

##### Push/Pop

These Javascript methods also exist in Ruby and are used the same way.

```rb
numbers = [ 1, 2, 3, 4, 5 ]
# => [1, 2, 3, 4, 5]

numbers.push( 6 )
# => [1, 2, 3, 4, 5, 6]

numbers.push( 7, 8, 9 )
# => [1, 2, 3, 4, 5, 6, 7, 8, 9]

numbers.pop
# => 9
```

##### Sort
* Organizes array values from lowest to highest. Numbers and strings.

```rb
numbers = [ 3, 1, 5, 2, 4 ]
# => [3, 1, 5, 2, 4]

numbers.sort
# => [1, 2, 3, 4, 5]
```

##### Delete
* Removes an argument from an array.
* If there are multiple instances of that argument, it will delete them all.
* Look up: `.delete_at()`, `.slice()`

```rb
numbers = [ 3, 1, 2, 2, 4 ]
# => [3, 1, 2, 2, 4]

numbers.delete( 2 )
# => 2

numbers
# => [3, 1, 4]
```

##### Shuffle

Q: Who has tried shuffling an array in this class already? What did you have to do?
* BOOM! Ruby comes with a native array shuffling method.

```rb
numbers = [ 1, 2, 3, 4, 5 ]
# => [1, 2, 3, 4, 5]

numbers.shuffle
# => [5, 1, 4, 2, 3]
```

### Hashes

A unordered, "dictionary-like" collection organized by key-value pairs. Very similar to Javascript objects...

```rb
wdi_class = {
   teacher: "John",  
   students: [ "Yacko", "Wacko", "Dot" ],  
   classroom: 2,  
   in_session: true,  
   schedule: {  
     morning: "Ruby Basics",
     afternoon: "Enumerables"
   }
 }  
# => {:teacher=>"John", :students=>["Yacko", "Wacko", "Dot"], :classroom=>2, :in_session=>true, :schedule=>{:morning=>"Ruby Basics", :afternoon=>"Enumerables"}}
```

Accessing hash values...  

```rb
wdi_class[:teacher]
# => "John"
```
> `:teacher` is a data type that is pretty unique to Ruby called a "symbol." We'll learn more about these later in the lesson.  

Modifying hash values...

```rb
wdi_class[:teacher] = "Jack"
# => "Jack"
```

#### Hash Methods

Like arrays, Ruby also provides us with a library of hash methods.  
* [Documentation](http://ruby-doc.org/core-2.2.0/Hash.html)

> As mentioned with arrays, do not worry about memorizing these methods. Just know how to look them up should the need arise.  

##### Keys

Returns an array with all the keys in a hash.

```rb
wdi_class.keys
# => [:teacher, :students, :classroom, :in_session, :schedule]
```

##### Merge

Combines two hashes.

```rb
classroom = {
 room: 1  
}  
# => {:room=>1}

locations = {
 location_one: "DC",  
 location_two: "NY",  
 location_three: "Boston"  
}  
# => {:location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

silly_hash = classroom.merge( locations )
# => {:room=>1, :location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

classroom
# => {:room=>1}

locations
# => {:location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}

silly_hash
# => {:room=>1, :location_one=>"DC", :location_two=>"NY", :location_three=>"Boston"}
```

### Ranges

Use ranges to quickly generate arrays of data types.
* Parentheses.
* Min and max value, separated by two periods.
* Generate array using `.to_a` method.

```rb
(1..5).to_a
# => [1, 2, 3, 4, 5]

("a".."z").to_a
# => ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
```

## Exercise/Quiz (15 minutes / 1:45)

### Exercise/Quiz Review (10 minutes / 1:55)

### BREAK (5 minutes / 2:00)

### Methods (10 minutes / 2:15)

The equivalent of Javascript "functions."
* Many things are referred to as "methods" in Ruby. Right now, we'll be talking about methods that are not attached to an object (e.g., array, hash).

Components
* `def` - the Ruby equivalent of `function`
* `double` - the method name in the below example
* `number` - the argument name in the below example
* `end` - closes the method

```rb
def double( number )
  doubled_number = number * 2  
  return doubled_number  
end  
# => :double

double( 3 )
# => 6

double 3
# => 6
```

You may have noticed that we use the same `return` notation as Javascript. This is called an **explicit return**, because we identify what exactly we want returned from the function.  

Ruby also lets us make **implicit returns**. This means that when we do not use the `return` keyword, Ruby will automatically return the value of the last line of code in the method.
* We encourage you to use **explicit returns** so we know exactly what your method is returning.

```rb
def double( number )
  doubled_number = number * 2  
  doubled_number  
end  
# => :double

double( 3 )
# => 6

double 3
# => 6
```

Ruby methods can also establish default argument values.
* In the below example, if we do not provide our `double` method with an argument, it will default to 5.

```rb
def double( number=5 )
  doubled_number = number * 2  
  puts "Your doubled number is #{doubled_number}"  
  doubled_number  
end  
# => :double

double
# Your doubled number is 10
# => 10
```

## Closing

What do you like about Ruby? How would you compare it to Javascript at this point?

### Review Learning Objectives

## Resources
* [Chris Pine's Learn to Program](https://pine.fm/LearnToProgram/chap_00.html)
* [Ruby Monk](https://rubymonk.com/)
* [Why's Poignant Guide to Ruby](http://poignant.guide/book/chapter-2.html)
* [Ruby Koans](http://rubykoans.com/)

## Additional Practice
* [Word Ladder](https://github.com/ga-wdi-exercises/word_ladder)
* [Who Won The Election?](https://github.com/ga-wdi-exercises/who_won_the_election)
* [Search For Obi-Wan](https://github.com/ga-wdi-exercises/search_for_obi_wan)
* [Pig-Latin](https://github.com/ga-wdi-exercises/pig_latin)
* [Letter Counter](https://github.com/ga-wdi-exercises/letter_counter)
