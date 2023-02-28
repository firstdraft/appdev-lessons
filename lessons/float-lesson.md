## Float

Ruby calls decimal numbers `Float`s. To create a `Float` rather than an `Integer`, just make sure to include a decimal point:

```ruby
5.class # => Integer
5.0.class # => Float
```

----

#### Quiz Question

- `"12".to_i.to_f` would return data of class?
- Float
    - Yes!
{: .free_text #to_f points="10" answer="1" }

----

### Methods

#### + - * / ** (math) 

The math methods work mostly like you'd expect, and similarly to the [ones for integers](https://learn.firstdraft.com/lessons/10#-------math){:target="_blank"}.

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

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/Float-math){:target="_blank"}
</div>

What did you discover? If _either_ side is a float, float division will be performed.

This is why `Integer`'s `.to_f` method can come in handy while doing math; at some point if you need to do division and need a fractional answer, then convert it to a `Float` first.

One other thing to keep in mind: you can use `**` in conjunction with fractions to calculate roots, since 9<sup>1/2</sup> is the same as the square root of 9, 8<sup>1/3</sup> is the same as the cube root of 8, etc.

```ruby
9 ** 0.5 # => 3.0
8 ** (1/3.0) # => 2.0
```

<div class="proj" markdown="1">

  Open the Gitpod `Float` project on Canvas that follows this reading and start with the exercise `find_hypotenuse.rb`.

  For a Gitpod refresher, see [this section](https://learn.firstdraft.com/lessons/9#start-the-gitpod-project){:target="_blank"} in `String`, where we opened our first workspace.
  
  _Remember_: the Pythagorean Theorem says that

  <!-- ![](assets/float/pythagorous.png) -->
  ![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677034341/pythagorous_axrds0.png)

  where `a` and `b` are the lengths of the shorter sides, and `c` is the length of the longest side. Read more about the formula [here](https://www.mathsisfun.com/pythagoras.html){:target="_blank"}.

</div>

#### round 

`Float`s can round themselves. Play around with the `.round` method:

```ruby
pi = 3.1415926535897932384626433832795028841976939937510
p pi.round(3)
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/round){:target="_blank"}
</div>

<div class="proj" markdown="1">

  Return to the Gitpod `Float` project and work through `round.rb`
</div>

#### rand 

The `rand` method that we met earlier can also be called with no arguments, in which case it returns a `Float` between 0 and 1. This is very handy for e.g. probabilities. Give it a try:

```ruby
p rand
```

<div class="experiment" markdown="1">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/float-rand){:target="_blank"}
</div>

###  Conclusion

That's it for `Float`. Next up, we'll learn to manipulate dates and times with the `Date` and `Time` classes.
