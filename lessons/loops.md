## Loops in Ruby

- Notes:

  - Copied from [`loops.md`](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/loops.md){target="_blank"}
  - See [Ruby Practice: Loops][Ruby Practice: Loops] for project: [https://github.com/appdev-projects/loops-chapter](https://github.com/appdev-projects/loops-chapter){target="_blank"}

### if: conditionally doing something once

Consider the following program, which utilizes an `if` statement:

```ruby
numbers = Array.new

if numbers.length < 10
  new_number = rand(100)
  numbers.push(new_number)
end

len = numbers.length

p numbers
p len
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/loops-conditionally-doing-something-once){target="_blank"}

What do you expect the output of the program to be when you click run? Try to interpret the program yourself before you ask Ruby to.

Okay, now you can click "run ▶". Did you guess right?

We start off with a blank array, `numbers`. If its length is less than `10` (this is true, since length is currently `0`), we push a new random number into it.

Once Ruby reaches the `if`'s `end`, it proceeds to the next line and continues to execute the rest of the code (whether the `if`'s condition was true or not).

At the end of the day, `numbers` has one element in it and `len` is `1`.

### while: conditionally doing something multiple times

Now, consider almost identical code, but with the `if` keyword swapped for a new keyword — `while`:

```ruby
numbers = Array.new

while numbers.length < 10
  new_number = rand(100)
  numbers.push(new_number)
end

len = numbers.length

p numbers
p len
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/loops-conditionally-doing-something-multiple-times){target="_blank"}

`while` works almost exactly like `if` — it evaluates the expression next to it, and if the expression is truthy, it executes the code on the lines between it and it's `end`; if not, it ignores the code on the lines between it and it's `end`.

There is one key difference: if the condition next to a `while` is truthy, after we reach it's `end`, the execution of the program **jumps back up to the `while` statement**.

Then the condition is evaluated *again*. **If it is *still* true, then the code inside the `while` statement is executed _again_.** And then the execution of the program jumps back up to the `while` statement *again*. Etc.

So in this case,

 - The first time we reach the `end`, we jump back up to the `while`.
 - Evaluate `a.length < 10` again — still true, since `1 < 10`.
 - So we push in another random number, and jump back up.
 - `2 < 10`? Yep, so we do it again.
 - We push in another random number, and jump back up.
 - `3 < 10`? Yep, so we do it again.
 - `4 < 10`? Yep, so we do it again.
 - Etc.
 - `10 < 10`? Nope, so now proceed to the line after the `end` and continue.
 - And `len` ends up being `10`.

What we've seen here is our very first **loop**; code that is executed multiple times. It could be an arbitrary number of times, perhaps even an infinite number of times if we aren't careful.

### Blocks

Fundamentally, all looping is implemented with `while`; but, this being Ruby, there are all sorts of convenience methods on top to make it as easy as possible to create loops for various contexts. For example, let's say I wanted to print:

```
"1 Mississippi"
"2 Mississippi"
"3 Mississippi"
# etc
"10 Mississippi"
```

exactly 10 times. I could do it using `while` like this; try interpreting the following code before you click "run":

```ruby
mississipis = 1

while mississipis <= 10
  p mississipis.to_s + " Mississippi"

  mississipis = mississipis + 1
end
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/loops-mississippis-with-while){target="_blank"}

Does the code make sense to you?[^incrementing]

[^incrementing]: If the line `mississipis = missippis + 1` looks a little odd to you, you're not alone. [Remember, this is _variable assignment_](https://chapters.firstdraft.com/chapters/754#updating-variables){target="_blank"}, not equivalence. So the expression on the right side (`mississipis + 1`) is evaluated _first_ until there's just one object (e.g `2`) left; and then that object replaces the contents of the variable (`mississipis`) named on the left. Rinse and repeat.

Or, rather than `while`, I could use `Integer`'s `.times` method, like this:

```ruby
mississipis = 1

10.times do
  p mississipis.to_s + " Mississippi"

  mississipis = mississipis + 1
end
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/loops-mississippis-with-times){target="_blank"}

Notice there's a new keyword here: `do`. This is because the `.times` method, in order to do its job of executing some code 10 times, needs a special argument — _the code to execute_.

In order to pass a method _some lines of code_ as an argument, we need to wrap the lines of code within the `do` and `end` keywords, creating what's called a **block** of code.

So, given a **block** of code, the `10.times` method will execute it for us exactly 10 times; this saves us the trouble of writing a condition for `while`.

#### Block variables

But the `.times` method will save us even more trouble than that; we can stop worrying about creating and incrementing the counter variable, `mississipis`, too. The `.times` method will create a **block variable** and assign values to it for us automatically, but we have to choose a name for it using some new syntax after the `do`: the vertical bars, `| |`, or "pipes". It looks like this:

```ruby
10.times do |mississipis|
  p mississipis.to_s + " Mississippi"
end
```

[Click here for a REPL to try it.](https://repl.it/@raghubetina/loops-first-block-variable){target="_blank"}

Try running it. Here's what's going on:

 - We created a block of code with `do`/`end` and gave it to `.times`.
 - We chose a name for a **block variable**, `mississipis`, with the `| |` after the `do`.
 - Behind the scenes, the `.times` method did `mississipis = 0` before the first iteration.
 - The `.times` method executed the block of code the first time.
 - Behind the scenes, the `.times` method did `mississipis = 1` before the second iteration.
 - The `.times` method executed the block of code the second time.
 - Etc.

Why does `.times` start by assigning `0` to its block variable during the first iteration, rather than `1`? Well, that's just how the author of the `.times` method made it work.

**BENP: isn't the reason for starting at 0 because of 0-indexing? If so, this is a good place to reiterate that.**

Fortunately, Ruby provides lots of other looping convenience methods that we can take advantage of instead, and each one assigns different values to its block variable.

In the REPL above, replace `10.times` with each of the following and play around with the arguments to get a sense of how each method works:

```ruby
5.upto(10)
99.downto(90)
1.step(10, 3)
10.step(1, -4)
```

## Ruby Practice: Loops

- Notes:

  - Copied from project README: [https://github.com/appdev-projects/loops-chapter](https://github.com/appdev-projects/loops-chapter){target="_blank"}

Run your Ruby file by typing `ruby ` and then the name of the file you want to run in the Terminal.

If we want to run `loops_multiples.rb`, we can write the command:

```bash
ruby loops_multiples.rb
```

To re-run this command, you can use the UP and DOWN arrow keys to look at the history of commands you've run in a Terminal.

### loops_letter_count.rb
Write a program that:

Asks the user to input a word and counts from 1 to however long the word is.

Example (`apple` is the input):
```bash
"Enter a word:"
apple
1
2
3
4
5
"apple is 5 letters long!"
```

### loops_multiples.rb
Write a program that:

Asks the user to input a number. The program should print multiplication table of entered number from 1 to 10.

Example (`2` is the input):
```bash
"Enter a number:"
2
2
4
6
8
10
12
14
16
18
20
```

### loops_fizzbuzz.rb
Write a program that prints the numbers from 1 to 100, except

for multiples of three print “Fizz” instead of the number
for multiples of five print “Buzz” instead of the number
for numbers which are multiples of both three and five print “FizzBuzz”

Your output should look something like
```bash
1
2
"Fizz"
4
"Buzz"
"Fizz"
7
8
"Fizz"
"Buzz"
11
"Fizz"
13
14
"FizzBuzz"
16
# etc
```
Hint: if x is a multiple of y, that means that we can divide x by y and have nothing leftover. Do we have anything in our Ruby toolbox that can help find remainders? Look through your older readings.