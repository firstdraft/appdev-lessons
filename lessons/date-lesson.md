## Date

Sure, we could just use a `String` to represent a date, like `"April 19, 1987"`. But Ruby has a built-in class that makes it much easier to work with dates: `Date`.

### Creating a date

The `Date` class isn't loaded into every Ruby program by default, so to use it we first need to say

```ruby
require "date"
```

(Usually we omit the parentheses around the string argument to the `require` method. Just like when we use `p "Hello, world!"` as opposed to `p("Hello, World!")`.)

#### Date.new

After `require "date"`, we can create a new instance as usual with:

```ruby
Date.new # => #<Date: -4712-01-01 ((0j,0s,0n),+0s,2299161j)>
```

By default, the new date is January 1st, of the year −4712! Interesting, but not very helpful.

<aside markdown="1">
Year 1 of the [Julian Period](https://en.wikipedia.org/wiki/Julian_day){:target="_blank"} was 4713 BC (−4712).
</aside>

You can also pass `Date.new` arguments to initialize with a specific year, month, and day:

```ruby
Date.new(2001)            #=> #<Date: 2001-01-01 ...>
Date.new(2001,2,3)        #=> #<Date: 2001-02-03 ...>
Date.new(2001,2,-1)       #=> #<Date: 2001-02-28 ...>
```

### Date Methods

#### Date.today 

The `Date.today` method returns an object initialized to the current date.

```ruby
Date.today # => #<Date: 2019-04-16 ((2458590j,0s,0n),+0s,2299161j)>
```

#### year 

Call the `year` method on a `Date` object to return just the year of the date as an `Integer`.

```ruby
t = Date.today # => #<Date: 2019-04-16 ((2458590j,0s,0n),+0s,2299161j)>
t.year # => 2019
```

----

#### Quiz Question

- What would you type after `t` above to convert the variable to a string?
- .to_s
    - Yes! That's the method we need.
{: .free_text #to_string points="10" answer="1" }

----

#### month 

Call the `month` method on a `Date` object to return just the month of the date as an `Integer`.

```ruby
t = Date.today # => #<Date: 2019-04-16 ((2458590j,0s,0n),+0s,2299161j)>
t.month # => 4
```

#### day 

Call the `day` method on a `Date` object to return just the day of the date as an `Integer`.

```ruby
t = Date.today # => #<Date: 2019-04-16 ((2458590j,0s,0n),+0s,2299161j)>
t.day # => 16
```

<div class="proj" markdown="1">

  Open the Gitpod [`Date` project](https://github.com/appdev-projects/ruby-project-date-1){:target="_blank"} on Canvas that follows this reading and start with the exercise `formatted.rb`.

  For a Gitpod refresher, see [this section](https://learn.firstdraft.com/lessons/9#start-the-gitpod-project){:target="_blank"} in `String` , where we opened our first workspace.
</div>

#### Date.parse 

The `Date.parse()` method accepts a `String` argument and tries to interpret it as a date, initializing a `Date` object.

```ruby
Date.parse("2001-02-03") #=> #<Date: 2001-02-03 ...>
Date.parse("20010203") #=> #<Date: 2001-02-03 ...>
Date.parse("3rd Feb 2001") #=> #<Date: 2001-02-03 ...>
```

It's pretty smart!

#### Subtraction 

You can subtract two dates from one another, which will return the number of days between them. The return value class is a `Rational`, which can be converted to a regular `Integer` with `.to_i`:

```ruby
number_of_days = Date.today - Date.parse("July 4, 1776")
 => (88674/1)
days.to_i
 => 88674
```

<div class="proj" markdown="1">
  
  Return to the Gitpod `Date` project and work through `math.rb`
</div>

#### monday? 

Returns `true` if the date is a Monday.

#### tuesday? 

Returns `true` if the date is a Tuesday.

#### wednesday? 

Returns `true` if the date is a Wednesday.

#### thursday? 

Returns `true` if the date is a Thursday.

#### friday? 

Returns `true` if the date is a Friday.

#### saturday? 

Returns `true` if the date is a Saturday.

#### sunday? 

Returns `true` if the date is a Sunday.

#### wday 

Returns the day of week (0-6, Sunday is zero).

```ruby
Date.new(2001,2,3).wday #=> 6
```

<div class="proj" markdown="1">
  
  Return to the Gitpod `Date` project and work through `monday.rb`
</div>

### Time

Ruby has a `Time` class as well, that shares most of its methods with the `Date` class.

```ruby
Time.now.wday # => 6
Time.now.saturday? # => true
Time.now.day # => 3
```

#### strftime 

The `strftime` method is used on a `Date` or `Time` object. It requires a `String` argument that will be used to format the Date or Time in a particular way.

_Assuming today is Monday, September 7th 2020_

```ruby
Time.now.strftime("%A") # => "Monday"
Time.now.strftime("%B") # => "September"
Time.now.strftime("%b") # => "Sep"
Time.now.strftime("%a %e, %R %p") # => "Mon, 7 14:35 PM"
```

You should **not** try to memorize what these patterns mean. Tools like [strftime.net](http://www.strftime.net){:target="_blank"} and [For a Good Strftime](https://www.foragoodstrftime.com/){:target="_blank"} exist to help compose the formatting string argument.

**BENP: new strftime exercise**

###  Conclusion

That's it for `Date` and `Time`. Next up, we'll learn how we can make lists of data with the `Array` class.

<span style="font-size: large">**Return to Canvas and head to the next part of the lesson**</span>

----