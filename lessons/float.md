## Float

Ruby calls decimal numbers `Float`s. To create a `Float` rather than an `Integer`, just make sure to include a decimal point:

```ruby
5.class # => Integer
5.0.class # => Float
```

### Methods

#### + - * / ** (math)

The math methods work mostly like you'd expect, and similarly to [the ones for integers](#integer-math).

The main difference to keep in mind is with `/`. Division with floats works the way that we're used to — it returns fractional results, as a `Float`:

```ruby
12.0 / 5.0 # => 2.4
```

Try the following and see what you get:

```ruby
12 / 5
12.0 / 5
12 / 5.0
```

<mark>✏️ **Exercise:**</mark> [Click here for a REPL to try it.](https://repl.it/@raghubetina/Float-math){target="_blank"}

What did you discover? If _either_ side is a float, float division will be performed.

This is why `Integer`'s `.to_f` method can come in handy while doing math; at some point if you need to do division and need a fractional answer, then convert it to a `Float` first.

One other thing to keep in mind: you can use `**` in conjunction with fractions to calculate roots, since 9<sup>1/2</sup> is the same as the square root of 9, 8<sup>1/3</sup> is the same as the cube root of 8, etc.

```ruby
9 ** 0.5 # => 3.0
8 ** (1/3.0) # => 2.0
```

##### Start the GitPod Project {-}

Open the GitPod project for this chapter and start with the exercises. [See prior steps][Start the GitPod Project for Integer] as a reminder. Fork the project from GitHub: [https://github.com/bpurinton-appdev/float-chapter/tree/bp-additions](https://github.com/bpurinton-appdev/float-chapter/tree/bp-additions){target="_blank"}.

<mark>✏️ **Exercise:**</mark> Work through `float_find_hypotenuse.rb`. _Remember_: the Pythagorean Theorem says that

![](assets/float/pythagorous.png)

where `a` and `b` are the lengths of the shorter sides, and `c` is the length of the longest side. Read more about the formula [here](https://www.mathsisfun.com/pythagoras.html){target="_blank"}.

#### round

`Float`s can round themselves. Play around with the `.round` method:

```ruby
pi = 3.1415926535897932384626433832795028841976939937510
p pi.round(3)
```

<mark>✏️ **Exercise:**</mark> [Click here for a REPL to try it.](https://repl.it/@raghubetina/round){target="_blank"}

<mark>✏️ **Exercise:**</mark> Return to the GitPod `Float` project and work through `float_round.rb`

#### rand

The `rand` method that we met earlier can also be called with no arguments, in which case it returns a `Float` between 0 and 1. This is very handy for e.g. probabilities. Give it a try:

```ruby
p rand
```

<mark>✏️ **Exercise:**</mark> [Click here for a REPL to try it.](https://repl.it/@raghubetina/float-rand){target="_blank"}

###  Conclusion

That's it for `Float`. Next up, we'll learn to manipulate dates and times with the `Date` and `Time` classes.

### Addendum: Even more Float methods

Looking for even more Float methods? See [here][More Float methods] for some additional methods added by the `activesupport` gem (automatically available within Ruby on Rails).