## If statements

- Notes:

  - Copied from [`conditionals.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/conditionals.md){target="_blank"}
  - See [Ruby Practice: Conditionals][Ruby Practice: Conditionals] for project: [https://github.com/appdev-projects/if-statements-chapter](https://github.com/appdev-projects/if-statements-chapter){target="_blank"}

Now that we can get input from our users, we can start to make our programs
smart, by behaving differently based on different conditions.

To do this, we need to add a new grammar to our toolbox: the `if`/`end` **keywords**. Here's how it looks:

```ruby
lucky_number = rand(100)

p "Your lucky number is " + lucky_number.to_s + "."

if lucky_number.odd?
  p "The number is odd."
end
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/first-conditional){target="_blank"}

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

[Click here for a REPL to try it.](https://repl.it/@raghubetina/multibranch-if){target="_blank"}

 - Note that there is **no space** in the `elsif` keyword, and that there is **no `e` in the middle** of the `elsif` keyword. (In other languages, this construct is `elseif`, `else if`, etc; but in Ruby it's just `elsif`.)
 - The conditions are checked in top-down priority, so even if more than one is true, whichever one is first has its branch executed; the rest are ignored.
 - If none are true, the final `else` fallback branch is executed; but you don't have to have one if you don't want one.
 - Inside a branch of an `if` statement, you can have as many lines of code as you want — and you can even have whole other multi-branch if statements, if that's what you need.
 - Try to indent the code within each branch by two spaces, especially if you have multiple nested `if` statements within one another.

### truthiness and falsiness

Why did I say "truthy" and "falsy" instead of just `true` and `false`? Because many — most — Ruby expressions return values other than `true` or `false`. _Any_ expression can appear next to an `if`, and some will cause the code inside the `if` statement to execute (these values are known as "truthy") and some will not (these are "falsy").

In the REPL below, try replacing `1 == 1` with each of the following. Before clicking "run" for each one, ask yourself, do you expect to see the output `"The expression is truthy."` or not?

 - `0`
 - `"false"`
 - `[]`
 - `nil`
 - `true`
 - `""`
 - `false`

```ruby
if 1 == 1 # Replace this with each expression. Which of them count as "truthy"?
  p "The expression is truthy."
else
  p "The expression is falsy."
end
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/truthiness){target="_blank"}

For how many of the above did you correctly predict the output? What did you learn about what objects count as truthy and what objects count as falsy in Ruby?

---

<p style="height: 500px"></p>

--- 

It turns out that **only `false` and `nil` are falsy**. _All_ other objects in Ruby are truthy — even `0`, `""`, and `[]`.

### Comparisons

That said, we'll mostly use expressions after `if` that return `true` or `false`. There are lot of methods that are designed to do this; we've seen `Integer`'s `.odd?` and `.even?`, but there are a lot more.

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
"apple" < "banana"
"apple" > "banana"
"apple" == "banana"
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

[Click here for a REPL to try it.](https://repl.it/@raghubetina/and-and-or){target="_blank"}

Basically, `&&` is stricter than `||`; both comparisons have to be true in order for the whole statement to be true when combined with `&&`; either one being true is sufficient for `||`.

### Challenge

Can you create a Rock, Paper, Scissors game?

[Click here for a REPL to try it.](https://repl.it/@raghubetina/rps-2){target="_blank"}

## Ruby Practice: Conditionals

- Notes:

  - Copied from project README: [https://github.com/appdev-projects/if-statements-chapter](https://github.com/appdev-projects/if-statements-chapter){target="_blank"}

Run your Ruby file by typing `ruby ` and then the name of the file you want to run in the Terminal.

If we want to run `conditionals_rps.rb`, we can write the command:

```bash
ruby conditionals_rps.rb
```

To re-run this command, you can use the UP and DOWN arrow keys to look at the history of commands you've run in a Terminal.

### conditionals_rps.rb

Write a program that:

Asks the player to input rock, paper, or scissors.
Based on what the player chose, prints "You played rock!" or "You played paper!" or "You played scissors!"
The computer is pretty dumb in this version of our game; it always plays scissors. Print "The computer played scissors!"
Based on what the player chose, prints "You won!" or "You lost!" or "You tied!"
If you need a refresher on the rules of Rock, Paper, Scissors: https://en.wikipedia.org/wiki/Rock%E2%80%93paper%E2%80%93scissors


### conditionals_palindrome.rb

Ask for a word, check if it is a palindrome, and display true if it is one and false if it isn't.

A word is a palindrome if it reads the same backwards as forwards, e.g. "madam".

Remember to display the actual value true or false, not the strings containing the letters "true" or "false".

Input:
`hannah`

Key output:
`true`

Complete input and output example:
```bash
"Enter one word"
hannah
true
```
