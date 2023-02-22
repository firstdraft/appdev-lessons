# The One Ruby Reference Part 1: Ruby Methods

This glossary should be used as a quick reference for Ruby; for more depth, click through to the "Full Explanation"s.

#### How to interpret this reference

This reference is organized by Ruby Class, e.g. `String`, `Array`, `Hash`, etc. Use the table of contents to find a section that interests you. Usually, each section describes a Ruby _method_. For example, here's what the section `String#split` looks like:

<!-- ![](assets/the-one-reference/how-to-use-the-one-reference.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677087530/how-to-use-the-one-reference_hseuda.png)

 - `String#split => Array` is called the _method signature_:
    - `String` since the method is defined for that class.
    - `#` since it is an instance method (as opposed to a class method, in which case the notation would be `.`).
    - `=> Array` since the _return value_ of this method is an instance of the class `Array`.
 - Then a description of the method.
 - Then examples.
 - Then, usually, a link to the longer explanation from the original chapter where the method was first introduced.

Please let us know if you find errors, omissions, or have any other suggestions or comments. Thank you!

## String

### .concat (.+)

`String#concat(Integer) ⇒ String`

or 

`String#concat(String) ⇒ String`

Appends the given arguments to a string. when given an integer as an argument, it converts the integer into ASCII code.  

```ruby
"hi".concat(33) # => "hi!"
```

```ruby
"Rub".concat(121)  # => "Ruby"
```

When given a string literal as an argument, it adds that string to the original string. `.+` or `+` is _similar_ to the `.concat` method. `+` will return a new combined `String` instead of modifying the original `String`. Each line of code below will give the same output.  

`"hi".concat(" there")`  
`"hi".+(" there")`  
`"hi" +(" there")`  
`"hi" + " there"`  

This method returns a new `String`.

