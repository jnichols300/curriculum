## Ruby Basics

### Learning Objectives

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


### Intro (5min)

HEADS UP: We are covering a lot of ground today. It's going to be a fast-paced class, so please raise your hand if I breeze over something quickly.
* For small technical questions, please use Slack and one of the other instructors will help you out.

#### What is Ruby? (5min)

Server-side language
* Remember Robin's diagram from Week #1?

![Client-Server Model](http://i.imgur.com/AfiaMQP.png)

Ruby resides in and is processed by a webpage's server.
* It gathers information from the database, filters it using logic, and from that generates HTML.
* That means you **cannot** look at or mess with a site's Ruby code as you did with Javascript.
* We won't be including Ruby files in our HTML documents. You'll learn more about back-end development and how to connect everything together next week.

#### What's Ruby like? (5min)

MINASWAN
* Does anybody remember this from Allie's lunchtime presentation last Friday?
  * "Matz Is Nice And So We Are Nice"
    * Mentality not only applies to how you should treat your fellow developers, but also the philosophy behind Ruby itself
  * Yukihiro Matsumoto ("Matz") created Ruby to increase developer happiness.

Ruby as a "natural" language
* While it isn't exactly simple, a lot of its features are going to feel intuitive.  
* Matz: "Ruby is simple in appearance, but is very complex inside, just like our human body."


#### Tools We'll Be Using (5min)

We'll be running Ruby the same way we used Node to run Javascript during out first class.

Ruby
* Check to make sure you have Ruby installed: `$ ruby -v`
  * Should get back something like: `ruby 2.2.1p85 (2015-02-26 revision 49769) [x86_64-darwin14]`
* If you need to install: `$ rvm install 2.2`
* Run a Ruby file: `$ ruby file_name.rb`

The REPL: Pry
* Allows us to run Ruby code one line at a time.
* Install: `$ gem install pry`
* Run REPL: `$ pry`
* Quit from REPL: `exit`
* Alternative: `$ irb`

### Some Differences From Javascript

Part of your homework last night was to identify a programming concept shared by Javascript and Ruby and compare/contrast its implementation in each of the languages.
- BOARD: Share and write on board.

#### Variables (5min)

No longer need to precede new variables with `var`. Just use the name of the variable!
* Variables are instantiated as they are used.
* Snakecase: all lower case, words separated by underscores.
* You should still keep names semantic!

Variables are still assigned using a single equals sign ( `=` )

```ruby
my_favorite_animal = "flying squirrel"
```

Although we don't use `var`, there is still syntax to designate whether a variable is local or global.
* nothing implies `local` (e.g., `my_number`)
* $ makes it global (e.g., `$my_number`)
* all-caps makes it a constant (e.g., `PI = 3.14`)


#### No Semicolons!

While your code will work if you close a line with `;`, common practice is not to use them.

#### Parentheses Optional

Since I'm in a Javascript state of mind, you will notice me using them pretty often.

```ruby
number = 3
if( number == 3 )
  puts( "It's a 3!" )
end

# => "It's a 3!"
if number == 3
  puts "It's a 3!"
end
# => "It's a 3!"
```

#### Puts and Gets (5min)

`puts` is the equivalent of Javascripts `console.log()`.

```ruby
puts "Hello!"
# => "Hello!"
```

Ruby also allows us to easily accept inputs from the command line using `gets`.
* Usually followed by `chomp`, which removes the new line generated by the user hitting return.
* If you need to convert your value to a number, add `.to_i` to the end of the method.
* Compared to Javascript and Node, which don't offer a simple way to do this.

```ruby
# Asks for and stores a command line input into the variable as a string.
puts "How old are you?: "
user_input = gets.chomp.to_i
```

### Data Types

Everything in Ruby is an **object**.
* Not like a Javascript object -- those are called **hashes** in Ruby.
* By "object" we mean that everything has its own set of properties and methods.
  * Not a new concept. Some data types in Javascript had their own properties and methods (e.g., `string.length`).
* Will learn more about this during your OOP class...

#### Numbers (5min)

Ruby uses same arithmetic operators as Javascript
* `+`, `-`, `*`, `/`, `%`
* `**` - Exponents
  - `2**4` - 2 to the 4th power
* Same order of operations too: P.E.M.D.A.S.  

```ruby
# Addition
1 + 2 = 3

# Substraction
6 - 5 = 1

# Multiplication
5 * 2 = 10

# Division
30 / 5 = 6

# Exponents
2 ** 4 = 16
```

#### Strings (10min)

Words, just like in Javascript.
* Surrounded by single or double-quotes
* Ruby uses similar escape characters
  - [List](http://www.java2s.com/Code/Ruby/String/EscapeCharacterslist.htm)
  - Must instantiate string with double-quotes for escape characters to work.

```ruby
name = "Adrian"

full_name = "Adrian\nMaseda"
puts full_name
# => Adrian
# => Maseda
```

Not only can you concatenate strings, now you can multiply them too!

```ruby
# Concatenation
"Hello " + "there!"
# => "Hello there!"

# Multiplication
# Imagine using this for your pyramid exercise!
"Hello there! " * 3
# => "Hello there! Hello there! Hello there! "

```

##### Interpolation

Sometimes you will want to print out a string that incorporates a variable. For example...

```ruby
my_name = "Adrian"
puts "Hi my name is: " + my_name
```

This works fine. Things aren't so simple when that variable is of a different data type. Like a number...
* Q: What's going to happen when we run this line of code?

```ruby
class_number = 6
puts "I am teaching WDI " + class_number
# => TypeError: no implicit conversion of Fixnum into String
```

In cases like the above, you either need to convert the variable to a string using `.to_s` OR use something called "interpolation."
* Surround the non-string variable with a hashtag and curly brackets: `#{variable}`

```ruby
class_number = 6
puts "I am teaching WDI #{class_number}"
# => "I am teaching WDI 6"
```

#### Nil (5min)

Ruby's "nothing".
* The equivalent of Javascript's `null`.
* You will usually see it when something does not have a return value (e.g., a `puts` statement).
* Also like Javascript, `nil` is falsey.

Can check if something is `nil` using `.nil?`
* **NOTE:** Any method that ends with a `?` means it will return a boolean value.

```ruby
something = "A thing"
something.nil?
# => false

something = nil
something.nil?
# => true
```

#### Booleans (5min)

Still `true` and `false`.
* We'll be using them in conditionals and comparisons just like in Javascript.

Comparisons in Ruby are nearly identical to Javascript
* `!=`, `&&`, `||`
* `<`, `>`, `<=`, `>=`, `==`
  - Don't worry about `===` in Ruby for now. It [does not](http://mauricio.github.io/2011/05/30/ruby-basics-equality-operators-ruby.html) have the same application as in Javascript.

Truthiness and falsiness is a lot less complicated in Ruby.
* **BOARD:** What values were "falsey" in Javascript?
  * `false`
  * `0`
  * `""`
  * `null`
  * `undefined`
  * `NaN`
* The only falsey values in Ruby are `nil` and `false`.

### Exercise: Temperature Converter (Part I) (20min)

[Temperature Converter (Ruby)](https://github.com/ga-dc/temperature_converter_ruby)

### BREAK (10min)

#### Symbols and (Im)mutability (15min)

Symbols are immutable values. That means they contain the same value through the entirety of a program and cannot be changed.
* Kind of like a string that never changes.
* Syntax: `variable_name = :symbol_name`
* No Javascript equivalent.

```ruby
favorite_animal = :dog

# Looks the same as a string when you print to console
puts favorite_animal
# => dog

# Alternative syntax
other_favorite_animal = :killer_whale
another_favorite_animal = :"flying squirrel"
```

You can convert symbols to -- but not replace them with -- other data types.

```ruby
# To string
favorite_animal = :dog
favorite_animal.to_s
# => "dog"
```

You cannot change a symbol's value...

```ruby
:dog = :bird
# SyntaxError: unexpected '=', expecting end-of-input
```

When/why would you use symbols?
* Make sure values that need to be constant stay constant.
* Enhance performance. Use less memory.
* Often used as keys in objects (hashes). More on that later this class.

### More on Variables (10min)

Symbols and data immutability are a good segue into talking more about variables and memory allocation in Ruby.

Haha!

![XKCD pointers comic](https://camo.githubusercontent.com/e015a8e243f53ffecd9b18fc5c8d770dde1948cc/687474703a2f2f626c6f672e70726f7465637465647374617469632e636f6d2f77702d636f6e74656e742f75706c6f6164732f323030372f30352f706f696e746572732e706e67)

Why is that so funny? Because variables are pointers to values in memory.

![Variables in memory diagram](https://camo.githubusercontent.com/62b04af497f124fc9b11ec3802d73497f5c9e305/687474703a2f2f64326177357865326a6c647175652e636c6f756466726f6e742e6e65742f626f6f6b732f727562792f696d616765732f7661726961626c65735f706f696e74657273312e6a7067)

#### .object_id

We can use the `.object_id` method to demonstrate that two variables are pointing to the same object.
- Returns an integer identifier for the object that is automatically generated by Ruby

```ruby
a = 10
b = a

a.object_id
# => 21
# You will probably get a different number than 21.

b.object_id
# => 21
```

#### Bang! (The `!` Symbol)

Unlike symbols, other data types in Ruby are mutable.
* We can not only change what values in memory variables are pointing to, but we can change those values in memory as well.

Methods with an `!` attached to the end of them usually means that they will modify the object they are calling on.
* Things can get tricky when you have multiple variables pointing at the same value. For example...

```ruby
# a points to a memory location containing 5
a = "cheeseburger"

# b now points to that same memory location
b = a

# Call upcase! (with a bang) on the value b is pointing to.
b.upcase!
# => "CHEESEBURGER"

# That means a is now also pointing to the modified value.
a
# => "CHEESEBURGER"
```

#### Exercise: Variable Assignment (20min)

[Exercise: Variable Assignment](https://gist.github.com/amaseda/35a62128d8795e045d49)
* Work in pairs and answer the questions in the link above.
* **NO CODING ALLOWED!** Stretch those brain muscles and talk these out with your partner.
* Writing these out on your table/whiteboard with markers is strongly encouraged.


### Data Collections

#### Arrays (10min)

An ordered collection of related values. Same syntax as Javascript arrays.
* Square brackets.
* Values separated by commas.
* Zero-indexed.

```ruby
# Ordered lists
numbers = [ 1, 2, 3 ]
animals = [ "dog", "cat", "horse" ]

# Select an array value according to its index
animals[0]
# => "dog"

# => Reassign a value at a specific index
animals[1] = "elephant"
animals
# => [ "dog", "elephant", "horse" ]
```

Another super cool Ruby feature is that you can perform arithmetic operations -- addition, subtraction, multiplication -- on arrays!

```ruby
numbers = [ 1, 2, 3 ]
more_numbers = [ 4, 5, 6, ]

# Addition
lots_of_numbers = numbers + more_numbers
# => [ 1, 2, 3, 4, 5, 6 ]

# Subtraction
lots_of_numbers - [ 4, 5, 6 ]
# => [ 1, 2, 3 ]

# Multiplication
numbers * 3
# => [ 1, 2, 3, 1, 2, 3, 1, 2, 3 ]
```

##### Array Methods

Ruby is very nice. It provides us with an extensive library of array methods we can use to traverse and manipulate arrays.
* [Documentation](http://ruby-doc.org/core-2.2.0/Array.html)
* Can't go over them all, but chances are if you could do it in Javascript then you can do it in Ruby.

###### Push/Pop

These Javascript methods also exist in Ruby and are used the same way.

```ruby
numbers = [ 1, 2, 3, 4, 5 ]

# Push
numbers.push( 6 )
# => [ 1, 2, 3, 4, 5, 6 ]

# Push (multiple elements)
numbers.push( 7, 8, 9 )
# => [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

# Pop
numbers.pop
# => [ 1, 2, 3, 4, 5, 6, 7, 8 ]
```

###### Sort
* Organizes array values from lowest to highest. Numbers and strings.

```ruby
numbers = [ 3, 1, 5, 2, 4 ]
numbers.sort
# => [ 1, 2, 3, 4, 5 ]
```

###### Delete
* Removes an argument from an array.
* If there are multiple instances of that argument, it will delete them all.
* Look up: `.delete_at()`, `.slice()`

```ruby
numbers = [ 3, 1, 2, 2, 4 ]
numbers.delete( 2 )
# => [ 3, 1, 4, ]
```

###### Shuffle

Q: Who has tried shuffling an array in this class already? What did you have to do?
* BOOM! Ruby comes with a native array shuffling method.

```ruby
numbers = [ 1, 2, 3, 4, 5 ]
numbers.shuffle
# => [ 4, 2, 1, 5, 3 ]
```

#### Ranges (5min)

Don't have time to cover ranges, but read up on them on your own time. They may come in handy!

Use ranges to quickly generate arrays of data types.
* Parentheses.
* Min and max value, separated by two periods.
* Generate array using `.to_a` method.

```ruby
# Generate array of numbers from 1 to 5 in increasing order.
(1..5).to_a
# => [ 1, 2, 3, 4, 5 ]

# Does it work on strings?
("a".."z").to_a
```


#### Hashes (Objects) (10min)

A unordered, "dictionary-like" collection organized by key-value pairs. Very similar to Javascript objects, but with some differences.
* Curly brackets
* Can use colons or "hash rockets" ( `=>` )

Keys
* Can be strings or symbols
  * Symbols look a little different here. Reverse notation of symbol_name followed by `:`
  * Latest convention is to use symbols over strings. Both are OK though.


```ruby
# Keys as strings
# We can store any data type in hashes, including nested arrays and hashes.
peanut_butter = {
  "teacher" => "Adrian",
  "students" => [ "Donut", "Peter", "Nayana" ],
  "classroom" => 2,
  "in_session" => true,
  "schedule" => {
                    "morning" => "Ruby Basics",
                    "afternoon" => "Enumeration"
                }
}

# Keys as symbols
peanut_butter = {
  teacher: "Adrian",
  students: [ "Donut", "Peter", "Nayana" ],
  classroom: 2,
  in_session: true,
  schedule: {
              morning: "Ruby Basics",
              afternoon: "Enumerables"
            }
}
```

The way you access values in a hash depends on what type of key you use.

```ruby
# If your keys are strings...
peanut_butter["teacher"]
# => "Adrian"

# If your keys are symbols...
peanut_butter[:teacher]
# => "Adrian"
```

The same goes for modifying hash values.

```ruby
# String keys
peanut_butter["teacher"] = "Andy"
# => "Andy"

# Symbol keys
peanut_butter[:teacher] = "Andy"
# => "Andy"
```

##### Hash Methods

Like arrays, Ruby also provides us with a library of hash methods.  
* [Documentation](http://ruby-doc.org/core-2.2.0/Hash.html)

##### Keys

Returns an array with all the keys in a hash.

```ruby
peanut_butter.keys
# => [ :teacher, :students, :classroom, :inSession?, schedule ]
```

##### Merge

Combines two hashes.

```ruby
classroom = {
  room: "Peanut Butter"
}

squads = {
  squad_one: "Elixir",
  squad_two: "Fortran",
  squad_three: "Ada"
}

updated_clasroom = classroom.merge( squads )
```

### BREAK (10min)

### Conditionals (10min)

#### If-Else

Pretty similar to Javascript, with some differences.
* No parentheses or curly brackets required.
* Begin blocks using `if`, `elsif` (no second "e"!) and `else`
* We close the whole loop using `end`.
  - This will be used throughout Ruby when dealing with code blocks (e.g., method/function).

Here's an example where we check for height at a roller coaster...

```ruby
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

#### Case

Don't have time to cover ranges, but read up on them on your own time. They may come in handy!

Just like Javascript's `switch` statement. Here's an example that displays a certain greeting depending on a language input.
* Note that the default case begins with `else`

```ruby
puts "Hello there! Give me a language: "
language = gets.chomp.to_s

case language
when "spanish"
  puts "Hola!"
when "french"
  puts "Bonjour!"
when "wookie"
  puts "URRAAGGARHRHH"
else
  puts "I don't know #{language}!"
end
```

### Methods (10min)

The equivalent of Javascript "functions."
* Many things are referred to as "methods" in Ruby. Right now, we'll be taking about methods that are not attached to an object (e.g., array, hash).

Components
* `def` - the Ruby equivalent of `function`
* `double` - the method name in the below example
* `number` - the argument name in the below example
* `end` - closes the method

```ruby
# A method that doubles a number. A number-to-be-doubled is taken in as an argument.
def double( number )
  doubled_number = number * 2
  return doubled_number
end
```

You may have noticed that we use the same `return` notation as Javascript. This is called an **explicit return**, because we identify what exactly we want returned from the function.  

Ruby also lets us make **implicit returns**. This means that when we do not use the `return` keyword, Ruby will automatically return the value of the last line of code in the method.
* We encourage you to use **explicit returns** so we know exactly what your method is returning.

```ruby
# A method that doubles a number. A number is taken in as an argument.
def double( number )
  doubled_number = number * 2
  doubled_number
end

double( 3 )
# => 6

# Without parentheses does the same thing.
double 3
# => 6
```

Ruby methods can also establish default argument values.
* In the below example, if we do not provide our `double` method with an argument, it will default to 5.

```ruby
def double( number=5 )
  doubled_number = number * 2
  puts "Your doubled number is #{doubled_number}"
  return doubled_number
end

# No arguments. Just call the function (i.e., type out its name).
double
# => 10
```

### Exercise: Temperature Converter (Part II) (30min)

[Temperature Converter (Ruby)](https://github.com/ga-dc/temperature_converter_ruby)
