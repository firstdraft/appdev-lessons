## Addendum: Some more Ruby methods

Here are some more Ruby methods that we didn't cover in the chapters, but which will likely come in handy in some of the Ruby Gym exercises. Of course, many of these are also collected in the long Ruby reference.

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

`gsub` also supports accepting a _regular expression_ as its first argument. We won't get into regular expressions in detail right now, but all languages (C, C++, Python, etc.) include a way to write regular expressions and they are a very powerful way to check whether input strings match certain patterns.

In Ruby, we work with regular expressions the way we work with everything else — via a class, `Regexp`. We create `Regexp` _literals_ with forward slashes (like we use quotes to create `String` literals), and then put the pattern that we're trying to match between the slashes.

For now, we're just going to copy-paste a few simple regexes[^regexone] that come in handy with `gsub`, in particular:

[^regexone]: If your project requires scanning text for patterns, then [RegexOne](https://regexone.com/){:target="_blank"} is a good resource for learning more. [Rubular](https://rubular.com/){:target="_blank"} is handy for quickly testing your regular expressions against some example strings.

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

Within a Rails application[^Rails], you can provide a `Symbol`[^Symbol] as an argument to `Float`'s `to_s` method. This allows you to convert the `Float` to a `String` _and_ add additional formatting at the same time.

[^Rails]:  Or anywhere using `activesupport`.

[^Symbol]: A `Symbol` is a Ruby Class that is similar to a `String`. Symbols start with a colon (`:`) at the beginning. See the chapter section. 

##### Phone 

```ruby
5551234.to_s(:phone) # => "555-1234"
```

In addition to providing a `Symbol` to the `to_s` method, you can provide an _additional_ `Hash`[^Hash] argument to tweak the some finer details about how we want to format the Float.

```ruby
1235551234.to_s(:phone, { :area_code => true }                     # => "(123) 555-1234"
1235551234.to_s(:phone, { :country_code => 1 } )                   # => "+1-123-555-1234"
1235551234.to_s(:phone, { :area_code => true, :extension => 555 }) # => (123) 555-1234 x 555
```

[^Hash]: A `Hash` is another Class is Ruby that. See the Hash chapter. Until you read that chapter, just be aware that this kind of formatting is possible and easy to do in a Rails application.

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