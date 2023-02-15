## Array

Next, we have a _very_ important class: `Array`. Most of what we do as developers is manage _lists of things_. Lists of photos, likes, followers, reviews, listings, messages, rides, events, concerts, projects, etc etc etc.

The first data type we're going to learn to help us manage lists of things is `Array`. This class, unlike the ones we've seen until now, is really just a _container_ for other objects, and can hold however many objects we want.

### Creating arrays

As always, we have the formal way of creating a new object in Ruby: use the `.new` method on the parent class:

```ruby
cities = Array.new
```

Try it out and see what you get if you `p cities`:

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/Arraynew){:target="_blank"}
</div>

#### push 

As you can see, Ruby represents an `Array` with square brackets, `[]`. The brand new array is empty; let's add some **elements** to it with the `.push` method. Try this:

```ruby
cities = Array.new

cities.push("Chicago")
cities.push("NYC")
p cities

cities.push("LA")
# Add some of your own, if you like
p cities
```

Now we're talking! We've stored multiple strings within a single array using the `.push` method. Ruby separates the elements in an array with commas.

<aside markdown="1">
You might come across a shorthand for `.push`, the `<<` method, known as the "shovel" operator. This allows you to write something like:

```ruby
cities.<<("Chicago")
```

Or with the syntactic sugar that we're very accustomed to by now:

```ruby
cities << "Chicago"
```

I personally prefer `.push` — I think it's more readable — but feel free to use the shovel if you like it better.
</aside>


#### Array literals 

Much like with `String`s, there's a shortcut to creating `Array`s. Rather than starting with `Array.new` and building it up from scratch one `.push` at a time, we can type an array "**literal**" directly into the code:

```ruby
cities = ["Chicago", "NYC", "LA"]
```

This is the technique that we'll be using most often.

### Methods

Now let's familiarize ourselves with some of `Array`'s methods.

#### at

After adding elements to the list, the next most important thing we need to be able to do is retrieve an element back out from the list. Our first tool for doing that is `.at`.

The `.at` method takes an `Integer` argument, which is interpreted as the position, or **index**, in the `Array` of the element that you want to retrieve. Give it a try:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

p cities
p cities.at(2)
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/array-at){:target="_blank"}
</div>

Whoa! Did you expect `cities.at(2)` to return `"LA"`? I sure didn't, the first time I tried it; I was expecting `"NYC"`.

It turns out that pretty much every programming language indexes the elements in an array starting at _zero_, not at one. So the first element is retrieved with `cities.at(0)`, the second element with `cities.at(1)`, etc. You'll get used to it after a while.

A couple of other things for you to experiment with:

 - What happens when you use an index greater than the length of the array?

    This is our first contact with `nil`, an object that represents **the absence of anything**. When you use an index "outside" the array, you might have expected to see an error message; but instead, Ruby returns `nil`.
 - What happens when you use a negative index?

#### at shorthand, [] 

There's a shorthand for `.at()` which is very common, so you should be familiar with it. It's the `.[]` method, so we _could_ write:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

p cities.[](2) # => "LA"
```

You guessed it — there's some syntactic sugar coming up. When a class has a method named `.[]`, Ruby allows the dot to be dropped, but the method name has to then move immediately next to the object it's being called on (no space), and the argument moves _inside_ the method name! Altogether, this allows us to write:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

p cities[2] # => "LA"
```

Which is sort of nice. I prefer `.at` because I think it reads better, but feel free to use the square brackets if you like that style better.

```ruby
array = [8, 3, 1, 19, 23, 3]

p array[2]
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/array-square-bracket){:target="_blank"}
</div>

#### first, last 

Since retrieving the elements at positions `0` (the first one) and `-1` (the last one) is so common, there are handy shortcut methods for those: `.first` and `.last`. Give them a try.

#### index 

The `.index` method is sort of the inverse of `.at`: given an object, `.index` searches within the array and returns the index where it resides. Give it a try:

```ruby
cities = ["Chicago", "NYC", "LA", "SF", "NOLA"]

p cities.index("SF")
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/array-index){:target="_blank"}
</div>

Some further things for you to experiment with:

 - What will `.index` return if the element is present in the array more than once?
 - What will `.index` return if the element is not present in the array at all?

#### String#split 

Before we proceed with more `Array` methods, I want to go back for a minute and talk about a method for the `String` class: `.split`. This method, when called on a `String`, will return an `Array` of substrings:

