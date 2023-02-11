## Addendum: Some more Ruby methods

Here are some more Ruby methods that we didn't cover in the chapters, but which will likely come in handy in some of the Ruby Gym exercises. Of course, many of these are also collected in [the long Ruby reference][The One Ruby Reference].

### String 

#### reverse {-}

The reverse method returns a new `String` with the characters from the `String` in reverse order.

```ruby
p "I can speak in backwords words".reverse
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/reverse){target="_blank"}
</div>

#### length {-}

The length method  returns the number of characters (as an `Integer`) that a `String` has.

```ruby
p "Supercalifragilisticexpialidocious".length
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/length){target="_blank"}
</div>

#### Advanced gsub techniques {-}

`gsub` also supports accepting a _regular expression_ as its first argument. We won't get into regular expressions in detail right now, but all languages (C, C++, Python, etc.) include a way to write regular expressions and they are a very powerful way to check whether input strings match certain patterns.

In Ruby, we work with regular expressions the way we work with everything else — via a class, `Regexp`. We create `Regexp` _literals_ with forward slashes (like we use quotes to create `String` literals), and then put the pattern that we're trying to match between the slashes.

For now, we're just going to copy-paste a few simple regexes[^regexone] that come in handy with `gsub`, in particular:

[^regexone]: If your project requires scanning text for patterns, then [RegexOne](https://regexone.com/){target="_blank"} is a good resource for learning more. [Rubular](https://rubular.com/){target="_blank"} is handy for quickly testing your regular expressions against some example strings.

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