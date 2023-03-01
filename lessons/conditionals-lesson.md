## If statements

Now that we can get input from our users, we can start to make our programs smart, by behaving differently based on different conditions.

----

#### Quiz Question

- Hold up. How do we get input from our users? Choose all that apply.
- The user opens a Gitpod workspace
    - No, the user only needs access to a command line for the programs we wrote so far
- We put the method `gets` in our code
    - Yes! When the Ruby interpreter reaches that method, it will stop the program and wait for input.
- We store the result of the method `gets` in a new variable
    - That's right! `gets` stands for "get string"
- We `chomp` any newline `\n` character off the user input
    - That's right! `gets.chomp` will remove the `\n` caused when the user presses <kdb>return</kbd>
- The user opens an `.rb` file and puts in their response
    - No, they don't touch our source code
- If we wanted a few things, we might `split` the input
    - Yes! `gets.chomp.split` with no arguments will just split on whitespace. `split("")` would cut every character apart.
{: .choose_all #user_gets points="10" answer="[2,3,4,6]" }

----

To add conditions based on user input, we need to add a new grammar to our toolbox: the `if`/`end` **keywords**. Here's how it looks:

```ruby
lucky_number = rand(100)

p "Your lucky number is " + lucky_number.to_s + "."

if lucky_number.odd?
  p "The number is odd."
end
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/first-conditional){:target="_blank"}
</div>

Try running this program a few times and see how it behaves. These expressions, which conditonally run some code based on the truth or falseness of some condition, are known as **conditionals** or **if statements**.

### The basic anatomy of if statements

The anatomy of an `if` statement is:

```ruby
if condition
  # code that runs if the condition is true
end
```

 1. First comes the `if` keyword.
 1. After the `if`, on the same line, comes any Ruby expression, which is evaluated until only one piece of data is left.
 1. If that final return value of `condition` is "truthy", then the code on the lines between the `if` and `end` keywords is executed.
 1. If the final return value of `condition` is "falsy", then the code on the lines between the `if` and `end` keywords is ignored.
 1. Either way, the program picks up execution on the next line after the `end` keyword and continues on.

#### Don't forget the end 

Every `if` requires a matching `end`, and forgetting it is a _very_ common mistake.

My advice: type the `end` _immediately_ after typing the `if` so that you don't forget it; _then_ worry about typing the condition, and the code that comes on the lines between the `if` and the `end`.

(While you're at it, indent the code on the lines between by two spaces so that it is visually clear what's inside the `if` statement.)

<div class="proj" markdown="1">

  Open the Gitpod [`if` statements project](https://github.com/appdev-projects/ruby-project-if-statements-1){:target="_blank"} on Canvas that follows this reading and start with the exercise `if_sample_even.rb`.

  For a Gitpod refresher, see [this section](https://learn.firstdraft.com/lessons/9#start-the-gitpod-project){:target="_blank"} in `String`, where we opened our first workspace.
</div>

### Multibranch if statements

We can also have **multibranch** `if` statements, where we specify fallback conditions to check and code to execute if the first condition is falsy:

```ruby
the_temp = rand(100)

p the_temp

if the_temp > 75
  p "It's going to be a great day today"
else
  p "Don't leave home today"
end
```

Or you can have multiple conditions that get checked, one after the other:

```ruby
the_temp = rand(100)

p the_temp

if the_temp > 75
  p "It's going to be a great day today"
elsif the_temp > 32
  p "It'll be an okay day today"
else
  p "Don't leave home today"
end
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/multibranch-if){:target="_blank"}
</div>

 - Note that there is **no space** in the `elsif` keyword, and that there is **no `e` in the middle** of the `elsif` keyword. (In other languages, this construct is `elseif`, `else if`, etc; but in Ruby it's just `elsif`.)
 - The conditions are checked in top-down priority, so even if more than one is true, whichever one is first has its branch executed; the rest are ignored.
 - If none are true, the final `else` fallback branch is executed; but you don't have to have one if you don't want one.
 - Inside a branch of an `if` statement, you can have as many lines of code as you want — and you can even have whole other multi-branch if statements, if that's what you need.
 - Try to indent the code within each branch by two spaces, especially if you have multiple nested `if` statements within one another.

----

#### Quiz Question

```ruby
n = 15

if n < 15
  s = "first part"
elsif n > 20
  s = "second part"
elsif n < 18
  s = "third part"
else
  s = "fourth part"
end

p "It picked the " + s
```

- In the above code, what would the full printed out statement be?
- It picked the third part
    - Yes!
{: .free_text #multibranch points="10" answer="1" }

----

### truthiness and falsiness

Why did I say "truthy" and "falsy" instead of just `true` and `false`? Because many — most — Ruby expressions return values other than `true` or `false`. _Any_ expression can appear next to an `if`, and some will cause the code inside the `if` statement to execute (these values are known as "truthy") and some will not (these are "falsy").

In the REPL below, try replacing `true` with each of the following. Before clicking "run" for each one, ask yourself, do you expect to see the output `"The expression is truthy."` or not?

 - `0`
 - `"false"`
 - `[]`
 - `nil`
 - `1 == 1`
 - `""`
 - `false`

```ruby
if true # Replace this with each expression. Which of them count as "truthy"?
  p "The expression is truthy."
else
  p "The expression is falsy."
end
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/truthiness){:target="_blank"}
</div>

For how many of the above did you correctly predict the output? What did you learn about what objects count as truthy and what objects count as falsy in Ruby?

----

#### Quiz Question

- Which of the expressions is "falsy"? Choose all that apply.
 - `0`
    - Nope.
 - `"false"`
    - Nope.
 - `[]`
    - Nope.
 - `nil`
    - Yes!
 - `1 == 1`
    - Nope.
 - `""`
    - Nope
 - `false`
    - Yes!
{: .choose_all #falsy points="10" answer="[4,7]" }

----

<p style="height: 200px"></p>

----

### Comparisons

It turns out that **only `false` and `nil` are falsy**. _All_ other objects in Ruby are truthy — even `0`, `""`, and `[]`.

That said, we'll mostly use expressions after `if` that return `true` or `false`. There are a lot of methods that are designed to do this; we've seen `Integer`'s `.odd?` and `.even?`, but there are a lot more.

For example, most classes have ways to compare _instances_ of the class to one another:

```ruby
1 < 2          # "1 is less than 2"
2 < 1          # "2 is less than 1"
24*365 > 10000 # There are more than 10,000 hours in a year
1 == 1         # "1 is equivalent to 1"
1 == 2         # "1 is equivalent to 2"
1 <= 2         # "1 is less than or equal to 2"
1 >= 2         # "1 is greater than or equal to 2"
1 != 1         # "1 is NOT equivalent to 1"
1 != 2         # "1 is NOT equivalent to 2"
"apple" == "apple"
"apple" != "banana"
```

#### Equivalence vs assignment 

Note the difference between the **equivalence operator** — two equals signs, `==` — and the variable assignment operator — one equals sign, `=`. Mixing up the two of them is probably _the_ most common typo programmers make:

```ruby
x = 2

if x = 3
  p "x is 3"
else
  p "x is not 3"
end
```

If you run the code above, what would be printed? Why?

We accidentally used the assignment operator instead of the equivalence comparison, and in doing so, we _set_ `x = 3` when we meant to check `if x == 3`.

You will 💯 make this typo, we all do at some point — when your conditional always is going into the `true` branch inexplicably, let this ring a bell!

----

#### Quiz Question

- The equivalence operator is (and does)...
- `=`, and it checks if two things are the same
    - No, that's the variable assignment operator, and it assigns objects into variables
- `=`, and it assigns objects into variables
    - No, that's the variable assignment operator.
- `==`, and it assigns objects into variables
    - Not quite, look above at the previous section.
- `==`, and it checks if two things are the same
    - Yes! `==` is not the same as `=`
{: .choose_best #equivalence points="10" answer="4" }

----

#### Quiz Question

```ruby
n = "giraffe"

if n != "giraffe"
  s = "first part"
elsif n == "Giraffe"
  s = "second part"
else
  s = "third part"
end

p "It picked the " + s
```

**Think carefully,** after each `if` or `elsif` ask yourself: is this expression resulting in a `true` or a `false`?

- In the above code, what would the full printed out statement be?
- It picked the third part
    - Yes!
{: .free_text #multibranch_conditional points="10" answer="1" }

----

#### Quiz Question

- In the above code, what `String` method could you use to modify `n` and have it print `It picked the second part`? (Hint: have a look at [the `String` lesson](https://learn.firstdraft.com/lessons/9){:target="_blank"}.)
- capitalize
    - Yes! 
- n = n.capitalize
    - Yes!
- n.capitalize
    - Yes!
{: .free_text #multibranch_conditional_v2 points="10" answer="[1,2,3]" }

----

<div class="proj" markdown="1">

  Return to the Gitpod `if` statements project and work through `rps.rb`.
</div>

<div class="proj" markdown="1">

  Also, work through `palindrome.rb`.

  (Hint: you will need a couple of methods from the [`String` lesson](https://learn.firstdraft.com/lessons/9){:target="_blank"}. What methods there can be used to make inputs a uniform case?)
</div>

### Combining conditions with AND and OR

Finally, another handy thing to have in your toolbelt are the **logical operators** `&&` (AND) and `||` (OR). These allow you to combine expressions; try these combined expressions out below:

```ruby
3.odd? && 4.even?
3.odd? && 4.odd?
3.even? && 4.odd?
3.odd? || 4.even?
3.odd? || 4.odd?
3.even? || 4.odd?
```

When used with `if` statements, this ability is very powerful:

```ruby
if 3.odd? && 4.even?
  p "The combined expression is truthy."
end
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/and-and-or){:target="_blank"}
</div>

Basically, `&&` is stricter than `||`; both comparisons have to be true in order for the whole statement to be true when combined with `&&`; either one being true is sufficient for `||`.

<div class="proj" markdown="1">

  Return to the Gitpod `if` statements project and work through `and_or.rb`.
</div>

###  Conclusion

That's it for `if` statements. Now we'll have a look at **loops** for iterating.

<span style="font-size: large">**Return to Canvas and head to the next part of the lesson**</span>

----