```ruby
"alice bob carol".split # => ["alice", "bob", "carol"]
```

If you provide no argument, the string is split upon whitespace, which is handy for e.g. turning a sentence into a list of words:

If you do provide an argument to `.split`, then the string will be chopped up wherever that argument occurs instead of whitespace — for example, use `"4,8,15,16,23,42".split(",")` to split on commas.

You can also `split` with the empty string, `""`, as an argument in order to turn a string into an `Array` of its individual characters:

```ruby
a = "Hello!".split("") # => ["H", "e", "l", "l", "o", "!"]
a.at(0) # => "H"
a.at(-1) # => "!"
```

**BENP: need an exercise here, split("") is important in .each project. Also, first time with negative indexing? Maybe insert something about this earlier in section (with exercise)**

This is particularly handy for us because it allows us to get a `String` of input from users with `gets` and then transform it into an `Array` for processing:

```ruby
p "Enter a series of numbers, separated by spaces:"

user_string = gets.chomp

user_numbers = user_string.split

length = user_numbers.count

p user_string
p user_numbers
p "You entered " + length.to_s + " numbers."
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/gets-with-split){:target="_blank"}
</div>

We'll be using this technique frequently to make things more interesting.

<div class="proj" markdown="1">

  Open the GitPod `Array` project on Canvas that follows this reading and start with the exercise `element_square.rb`.
  
  For a GitPod refresher, see the `String` reading where we opened our first workspace.
</div>

#### count 

`.count` counts how many elements are in the list, if called with no arguments. If an argument is provided, it counts how many times that argument occurs in the list.

```ruby
a = [8, 3, 1, 19, 23, 3]

p a.count

p a.count(3)
```

**BENP: add project with count() with an argument, becomes important again in .each**

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/count){:target="_blank"}
</div>

<div class="proj" markdown="1">
  
  Return to the GitPod `Array` project and work through `count.rb`
</div>
 
#### include? 

A thin convenience layer on top of `.count`, `.include?` will quickly tell you whether a value is present within an `Array`:

```ruby
a = [ "a", "b", "c" ]
a.include?("b")   # => true
a.include?("z")   # => false
```

#### exclude? 

Similar to `.include?`, but the opposite:

```ruby
a = [ "a", "b", "c" ]
a.exclude?("b")   # => false
a.exclude?("z")   # => true
```

#### reverse 

```ruby
array = [8, 3, 1, 19, 23, 3]

p array.reverse # => [3, 23, 19, 1, 3, 8]
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/array-reverse){:target="_blank"}
</div>

<div class="proj" markdown="1">
  
  Return to the GitPod `Array` project and work through `reverse.rb`
</div>

#### sort 

```ruby
array = [12, 4, 5, 13, 56, 32]

p array.sort # => [4, 5, 12, 13, 32, 56]
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/sort){:target="_blank"}
</div>

#### shuffle 

```ruby
array = [1, 2, 3, 4, 5]

p array.shuffle # Returns a copy of array in random order
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/shuffle){:target="_blank"}
</div>

#### sample 

```ruby
array = [8, 3, 1, 19, 23, 3]

p array.sample # => Returns a single random element from the array
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/sample){:target="_blank"}
</div>

#### min 

```ruby
a = [8, 3, 1, 19, 23, 3]

p a.min # => 1
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/min){:target="_blank"}
</div>

#### max 

```ruby
a = [8, 3, 1, 19, 23, 3]

p a.max # => 23
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/max){:target="_blank"}
</div>

<div class="proj" markdown="1">
  
  Return to the GitPod `Array` project and work through `min_max_difference.rb`
</div>

#### sum 

```ruby
a = [8, 3, 1, 19, 23, 3]

p a.sum # => 57
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/sum){:target="_blank"}
</div>

<div class="proj" markdown="1">
  
  Return to the GitPod `Array` project and work through `sum_elements.rb`
</div>

#### join 

You can think of `Array`'s `.join` method as the inverse of `String`'s `.split` method:

```ruby

"hello!".split("")
# => ["h", "e", "l", "l", "o", "!"]

["h", "e", "l", "l", "o", "!"].join
# => "hello!"
```

That is, the `.split` method is called on a `String` and returns an `Array` of substrings; while the `.join` method is called on an `Array` (where each element must be a `String`) and returns a single `String`.

###  Conclusion

That's it for `Array`s. Now we'll have a look at **conditionals** with `if` statements.