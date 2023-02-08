## Float

Ruby calls decimal numbers `Float`s. To create a `Float` rather than an `Integer`, just make sure to include a decimal point:

```ruby
5.class # => Integer
5.0.class # => Float
```

### Methods

#### + - * / ** (math) {-}

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

<div class="experiment">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/Float-math){target="_blank"}
</div>

What did you discover? If _either_ side is a float, float division will be performed.

This is why `Integer`'s `.to_f` method can come in handy while doing math; at some point if you need to do division and need a fractional answer, then convert it to a `Float` first.

One other thing to keep in mind: you can use `**` in conjunction with fractions to calculate roots, since 9<sup>1/2</sup> is the same as the square root of 9, 8<sup>1/3</sup> is the same as the cube root of 8, etc.

```ruby
9 ** 0.5 # => 3.0
8 ** (1/3.0) # => 2.0
```

##### Start the GitPod Project {-}

<div class="proj">

  Open the GitPod `Float` project for this chapter and start with the exercise `float_find_hypotenuse.rb`:

  LTI{Load assignment}(https://github.com/bpurinton-appdev/float-chapter/tree/bp-additions)[MV4dKHMwdAFhfRn752YW3TAY]{KBpPhe42o6wDRi35rWagKY4F}(20)[float_project] 
  
  For a GitPod refresher, [see here](#start-gitpod-project).
  
  _Remember_: the Pythagorean Theorem says that

  ![](assets/float/pythagorous.png)

  where `a` and `b` are the lengths of the shorter sides, and `c` is the length of the longest side. Read more about the formula [here](https://www.mathsisfun.com/pythagoras.html){target="_blank"}.

</div>

#### round {-}

`Float`s can round themselves. Play around with the `.round` method:

```ruby
pi = 3.1415926535897932384626433832795028841976939937510
p pi.round(3)
```

<div class="experiment">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/round){target="_blank"}
</div>

<div class="proj">

  Return to the GitPod `Float` project and work through `float_round.rb`
</div>

#### rand {-}

The `rand` method that we met earlier can also be called with no arguments, in which case it returns a `Float` between 0 and 1. This is very handy for e.g. probabilities. Give it a try:

```ruby
p rand
```

<div class="experiment">
  
  [Click here for a REPL to try it.](https://repl.it/@raghubetina/float-rand){target="_blank"}
</div>

###  Conclusion

That's it for `Float`. Next up, we'll learn to manipulate dates and times with the `Date` and `Time` classes.

#### Addendum: Even more Float methods {-}

Looking for even more Float methods?

Ruby on Rails enhances certain Ruby classes with additional convenience methods that aren't included in plain ol' Ruby. Many of these are included in the `activesupport` gem that comes with Rails; you could also include it in a pure Ruby program if you wanted to.

 - To use the following methods within Ruby on Rails, you don't have to do anything.
 - To use the following methods in a plain Ruby script, include the line:

    ```ruby
    require 'activesupport'
    ```

##### Formatting Floats as Strings {-}

As we know, you can call the `.to_s` method on a Float to convert the number into a String:

```ruby
10.25.to_s # => "10.25"
```

Within a Rails application[^Rails], you can provide a `Symbol`[^Symbol] as an argument to `Float`'s `to_s` method. This allows you to convert the `Float` to a `String` _and_ add additional formatting at the same time.

[^Rails]:  Or anywhere using `activesupport`.

[^Symbol]: A `Symbol` is a Ruby Class that is similar to a `String`. Symbols start with a colon (`:`) at the beginning. See the chapter section [here][A brief interlude: Symbols]. 

##### Phone {-}

```ruby
5551234.to_s(:phone) # => "555-1234"
```

In addition to providing a `Symbol` to the `to_s` method, you can provide an _additional_ `Hash`[^Hash] argument to tweak the some finer details about how we want to format the Float.

```ruby
1235551234.to_s(:phone, { :area_code => true }                     # => "(123) 555-1234"
1235551234.to_s(:phone, { :country_code => 1 } )                   # => "+1-123-555-1234"
1235551234.to_s(:phone, { :area_code => true, :extension => 555 }) # => (123) 555-1234 x 555
```

[^Hash]: A `Hash` is another Class is Ruby that. See the [Hash chapter](#hash-chapter). Until you read that chapter, just be aware that this kind of formatting is possible and easy to do in a Rails application.

##### Currency {-}

```ruby
1234567890.50.to_s(:currency)                  # => "$1,234,567,890.50"
67890.506.to_s(:currency, { :precision => 3 }) # => "$67,890.506"
```

##### Percentage {-}

```ruby
100.to_s(:percentage)                                            # => "100.000%"
100.to_s(:percentage, { :precision => 0 } )                      # => "100%"
1000.to_s(:percentage, { :delimiter => ".", :separator => "," }) # => "1.000,000%"
```
