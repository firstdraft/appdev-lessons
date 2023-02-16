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

  Open the GitPod `Integer` project on Canvas that follows this reading and start with the exercise `math.rb`.

  For a GitPod refresher, see the `String` reading where we opened our first workspace.
</div>

#### odd? and even? 

The `.odd?` and `.even?` methods return `true` or `false` based on whether the number is, well, odd or even. Don't be thrown off by the question mark at the end of the method name — it's nothing special, just another letter. Rubyists like to end method names with a question mark when methods return `true` or `false`.

```ruby
p 7.odd?
```

<div class="experiment" markdown="1">
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/odd){:target="_blank"}
</div>

<div class="proj" markdown="1">
  Return to the GitPod `Integer` project and work through `odd.rb`
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

#### to_s 

We often will want to combine our `Integer`s with `String`s when crafting output for our users. Give it a try:

```ruby
lucky_number = rand(100)
p "Your lucky number is" + lucky_number
```

Uh oh! RTEM!

It turns out that `String`'s `+` method can only add two strings together, not a string and an object of some other class. So, a lot of times we'll need to convert an `Integer` into a `String` prior to output. Fortunately `Integer` has a handy method, `to_s` (or "to string"), that does just that:

```ruby
p 98.to_s
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/tos){:target="_blank"}
</div>

#### to_f 

Similarly, there's a `to_f` (or "to float") method to convert an `Integer` to a `Float`, which is often handy for doing math, as we'll see next.

<div class="proj" markdown="1">

  Return to the GitPod `Integer` project and work through `birth_year.rb`
</div>

###  Conclusion

That's it for `Integer`. Next up, its close cousin: `Float`.