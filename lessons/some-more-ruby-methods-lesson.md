## Some more Ruby methods

Here are some more Ruby methods that we didn't cover in the previous sections, but which will likely come in handy in some of the Ruby Gym exercises. Of course, these are also collected in [The One Ruby Reference](https://learn.firstdraft.com/lessons/33){:target="_blank"} for quick reference.

### More String 

#### reverse 

The reverse method returns a new `String` with the characters from the `String` in reverse order.

```ruby
p "I can speak in backwords words".reverse
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/reverse){:target="_blank"}
</div>

#### length 

The length method  returns the number of characters (as an `Integer`) that a `String` has.

```ruby
p "Supercalifragilisticexpialidocious".length
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/length){:target="_blank"}
</div>

#### include? 

`include?` takes a String argument and returns `true` or `false` if the argument exists in the String that `include?` is called on.

```ruby
p "Happy Days".include?("H")

p "Happy Days".include?("Z")
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/stringinclude){:target="_blank"}
</div>

#### Advanced gsub techniques 

[`gsub`](https://learn.firstdraft.com/lessons/9#gsub){:target="_blank"} also supports accepting a _regular expression_ as its first argument. We won't get into regular expressions in detail right now, but all languages (C, C++, Python, etc.) include a way to write regular expressions and they are a very powerful way to check whether input strings match certain patterns.

In Ruby, we work with regular expressions the way we work with everything else — via a class, `Regexp`. We create `Regexp` _literals_ with forward slashes (like we use quotes to create `String` literals), and then put the pattern that we're trying to match between the slashes.

For now, we're just going to copy-paste a few simple regexes that come in handy with `gsub`, in particular:

<aside markdown="1">
If your project requires scanning text for patterns, then [RegexOne](https://regexone.com/){:target="_blank"} is a good resource for learning more. [Rubular](https://rubular.com/){:target="_blank"} is handy for quickly testing your regular expressions against some example strings.
</aside>

 - `/\s+/` matches all whitespace, so we can use it with `gsub` to _remove_ all whitespace:

    ```ruby
    "Hello there,\nfriend".gsub(/\s+/, "") # => "Hellothere,friend"
    ```
 - `/[^0-9]/` matches everything _except_ numeric digits, so we can use it with `gsub` to _remove_ everything except digits:

    ```ruby
    "March 29th!".gsub(/[^0-9]/, "") # => "29"
    ```
 - `/[^a-z]/i` matches everything _except_ letters (case-insensitively using the `i` mode after the `//` slashes). So we can use it with `gsub` to _remove_ everything except letters:

    ```ruby
    "March 29th!".gsub(/[^a-z]/i, "") # => "Marchth"
    ```
 - `/[^a-z0-9\s]/i` matches everything _except_ letters, digits, and whitespace, so we can use it to remove everything except for those:

    ```ruby
    "March 29th!".gsub(/[^a-z0-9\s]/i, "") # => "March 29th"
    ```

### More Float

Looking for even more Float methods?

Ruby on Rails enhances certain Ruby classes with additional convenience methods that aren't included in plain ol' Ruby. Many of these are included in the `activesupport` gem that comes with Rails; you could also include it in a pure Ruby program if you wanted to.

 - To use the following methods within Ruby on Rails, you don't have to do anything.
 - To use the following methods in a plain Ruby script, include the line:

    ```ruby
    require 'activesupport'
    ```

#### Formatting Floats as Strings 

As we know, you can call the `.to_s` method on a Float to convert the number into a String:

```ruby
10.25.to_s # => "10.25"
```

Within a Rails application (or anywhere using `activesupport`), you can provide a `Symbol` as an argument to `Float`'s `to_s` method. This allows you to convert the `Float` to a `String` _and_ add additional formatting at the same time.

<aside markdown="1">
Recall from the [`Hash` chapter](https://learn.firstdraft.com/lessons/18#a-brief-interlude-symbols){:target="_blank"}, a `Symbol` is a Ruby Class that is similar to a `String`. Symbols start with a colon (`:`) at the beginning.
</aside>

##### Phone 

```ruby
5551234.to_s(:phone) # => "555-1234"
```

In addition to providing a `Symbol` to the `to_s` method, you can provide an _additional_ `Hash` argument to tweak the some finer details about how we want to format the Float.

```ruby
1235551234.to_s(:phone, { :area_code => true }                     # => "(123) 555-1234"
1235551234.to_s(:phone, { :country_code => 1 } )                   # => "+1-123-555-1234"
1235551234.to_s(:phone, { :area_code => true, :extension => 555 }) # => (123) 555-1234 x 555
```

##### Currency 

```ruby
1234567890.50.to_s(:currency)                  # => "$1,234,567,890.50"
67890.506.to_s(:currency, { :precision => 3 }) # => "$67,890.506"
```

##### Percentage 

```ruby
100.to_s(:percentage)                                            # => "100.000%"
100.to_s(:percentage, { :precision => 0 } )                      # => "100%"
1000.to_s(:percentage, { :delimiter => ".", :separator => "," }) # => "1.000,000%"
```

### More Array

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

#### join 

You can think of `Array`'s `.join` method as the inverse of [`String`'s `.split` method](https://learn.firstdraft.com/lessons/14#stringsplit){:target="_blank"}:

```ruby

"hello!".split("")
# => ["h", "e", "l", "l", "o", "!"]

["h", "e", "l", "l", "o", "!"].join
# => "hello!"
```

That is, the `.split` method is called on a `String` and returns an `Array` of substrings; while the `.join` method is called on an `Array` (where each element must be a `String`) and returns a single `String`.

### More .each

#### each_with_index 

There are some rare cases when you are looping over an array and, within the block, you would like access to the element _and_ its index. For example, maybe you want to print a line after every other element. You could fall back to `.times` in these scenarios, but there's also another `Array` method that has your back: `.each_with_index`. It looks like this:

```ruby
p "Enter at least 2 words, separated by spaces:"
user_words = gets.chomp.split
p "user_words:"
p user_words

user_words.each_with_index do |the_word, the_index|
  p the_word.capitalize
  p the_word.reverse
  p the_word.upcase

  if the_index.odd?
    p "=" * 20
  end
end
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/each-each-with-index){:target="_blank"}
</div>

As you can see, some methods provide more than one block variable. `.each_with_index` allows you to name two variables within the pipes; the first one will receive the element, and the second one will receive the index of the iteration. Within the block you can use both variables as you see fit. In rare cases, handy.

----