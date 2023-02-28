## Integer

Ruby differentiates between whole numbers, or `Integer`s, and decimal numbers, or `Float`s.

 ```ruby
7.class # => Integer
7.0.class # => Float
```

(In fact, you can always call the method `.class` on _any_ object, ever, at any time, to ask it what class it is.)

We'll learn about integers first.

###  Syntax

`Integer`s begin with a digit (0-9) and end when Ruby meets anything other than a digit (a space, a comma in an array, a closing parentheses at the end of method arguments, etc) — _except_ for underscores, which you can use as a delimiter if it helps to understand the number:

```ruby
10000000    # Is this 1 million? 100 million?
10_000_000  # Ah, it's easier to tell now.
```

###  Methods

Let's experiment with some common methods for `Integer`s:

#### + - * / % ** (math)

We, of course, have the standard math methods, like the calculator language. These methods all have the same syntactic sugar that the `String` versions did, so we can say `12 + 5` rather than `12.+(5)` (thankfully).

Try each of the following:

```ruby
12 + 5
12 - 5
12 * 5
12 / 5
```

<div class="experiment" markdown="1">
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/add-subtract-multiply-divide-exponent){:target="_blank"}
</div>

Whoa! Did you get what you expected for that last one?

It turns out that the `Integer` version of division will only return another `Integer`, and so `/` only returns the whole part (like in elementary school). If you want the remainder, you have to use the `%` (called the "modulus") operator. Try this:

```ruby
12 % 5
```

Another maybe unexpected thing: raising a number to a power, e.g. 3<sup>2</sup>, is not done using the `^` like in many other computing environments. Instead, use the double-star `**` operator:

```ruby
3 ** 2
```

Once you've played with the REPL, it's time to move into the graded project environment.

<div class="proj" markdown="1">

  Open the Gitpod `Integer` project on Canvas that follows this reading and start with the exercise `math.rb`.

  For a Gitpod refresher, see [this section](https://learn.firstdraft.com/lessons/9#start-the-gitpod-project){:target="_blank"} in `String`, where we opened our first workspace.
</div>

----

#### Quiz Question

- Let's recall: Of the options below, how do we typically store user input in our code?
- `the_users_input = puts`
    - Not quite, maybe have a look at the previous String lesson again
- `the_users_input = input.chomp`
    - Not quite, maybe have a look at the previous String lesson again
- `gets`
    - Yes, but what do we add to remove the newline character?
- `gets.chomp`
    - Yes, but how do we actually _store_ the data.
- `the_users_input = gets.chomp`
    - Correct!
{: .choose_best #gets_chomp points="10" answer="5" }

----

#### odd? and even? 

The `.odd?` and `.even?` methods return `true` or `false` based on whether the number is, well, odd or even. Don't be thrown off by the question mark at the end of the method name — it's nothing special, just another letter. Rubyists like to end method names with a question mark when methods return `true` or `false`.

```ruby
p 7.odd?
```

<div class="experiment" markdown="1">
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/odd){:target="_blank"}
</div>

#### rand 

There's another special method like `p` that we are allowed to call "in space", i.e. not on the right side of a dot, called `rand`. It returns a random number, and is very useful for all kinds of stuff, everything from games to statistical analysis:

<aside markdown="1">
`rand` is another method defined on `Kernel`, so the longhand would be `Kernel.rand(6)`.
</aside>

```ruby
rand(6) # => returns a random integer between 0 and 5
```

Somewhat oddly, `rand(n)` will return a random integer between `0` and `n - 1` rather than between `1` and `n`. That may seem surprising, but it's actually pretty handy because a lot of times what we want to do is generate a random _offset_ and it's convenient for that to include 0 as a possibility.

Give it a try:

```ruby
# random number between 0 and 8
p rand(9)
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/rand){:target="_blank"}
</div>

----

#### Quiz Question

- Trying to run `rand("9")` results in...
- `no implicit coversion of String into Integer`
    - Yes! Another error message! We'll see how to solve it below.
- A random number between 0 and 8
    - Really? Did you try it?
- `no implicit conversion of Integer into String`
    - Really? Did you try it?
{: .choose_best #rand_string points="10" answer="1" }

----

#### String#to_i 

Let's go back to `String` for a moment and talk about the method `to_i`. (We write `Object#method` often, and we'll see in a later lesson how it is different from `Object.method`.)

Sometimes you have a string that contains a number, usually input from a user, and want to do math on it. `to_i` will attempt to convert a `String` object into an `Integer` object.

```ruby
p "8".to_i
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/toi){:target="_blank"}
</div>

----

#### Quiz Question

- What would you add to the previous error code `rand("9")` to get it working?
- `rand("9").to_i`
    - Not quite. Think about the order of operations
- `rand.to_i("9")`
    - No, we want the argument "9" passed to `rand` not `to_i`
- `rand(9)`
    - Technically yes, but what would we _add_ to the code that we just learned about?
- `rand("9".to_i)`
    - Yes!
{: .choose_best #rand_fixed points="10" answer="4" }

----

<div class="proj" markdown="1">
  Return to the Gitpod `Integer` project and work through `odd.rb`
</div>

#### to_s 

Okay, back to `Integer` methods. We often will want to combine our `Integer`s with `String`s when crafting output for our users. Give it a try:

```ruby
lucky_number = rand(100)
p "Your lucky number is" + lucky_number
```

Uh oh! [RTEM](https://learn.firstdraft.com/lessons/7#seriously-please-read-the-error-message){:target="_blank"}!

It turns out that `String`'s `+` method can only add two strings together, not a string and an object of some other class. So, a lot of times we'll need to convert an `Integer` into a `String` prior to output. Fortunately `Integer` has a handy method, `to_s` (or "to string"), that does just that:

```ruby
p 98.to_s
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/tos){:target="_blank"}
</div>

<div class="proj" markdown="1">

  Return to the Gitpod `Integer` project and work through `birth_year.rb`
</div>

#### to_f 

Similar to `to_i`, there's a `to_f` (or "to float") method to convert an `Integer` to a `Float`, which is often handy for doing math, as we'll see next.

###  Conclusion

That's it for `Integer`. Next up, its close cousin: `Float`.

<span style="font-size: large">**Return to Canvas and head to the next part of the lesson**</span>

----