[Full explanation](https://learn.firstdraft.com/lessons/9#string-addition-aka-){:target="_blank"} 

### \* method

Multiplies the original string by the given integer and returns the new modified `String`.

```ruby
"Ya" * 5
```

Returns `"YaYaYaYaYa"`

```ruby
"Ya" * 0
```

Returns `""`

[Full explanation](https://learn.firstdraft.com/lessons/9#string-multiplication-aka-){:target="_blank"}

### .upcase

`String#upcase ⇒ String`

Converts all lowercase letters to their uppercase counterparts in the given string and returns the new modified `String`.  

```ruby
"hello".upcase`
```

Returns

`"HELLO"`

[Full explanation](https://learn.firstdraft.com/lessons/9#upcase){:target="_blank"}

### .downcase

`String#downcase ⇒ String`

Converts all the uppercase letters to their lowercase counterparts from the given `String`. Returns the new modified `String`. 

```ruby
"HI".downcase`
```

Returns

`"hi"`

[Full explanation](https://learn.firstdraft.com/lessons/9#downcase){:target="_blank"}

### .swapcase

`String#swapcase ⇒ String`

Converts all the uppercase letters to their lowercase counterparts and lowercase letters to their uppercase counterparts from the given string. Returns the new modified `String`.  

```ruby
"Hi There".swapcase
```

Returns

`"hI tHERE"`

* * *

```ruby
"hI tHERE".swapcase
```

Returns

`"Hi There"`

[Full explanation](https://learn.firstdraft.com/lessons/9#swapcase){:target="_blank"}

### .reverse (String)

`String#reverse ⇒ String`

Returns a new `String` with the characters from the original String in reverse order.  

```ruby
"stressed".reverse
```

Returns

`"desserts"`  

[Full explanation](https://learn.firstdraft.com/lessons/21#reverse){:target="_blank"}

### .length

`String#length ⇒ Integer`

Returns the `Integer` number of charactersin the `String`.  

```ruby
"hippopotamus".length
```

Returns

`12`

[Full explanation](https://learn.firstdraft.com/lessons/21#length){:target="_blank"}

### .chomp

`String#chomp ⇒ String`

or

 `String#chomp(String) ⇒ String`

When not given any argument, removes the `"\n"` (newline) character from the end of the string. When given an argument of a charcter or a string, it remove that argument from the _end_ of the orginal string. 

Returns a new `String` with the character removed. 

```ruby
"Hey!\n".chomp  
"Hey!".chomp("!")  
"Hey There".chomp("There")  
"Hey!".chomp("y")
```

```ruby
"Hey!"  
"Hey"  
"Hey "  
"Hey!"
```

```ruby
p "What is your name?"
name = gets # supposes the user inputs "Clark" and then hits return
p "Hi" + name
```

Prints

`"Hi Clark\n"` 

```ruby
p "What is your name?"
name = gets # supposes the user inputs "Clark" and then hits return
p "Hi" + name.chomp
```

Prints

`"Hi Clark"`

```ruby
p "What is your name?"
name = gets.chomp # supposes the user inputs "Clark" and then hits return
p "Hi" + name
```

`"Hi Clark"`

[Full explanation](https://learn.firstdraft.com/lessons/9#chomp){:target="_blank"}

### .gsub

`String#gsub(String, String) ⇒ String`

Substitutes the all occurances of the first argument with the second argument in original string and returns a new `String` with the substitutes made.  

```ruby
"Hello".gsub("ello", "i")
```

Returns

`"Hi"`  

```ruby
"Hi.there".gsub(".", " ")
```

Returns

`"Hi there"`  

Giving an empty string as the second arugment deletes any occurences of the first arugument in the string.   

```ruby
"example @ ruby.com".gsub(" ", "")
```

Returns

`"example@ruby.com"` 

[Full explanation](https://learn.firstdraft.com/lessons/9#gsub){:target="_blank"}, and [explanation of advanced gsub](https://learn.firstdraft.com/lessons/21#advanced-gsub-techniques){:target="_blank"} with `Regexp`.

### .to_i (String)

`String#to_i  ⇒ Integer`

Converts a string literal that contains a number to an integer. The `Integer` is returned.  

```ruby
"8".to_i
```

Returns

`8`

```ruby
p "What is your lucky number?"
lucky_number = gets.chomp # Suppose the user types is "7" and then hits return
square = lucky_number ** 2 # This will throw an error.
```

Returns

`NoMethodError (undefined method '**' for "7":String)`

This is where the `.to_s` method comes handy.

```ruby
p "What is your lucky number?"
lucky_number = gets.chomp # Suppose the user types is "7" and then hits return
square = lucky_numbe.to_i ** 2 # This will throw an error.
p square
```

Returns

`"49"`

[Full explanation](https://learn.firstdraft.com/lessons/9#to_i){:target="_blank"}

### .strip

`String#strip  ⇒ String`

Removes all leading and trailing whitespace in the string.  

Returns a new `String` that has been modified from the original. 

```ruby
"   hi there ".strip
```

Returns

`"hi there"`

[Full explanation](https://learn.firstdraft.com/lessons/9#strip){:target="_blank"}

### .capitalize

`String#capitalize ⇒ String`

Capitalizes the first character of a string.

Returns a new `String` that has been modified from the original.

```ruby
"capitalize".capitalize
```

Returns

`"Capitalize"`

[Full explanation](https://learn.firstdraft.com/lessons/9#capitalize){:target="_blank"}

### .split

`String#split ⇒ Array`

or

`String#split(String) ⇒ Array`

Splits a string into an substrings and creates an Array of these substrings. when not given argument, `.split` uses whitespace to divide the string. when given an argument, `.split` divides the string on that argument.

Returns an `Array` of the divided `String`.

```ruby
"Hello hi byebye".split
```

Returns

`["Hello", "hi", "byebye"]`

```ruby
"one!two!three!".split("!")
```

Returns

`["one", "two", "three"]`

[Full explanation](https://learn.firstdraft.com/lessons/14#stringsplit){:target="_blank"}

### .include?

`String#include?(String) ⇒ Boolean`

Returns a `Boolean` (`true` or `false`) based on whether the string argument is inside the string the method is being called on.

```ruby
"Happy".include?("H")
```

Returns

`true`

```ruby
"Happy".include?("Z")
```

Returns

`false`

[Full explanation](https://learn.firstdraft.com/lessons/21#include){:target="_blank"}

## Integer

Whole numbers.

### Math Operations for the Integer Class

`12 + 5 # => 17`  
`12 - 5 # => 7`  
`12 * 5 # => 60`  
`12 / 5 # => 2`  
The `/` operator for integers only returns a whole number and omits the remainder.

[Full explanation](https://learn.firstdraft.com/lessons/10#-------math){:target="_blank"}

### `%` (modulus) operator

`Integer % Integer ⇒ Integer`

Returns the `Integer` remainder from a divisions.  

```ruby
13 / 5
```

Returns

`3`

[Full explanation](https://learn.firstdraft.com/lessons/10#-------math){:target="_blank"}

### `**` operator Integer

`Integer ** Integer ⇒ Integer`

Raises a number to a power.  

Returns an `Integer`

`3 ** 2 # => 9`  
`2 ** 3 # => 8`

[Full explanation](https://learn.firstdraft.com/lessons/10#-------math){:target="_blank"}

### .odd? and .even? method

`Integer#odd? ⇒ Boolean`

or

`Integer#even? ⇒ Boolean`

Returns a `Boolean` (`true` or `false`) based on whether the integer is odd or even.

`7.odd?`

Returns

`true`

`8.odd?`

Returns

`false`

`8.even?`

Returns

`true`

`7.even?`

Returns

`false`

[Full explanation](https://learn.firstdraft.com/lessons/10#odd-and-even){:target="_blank"}

### rand

`Integer#rand ⇒ Float`

or

`Integer#rand(Integer) ⇒ Integer`

or

`Integer#rand(Range) ⇒ Integer`

-   Creates a random `Float` (decimal number) between 0 to 1
-   Can be given an optional `Integer` argument that will generate and return an `Integer` between 0 and the argument.
-   Can be given an optional argument of a `Range` that will generate a random `Integer` that between the `Range`.

```ruby
rand           # returns => 0.21374618638...
rand(10)       # returns => 7
rand((10..20)) # returns => 19
```

[Full explanation](https://learn.firstdraft.com/lessons/10#rand){:target="_blank"}

### .to_s

`Integer#to_s ⇒ String`

Converts an integer to a string literal.

Returns a `String`

`8.to_s`

> "8"

```ruby
lucky_number = rand(10) # assigns a random integer between 0 to 9 to the variable lucky_number
p "My lucky number is " + lucky_number + "!" 
```

The above block of code won't work and will throw an error.

`TypeError (no implicit conversion of Integer into String)`

This is where the `.to_s` method comes handy. 

```ruby
lucky_number = rand(10) # assigns a random integer between 0 to 9 to the variable lucky_number
p "My lucky number is " + lucky_number.to_s + "!" 
```

> "My lucky number is 7!"

`"There are " + 7.to_s + " pineapples."`

> "There are 7 pineapples"

[Full explanation](https://learn.firstdraft.com/lessons/10#to_s){:target="_blank"}

### .to_f

`Integer#to_f ⇒ Float`

converts an integer to a `Float` (decimal number).  
`7.to_f`

> 7.0

```ruby
number = 10       #  
p number / 3      # Returns => 3
p number.to_f / 3 # Returns => 3.3333333333333335
```

[More examples below](https://learn.firstdraft.com/lessons/33#integer-and-float-division-examples){:target="_blank"}

[Full explanation](https://learn.firstdraft.com/lessons/10#to_f){:target="_blank"}

## Float

Decimal numbers.

### Math Operations for the Float Class

Standard operations are similar to those for the Integer class. The only exception is the `/` operator which returns fractional results.

```ruby
12 / 5     # => 2 
12.0 / 5.0 # => 2.4 
12 / 5.0   # => 2.4  
12.0 / 5   # => 2.` 
```

### `**` Float operator

`Float ** Float ⇒ Float`

The `**`operator for Floats can additionally be used to calculate roots. 

```ruby
9 ** 0.5     # => 3.0, since 9^(1/2) = sqaureroot of 9  
8 ** (1/3.0) # => 2.0, since 8^(1/3) = cuberoot of 8  
```

[Full explanation](https://learn.firstdraft.com/lessons/11#------math){:target="_blank"}

### .round

`Float#round ⇒ Integer`

or

`Float#round(Integer) ⇒ Float`

-   Returns the whole part (`Integer` of a decimal when not given any argument.  
-   When given an argument, returns a `Float` rounded to the number of decimal places specified by the argument.  

`3.14159.round # => 3`  
`3.14159.round(3) # => 3.142`  
`3.14139.round(3) # => 3.141`  

[Full explanation](https://learn.firstdraft.com/lessons/11#round){:target="_blank"}

### .to_i (Float)

`Float#to_i  ⇒ Integer`

Converts a float to an integer by rounding the float down to closest whole number.

Returns an `Integer`  

`"8.9".to_i`  

> 8

`"8.1".to_i`  

> 8

#### Integer and Float division examples

`12 / 5 # => 2`  
`(12 / 5).to_f # => 2.0`  
`12.to_f / 5 # => 2.4`  
`12 / 5.to_f # => 2.4`  
`(12.0 / 5 ).to_i # => 2`  
`(12 / 5.0).to_i # => 2`  

## Date

### Creating a Date

To use the Date class in a Ruby program, we need to say:  
`require "date"`  

**_Note:_**

Only _Ruby_ programs need to have a `require` statement for the Date class. _Rails_ already does this for you.

### Date.new

`Date.new ⇒ Date`

Use the `.new` method to create a new instance of a Date object. The `.new` method can be used with or without argument. When given no arguments, the default date is set to _Jan 1st, -4712 BCE_.

```ruby
Date.new                  # => #<Date: -4712-01-01 ((0j,0s,0n),+0s,2299161j)>
Date.new(2001)            # => #<Date: 2001-01-01 ...>
Date.new(2001,2,3)        # => #<Date: 2001-02-03 ...>
Date.new(2001,2,-1)       # => #<Date: 2001-02-28 ...>
```

[Full explanation](https://learn.firstdraft.com/lessons/12#datenew){:target="_blank"}

### Date.today

`Date.today ⇒ Date`

Initializes a Date object to the current date.

Returns a `Date`

`Date.today # => #<Date: 2019-04-16 ((2458590j,0s,0n),+0s,2299161j)>`  

[Full explanation](https://learn.firstdraft.com/lessons/12#datetoday){:target="_blank"}

### Date.parse()

`Date.parse(String) ⇒ Date`

Returns a `Date` object initialized to a date, interpreted from the given String argument.

```ruby
Date.parse("2001-02-03")   # => #<Date: 2001-02-03 ...>
Date.parse("20010203")     # => #<Date: 2001-02-03 ...>
Date.parse("3rd Feb 2001") # => #<Date: 2001-02-03 ...>
```

[Full explanation](https://learn.firstdraft.com/lessons/12#dateparse){:target="_blank"}

### Subtraction

Two dates can be subtracted from one another. The `-` operator returns a `Rational` which can be converted into an `Integer` to find the days in between the two dates.  

```ruby
number_of_days = Date.today - Date.parse("July 4, 1776") 
# => number_of_days = (88674/1)
number_of_days.to_i # => 88674
```

[Full explanation](https://learn.firstdraft.com/lessons/12#subtraction){:target="_blank"}

### Date.mday

`Date.mday ⇒ Integer`

Returns the day of the month (1-31).

```ruby
held_on = Date.new(2001,2,3)
held_on.mday # => 3
```

[Full explanation](https://learn.firstdraft.com/lessons/12#day){:target="_blank"}

### Date.wday

`Date.wday ⇒ Integer`

Returns the day of the week as an `Integer` (0-6, Sunday is 0).

```ruby
held_on = Date.new(2001,2,3)
held_on.wday # => 6
```

[Full explanation](https://learn.firstdraft.com/lessons/12#wday){:target="_blank"}

### Days of the Week

`Date#moday? ⇒ Boolean`

```ruby
date = Date.new
date.monday?    # => true if date is a Monday.
date.tuesday?   # => true if date is a Tuesday.
date.wednesday? # => true if date is a Wednesday.
date.thursday?  # => true if date is a Thursday.
date.friday?    # => true if date is a Friday.
date.saturday?  # => true if date is a Saturday.
date.sunday?    # => true if date is a Sunday.
```

Returns a `Boolean` (`true` or `false`), if this given `Date` is a particular day of the week.

[Full explanation](https://learn.firstdraft.com/lessons/12#monday){:target="_blank"}

## Array

List of objects represented with square brackets, \[].

### Creating an Array

`Array.new ⇒ Array`

initializes a new empty Array.  

[Full explanation](https://learn.firstdraft.com/lessons/14#creating-arrays){:target="_blank"}

`cities = Array.new # => cities = []`  
or  
`cities = [] # => cities = []` 

[Full explanation](https://learn.firstdraft.com/lessons/14#array-literals){:target="_blank"}

### .push

`Array#push(Object) ⇒ Array`

Adds elements to the end of an Array. Returns the modified `Array`.

```ruby
cities.push("Chicago")
cities.push("Los Angeles")
cities.push("New York City")
```

or  

```ruby
cities = ["Chicago", "Los Angeles", "New York City"]
# Initializes and adds elements to an Array
```

[Full explanation](https://learn.firstdraft.com/lessons/14#push){:target="_blank"}

### .at()

`Array#.at(Integer) ⇒ Object`

Takes an Integer argument and return the element in that position of an Array. The following lines of code show the various forms of the `.at` method and return the same output.

Returns an `Object`  

```ruby
cities = ["Chicago", "Los Angeles", "New York City"]
cities.at(2)  
cities.[](2){:target="_blank"}  
cities[2]
```

> `"New York City"`

**_Note:_**
1. Ruby indexes the elements in an array starting at _zero_, that is, the first element of an array will have the index _zero_.
2. Trying to access an element using an index greater than the length of the array will give you `nil`.  
`cities.at(3) # => nil`
3. Using a negative index will retrieve elements from the end of the least.  
`cities.at(-1) # => "New York City"`  
`cities.at(-2) # => "Los Angeles"`  
`cities.at(-3) # => "Chicago"`  
`cities.at(-4) # => nil` 

[Full explanation](https://learn.firstdraft.com/lessons/14#at){:target="_blank"}

### .first and .last

`Array#first ⇒ Object` or `Array#last ⇒ Object`

Retrieves and returns the first or the last element of an array.

Returns an `Object`

`cities.first # => "Chicago"`  
`cities.last) # => "New York City"`

[Full explanation](https://learn.firstdraft.com/lessons/14#first-last){:target="_blank"}

### .index

`Array#index(Object) ⇒ Integer`

Returns an `Integer` that is the index of an element.  
`cities.index("Los Angeles") # => 1`

[Full explanation](https://learn.firstdraft.com/lessons/14#index){:target="_blank"}

### .count

`Array#count ⇒ Integer` or `Array#count(Object) ⇒ Integer`

Returns the number of elements in a list, when give no arguments. If given an argument, returns the number of times that arguments occurs in the array. In both instances, this method returns an `Integer`

```ruby
nums = [8, 3, 1, 19, 23, 3]
nums.count # => 6
nums.count(3) # => 2
nums.count(2) # => 0
```

[Full explanation](https://learn.firstdraft.com/lessons/14#count){:target="_blank"}

### .reverse (Array)

`Array#reverse ⇒ Array`

Returns a new `Array`Array with the elements of the original Array but in the reversed order.  
`nums.reverse # => [3, 23, 19, 1, 3, 8]`

[Full explanation](https://learn.firstdraft.com/lessons/14#reverse){:target="_blank"}

### .sort

`Array#.sort ⇒ Array`

Returns a new `Array` with the elements of the original Array but in the sorted in increasing order.  
`nums.sort # => [1, 3, 3, 8, 19, 23]`

[Full explanation](https://learn.firstdraft.com/lessons/21#sort){:target="_blank"}

#### Example: Sorting an Array in decreasing order
```ruby
nums = [8, 3, 1, 19, 23, 3]
nums.sort # => [1, 3, 3, 8, 19, 23] 
nums.reverse # => [3, 23, 19, 1, 3, 8] 
nums.sort.reverse # => [23, 19, 8, 3, 3, 1], first sorts then reverses the Array. 
```
### .shuffle

`Array#shuffle ⇒ Array`

Returns a new `Array` with the elements of the original Array but with the order shuffled randomly.  
`nums.shuffle # => [3, 23, 8, 19, 1, 3]`  
`nums.shuffle # => [19, 3, 1, 8, 3, 23]` 

[Full explanation](https://learn.firstdraft.com/lessons/21#shuffle){:target="_blank"}

### .sample

`Array#sample ⇒ Array`

Returns a random element from the array.  
`nums.sample # => 23`  
`nums.sample # => 3`

[Full explanation](https://learn.firstdraft.com/lessons/14#sample){:target="_blank"}

### .min and .max

`Array#min ⇒ Object` or `Array#max ⇒ Object`

Retrieve the elements of minimum and the maximum values in the array.  
`nums.min # => 1`  
`nums.max # => 23`

[Full explanation](https://learn.firstdraft.com/lessons/14#min){:target="_blank"}

### .sum (Array)

`Array#sum`

Returns the sum of all the elements in the array.  
`nums.sum # => 57`

**Note** This method only works in the elements in the `Array` are _not_ a `Hash`.

[Full explanation](https://learn.firstdraft.com/lessons/14#sum){:target="_blank"}

## Hash

List of objects represented with curly brackets, {}. Unlike Arrays, each cell is not automatically numbered, but is rather given a label by us.

### Interlude: Symbol

Symbols are a sequence of characters and are used to to label something internally in the code. They are created by starting them off with a colon and follow the same naming conventions as variables, `:hello`.  
`:hello.class # => Symbol`

[Full explanation](https://learn.firstdraft.com/lessons/18#a-brief-interlude-symbols){:target="_blank"}

### Creating a Hash

`Hash.new ⇒ Hash`

`person1 = Hash.new`  
or  
`person2 = {}`

### .store

`Hash#store(Object, Object) ⇒ Object`

Adds elements to a Hash by taking two arguments, a label (or _key_) and a piece of data (or _value_).

This method returns the `Object` that was stored.

The `key` can be any type, although is usually a `Symbol`. The value can also be of any type.

```ruby
person1.store(:first_name, "Raghu")
person1.store(:last_name, "Betina")
person1.store(:role, "Instructor")
# => person1 = {:first_name=>"Raghu", :last_name=>"Betina", :role=>"Instructor"}
```

or we can fill up a hash by typing in the hash literal  
`person2 = { :first_name => "Jocelyn", :last_name => "Williams", :role => "Student" }`

**_Note:_**
1. Ruby represents each key/value pair by separating them with a `=>`, known as a "hash rocket."
2. If the value associated with a key already exists when you try to `.store` something under it, its value will be replaced.

[Full explanation](https://learn.firstdraft.com/lessons/18#creating-hashes-and-storing-values){:target="_blank"}

### .fetch

`Hash#fetch(Object) ⇒ Object`

or

`Hash#fetch(Object, Object) ⇒ Object`

Both `.fetch` and `.[]` can be used to retrieves the data held by a key.
`person1.fetch(:last_name)# => "Betina"`  
`person2.[:last_name] # => "Williams"` 

If `.fetch` is given key that is not present in the hash, it will throw an error. But `.[]` is given key that is not present in the hash, it returns `nil`. 

Fallback: pass in a second default argument that `.fetch` will return if the key is not present in the hash.  
`person1.fetch(:middle_name, "None provided") # => "None provided"`

[Full explanation](https://learn.firstdraft.com/lessons/18#fetch){:target="_blank"}

## Conditionals

Basic Anatomy of multibranch `if` statements:

```ruby
if condition1
  # do something if condition1 is true
elsif condition2
  # do something if condition2 is true
else # if both condition1 and condition2 were falsy
  # do something else
end
```

**Example:**

```ruby
p "Type a number less than 10 and greater than 0:"
user_input = gets.chomp.to_i # gets user input, removes newline character, converts the string to integer. 
if user_input == 5 
  p "You win!" # Will print this if the user input is 5
elsif user_input < 10 && user_input > 0 # check if the user input is valid
  p "You lose!" # Will print this if the user input is between 1 and 9
else
  p "You didn't type in a valid number." # Will print this if the user input is not between 1 and 9
end
```

**Don't forget the `end` keyword.**

[Full explanation](https://learn.firstdraft.com/lessons/15){:target="_blank"}

## Loops

**while statements:**  

```ruby
while boolean
  # ruby code here
end

⇒ nil
```
`while` is similar to `if`. The difference is everytime the execution of the program reaches the `end` it jumps back and evaluates the _truthiness_ of the condtion next to the `while` statement and decides whether or not to execute the code within the `while` loop.

```ruby
while condition 
  # do something while condition is true
end # jump back to the while statement
```

**Example:**

```ruby
limit = 5
while limit > 0 
  p limit
  limit = limit - 1
end 
```

> 5  
> 4  
> 3  
> 2  
> 1  

**_Note:_**  
If the condition next to the `while` always evaluates to be "truthy," then the program will be stuck in a neverending loop, infamously known as an
**infinite loop**.

[Full explanation](https://learn.firstdraft.com/lessons/16#while-conditionally-doing-something-multiple-times){:target="_blank"}

## Blocks

### .times

```shell
Integer#times do
  # ruby code here
end

⇒ Integer
```

or

```shell
Integer#times do |Integer|
  # ruby code here
end

⇒ Integer
```

The `.times` method takes a [`Block`](https://learn.firstdraft.com/lessons/16#blocks){:target="_blank"} as an argument and will execute the code within that block the number of times specified by the integer. A `Block` of code is the code written in between the keywords `do` and `end`. This looping method returns an `Integer` of the number of times the loop ran.

```ruby
10.times do
  p "Hi"
end
```

The above block of code will print "Hi" 10 times all on newlines. 

To keep a track of the iteration number, `.times` can create a [block variable](https://learn.firstdraft.com/lessons/16#block-variables){:target="_blank"} that starts of counting the iteration number starting at _zero_. After each execution of the code within the block, the block variable is incremented by 1.  

```ruby
10.times do |counter|
  p counter
end
```

The above block of code will print the numbers 0 to 9 all on newlines.

[Full explanation](https://learn.firstdraft.com/lessons/16#blocks){:target="_blank"}

#### Other methods

### .upto

```shell
Integer#upto do |Integer|
  # ruby code here
end

⇒ Integer
```
The `upto` method takes the first `Integer` the method is called on and uses it to initialize the value of
the block variable. The second `Integer` becomes the stopping condition to the loop as the block variable'
increases by one after each iteration. The method returns an `Integer`; the initial value of the block variable. 

```ruby
5.upto(10) do |counter|
  # do something
end
```

The above block of code starts the block variable `counter` at 5 and executes the block until counter is 10.

### .downto

```shell
Integer#downto do |Integer|
  # ruby code here
end

⇒ Integer
```
The `downto` method takes the first `Integer` the method is called on and uses it to initialize the value of
the block variable. The second `Integer` becomes the stopping condition to the loop as the block variable'
decreases by one after each iteration. The method returns an `Integer`; the initial value of the block variable.

```ruby
10.downto(5) do |counter|
  # do something
end
```

The above block of code starts the block variable `counter` at 10 and executes the block until counter is 5. 

### .step

```shell
Integer#step(Integer, Integer) do |Integer|
  # ruby code here
end

⇒ Integer
```
The `step` method initializes the block variable to be the value of the `Integer` that called the method. The first `Integer` argument is the the value the block variable is when the loop will stop. The last `Integer`argument is what value to modify the block variable  after each iteration. This method returns the `Integer` that called the method. 

```ruby
1.step(10, 3) do |counter|
  p counter
end
```

> 1  
> 4  
> 7  
> 10  

The above block of code starts the block variable `counter` at 1 and executes the block until counter is 10 but after each iteration the `counter` will be incremented by 3 instead of 1. `.step` can also be used to decrement the counter by a certain value. 

```ruby
10.step(1, -4) do |counter|
  p counter
end
```

> 10  
> 6  
> 2  

## Looping through Arrays

### .each

```shell
Array#each do |Object|
  # ruby code here
end

⇒ Array
```

Given an array, the `.each` method will loop through each element of the array starting with the very first one.

Returns the `Array` the method was called on.

```ruby
cities = ["Chicago", "LA", "NYC"]
cities.each do |city|
  p city
end
```

```ruby
"Chicago"  
"LA"  
"NYC"
```

The block variable `city` holds the value of the elements in the array `cities`. It starts with the first element `"Chicago"` and then changes with each interation, holding the value of the next element (`"LA"`) in the array and so on.

[Full explanation](https://learn.firstdraft.com/lessons/17#arrays-each-method){:target="_blank"}

### .each_with_index

```shell
Array#each_with_index do |Object, Integer|
  # ruby code here
end

⇒ Array
```

To keep a track of the iteration number while looping through an array, `.each_with_index` creates an additional block variable that starts of counting the iteration number starting at _zero_. After each execution of the code within the block, the block variable is incremented by 1.  

```ruby
cities.each_with_index do |city, count|
  p count.to_s + " " + city
end
```

```ruby
"0 Chicago"  
"1 LA"  
"2 NYC"
```

`city` holds the value of elements in the array `cities`. `count` holds the index of the element that `city` currently holds. 

**_Note:_**  
Variables created as a block variables can only be used within that block (between `do` and `end`). Using that variable outside that block will throw an error.

[Full explanation](https://learn.firstdraft.com/lessons/21#each_with_index){:target="_blank"}
