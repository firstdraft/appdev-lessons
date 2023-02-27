## String

Let's start by getting a more formal introduction to our friend, `String`.

First of all, notice that when I refer to Ruby classes, I capitalize the first letter. The _only_ time we use capital letters when we're programming is when we refer to Ruby classes. All other times — variable names, file names, etc — we're going to use lowercase letters only (other than when we're writing some copy inside a string, of course).

### Creating strings

We've actually been taking a shortcut this whole time when we've been saying something like

```ruby
s = "Hello, world!"
```

In Ruby, the formal way to create a new object is to use the `.new` method on the parent class:

```ruby
s = String.new
```

This will, however, just give us back an empty string `""`.

#### Make the invisible visible in Gitpod 

In the technical setup, we saw [how we can start a workspace with Gitpod](https://learn.firstdraft.com/lessons/28#getting-started-with-gitpod){:target="_blank"}. Let's refresh here and actually make use of a Gitpod workspace to write some code in.

<div class="experiment" markdown="1">

   Let's practice **making the invisible visible**. We will spend a moment getting a Gitpod workspace set up, and then running Ruby programs from the terminal there. The steps are:

   1. If you didn't already, sign up for a [Gitpod.io](https://www.gitpod.io){:target="_blank"} account. It will ask you to sign in using your GitHub account.

   1. We will create a **workspace** for each project that we work on. Each workspace is based on a GitHub **repository** or **repo** (i.e., a folder with some code in it). For example, here is a repository:
   
         [https://github.com/appdev-projects/helloruby](https://github.com/appdev-projects/helloruby){:target="_blank"}

   1. To create a Gitpod workspace based on a repo, in the address bar of your browser enter **https\://gitpod.io/#** and then the URL of the repo. For example,

         **https\://gitpod.io/#https\://github.com/appdev-projects/helloruby**

   1. This creates a blank, brand-new computer. This is not a REPL, nor is it an HTML application like we made for Rock, Paper, Scissors. But Ruby _is_ installed on this computer. 
   
   1. We can create a Ruby file by right-clicking in the file explorer and selecting "New File". We can call our file `howdy.rb`, making sure to end it with the extension `.rb`.

   1. With `howdy.rb` open in the editor window, we can add some code like `p "Hello, world!"`, and save the file (or turn on "Auto Save").

   1. Now we can run the file by clicking on the terminal and typing (after the `$`-sign): `ruby howdy.rb`. When we press <kbd>return</kbd> on our keyboard, the code in `howdy.rb` will execute and show us the result!

   To get more comfortable with these steps, create another file called `invisible_to_visible.rb`, and fill it with this code:

```ruby
# One-by-one, uncomment the p statements 
# below and rerun the code
s = String.new
# p s 
s = "Hello, world!"
# p s
s = s.upcase
# p s
```

   Once the file is saved, remove the leading `#` from the `p`rint statements one by one, and run the code each time with `ruby invisible_to_visible.rb` at the terminal prompt. You don't need to type it out every time, you can just press the <kbd>Up ↑</kbd> arrow key when your cursor is at the terminal `$`-sign prompt to cycle to the previous entry.

</div>

When you are done experimenting, and you've answered the quiz question below, feel free to close the Gitpod project window. We will open another project momentarily and only one Gitpod tab will limit confusion.

----

#### Quiz Question

- In the `invisible_to_visible.rb` code that you wrote above, which of the following is true?
- The variable `s` contained *both* `"Hello, world!"` and `"HELLO, WORLD!"` in the end
    - Really? Did you try it?
- We completely overwrote the original `"Hello, world!"` content of `s`
    - Yes! Remember we can have `s` on both sides of a variable assignment operator
- We overwrote the variable `s` with new content, but we should never do that in real Ruby code in our apps
    - Nope. This is a very common step and you should get used to seeing it.
- None of the above
    - Not quite, experiment with the code a bit more.
{: .choose_best #invis_to_vis points="10" answer="2" }

----


#### ASCII Codes 

With the `String.new` approach, we would have to add each character to our variable `s` one by one. One way to do so is by using the `.concat` method, which accepts a number as an argument, interprets it as an ASCII code, translates it into a single character, and adds it on to the end of the original string.

What's an ASCII code? At the hardware level, computers only store integers (specifically, in _binary_ form — using only `0`s and `1`s); so all other datatypes need to be encoded somehow as a number. [ASCII](https://en.wikipedia.org/wiki/ASCII){:target="_blank"}, or American Standard Code for Information Interchange, was one scheme that was developed in the early days of computing to store English characters as integers. The codes are as follows:

<aside markdown="1">
Nowadays we use much more sophisticated encoding schemes such as [Unicode](https://en.wikipedia.org/wiki/Unicode){:target="_blank"} that supports glyphs from many more languages, and even emojis 🙌🏾 Fortunately, Ruby handles most of this low-level stuff for us behind the scenes, so we never really have to worry about it anymore.
</aside>


**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**|**ASCII Code**|**Character**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
32|(space)|48|`0`|64|`@`|80|`P`|96|<code>`</code>|112|`p`
33|`!`|49|`1`|65|`A`|81|`Q`|97|`a`|113|`q`
34|`"`|50|`2`|66|`B`|82|`R`|98|`b`|114|`r`
35|`#`|51|`3`|67|`C`|83|`S`|99|`c`|115|`s`
36|`$`|52|`4`|68|`D`|84|`T`|100|`d`|116|`t`
37|`%`|53|`5`|69|`E`|85|`U`|101|`e`|117|`u`
38|`&`|54|`6`|70|`F`|86|`V`|102|`f`|118|`v`
39|`'`|55|`7`|71|`G`|87|`W`|103|`g`|119|`w`
40|`(`|56|`8`|72|`H`|88|`X`|104|`h`|120|`x`
41|`)`|57|`9`|73|`I`|89|`Y`|105|`i`|121|`y`
42|`*`|58|`:`|74|`J`|90|`Z`|106|`j`|122|`z`
43|`+`|59|`;`|75|`K`|91|`[`|107|`k`|123|`{`
44|`,`|60|`<`|76|`L`|92|`\`|108|`l`|124|`|`
45|`-`|61|`=`|77|`M`|93|`]`|109|`m`|125|`}`
46|`.`|62|`>`|78|`N`|94|`^`|110|`n`|126|`~`
47|`/`|63|`?`|79|`O`|95|`_`|111|`o`|
{: .bleed-full }

Given those ASCII codes, we can now build up a new string from scratch like so:

```ruby
# instantiate a new variable of String class
my_string = String.new

# make the invisible visible!
p my_string # => ""

# use the concat method to add characters
# one-by-one to the empty string variable
my_string.concat(72)
my_string.concat(101)
my_string.concat(108)
my_string.concat(108)
my_string.concat(111)
my_string.concat(44)

# make the invisible visible!
p my_string # => "Hello,"

# add some more characters again
my_string.concat(32)
my_string.concat(119)
my_string.concat(111)
my_string.concat(114)
my_string.concat(108)
my_string.concat(100)
my_string.concat(33)

# make the invisible visible!
p my_string # => "Hello, world!"
```

<div class="experiment" markdown="1">
   This is just a quick sandbox, so [click here for a REPL to try it.](https://repl.it/@raghubetina/creating-objects-with-new){:target="_blank"}
</div>

----

#### Quiz Question

- The ASCII code for the "pipe" symbol `|` is...
- 124
    - Yes! 
{: .free_text #ascii points="10" answer="1" }

----

#### Start the Gitpod Project

Once you've played with the REPL, it's time to move into the graded project environment.

In our [previous steps](#make-the-invisible-visible-in-gitpod), we opened a Gitpod workspace via **https\://gitpod.io/#[SOME REPO]**. But, for most projects, you will be "forking" an existing GitHub repo to your account, then opening it on Gitpod, so that you can save changes and keep your own copy around for future reference. We prepared these steps, so you just need to click on the **Load assignment** button on Canvas, as described below.

If you need a full refresher on working with Gitpod, see the [technical setup instructions](https://learn.firstdraft.com/lessons/29){:target="_blank"}.

<div class="proj" markdown="1">

   **Note: these steps go for opening any Gitpod project for the Ruby lessons, just change the project and file names.**

   Open the Gitpod `String` project on Canvas that follows this reading and start with the exercises. Follow the instructions below and complete the task in the `concat.rb` file.

   <!-- 1. LTI{Load assignment}(https://github.com/appdev-projects/ruby-project-string-1)[MV4dKHMwdAFhfRn752YW3TAY]{KBpPhe42o6wDRi35rWagKY4F}(100)[string_project] -->

   1. On Canvas, open the project assignment that follows this reading. Click on the "Load in new window" button, then click on the green button to "Create new workspace on Gitpod", which will open a new project for you to work on! **Keep this Gitpod tab open, there may be more than one exercise per chapter**. If you close the Gitpod window, you can always click the Canvas link again, but this time click "Find existing workspace in Gitpod Dashboard".

   <!-- ![](assets/string/canvas-gitpod-start-project.png) -->

   1. Open the `concat.rb` file in the editor window.

   1. Modify the file per the instructions on top.

   1. Run your Ruby file by typing `ruby ` and then the name of the file you want to run in the terminal. If we want to run `concat.rb`, we can write the command:

         ```bash
         ruby concat.rb
         ```
      
         Remember, if there are multiple files with similar names, start typing the name and then just press <kbd>Tab</kbd> on your keyboard to let the terminal complete the name. You rarely need to type full filenames out — use **tab completion**!

   1. To re-run this command, you can use the <kbd>Up ↑</kbd> and <kbd>Down ↓</kbd> arrow keys to look at the history of commands you've run in a terminal.

   1. When you think you have the required output, [run `rails grade`](https://learn.firstdraft.com/lessons/29#getting-automated-feedback-with-rails-grade){:target="_blank"} at the terminal prompt and proceed when the test(s) passes without errors.

   1. If you want to save your work on Github (because Gitpod will delete the workspace), from the terminal you need to start the app browser with `bin/server` and then navigate to the **/git** URL path to bring up the commit and push interface, [as we usually do](https://learn.firstdraft.com/lessons/30#using-git-in-your-projects){:target="_blank"}.

   If you are struggling, **try to experiment directly in the `irb` environment** by typing `irb` into the terminal and pressing enter. This will start an interactive Ruby terminal, where you can enter individual lines of Ruby to see their output. If you start `irb` then the terminal will no longer be in the `bash` environment so things like `rails grade` won't work. You will need to open a second terminal with the plus (+) icon and switch between the `irb` and `bash` terminals as needed. Alternatively type `exit` at the `irb` terminal prompt to return to the `bash` environment. If you ever want to clear the terminal output to see a fresh new line, press <kbd>Ctrl</kbd>+<kbd>K</kbd>. And if you ever close the terminal and need to re-open it, press <kbd>Ctrl</kbd>+<kbd>J</kbd>.

</div>

#### String literals 

Done with `concat.rb`? What a pain! Now that we've shown that, under the hood, even creating a string follows the syntax of `noun.verb` — let's never do it again. From now on, we'll use the shortcut of creating string "**literals**" in place by typing the characters we want within quotes: `"Thank goodness!"`

These kinds of exceptions to the regular grammar in order to make life easier are known as "**syntactic sugar**".

### Methods

Next, let's familiarize ourselves with some of the `String` class's methods. For each method below, there is a an `.rb` exercise in the Gitpod project. So keep that project window open and work through it with `rails grade` as you go!

For each method below, we've also provided some REPLs. They are there for you to experiment with the code, click "▶ Run", or use the `irb` terminal and see how the methods work. Keep these methods in mind when working on the assignments in Gitpod.

#### String addition, a.k.a. + 

We've already met the `.concat` method. `.concat` can accept an integer as an argument, which it interprets as an ASCII code, translates into a single character, and adds to the original string:

```ruby
"hi".concat(33) # => "hi!"
```

`.concat` can also accept a string literal as an argument, in which case it just adds the whole thing to the end of the original string.

```ruby
"hi".concat(" there") # => "hi there"
```

There's also a shorthand for `.concat`: `.+`. That may look a little funny, but it's nothing special, really; it's just a method with a very short (one letter long) name:

<aside markdown="1">
`.concat` as a shorthand for `.+` is not _quite_ true. The `+` method is not just an alias for `concat` — they do slightly different things. But they're close enough, for our purposes.
</aside>

```ruby
"hi".+(" there") # => "hi there"
```

But here's where it gets interesting; Ruby has another bit of nice _syntactic sugar_ for us. If a class has a method named `+`, then you are allowed to drop the `.` before the method name when you call it, and just say:

```ruby
"hi" +(" there") # => "hi there"
```

Wild! And, as we learned earlier when we were [introduced to the `p` method](https://learn.firstdraft.com/lessons/8#make-the-invisible-visible){:target="_blank"}, Ruby also allows you to omit the parentheses around arguments if you want to; so this can be further shortened to:

```ruby
"hi" + " there" # => "hi there"
```

Now this is really starting to look familiar! It's a lot like the calculator language, actually. [Developer happiness](https://learn.firstdraft.com/lessons/8#developer-happiness){:target="_blank"}, indeed.

```ruby
a = "Hello"
b = "World"
p a + b # => "HelloWorld"        # You can add strings together
```

<div class="experiment" markdown="1">

   [Click here for a REPL to try it.](https://repl.it/@raghubetina/concatenation){:target="_blank"}
</div>


<div class="proj" markdown="1">

   Return to the Gitpod `String` project and work through `addition.rb`
</div>

#### String multiplication, a.k.a * 

`String`s can be multiplied by numbers using the `*` method:

```ruby
"Ya" * 5 # => "YaYaYaYaYa"
```

This sort of makes sense, if you think about multiplication as being repeated addition.

<aside markdown="1">
More syntactic sugar here, like with the `+` method above; you can say `"Ya" * 5` rather than `"Ya".*(5)`.
</aside>

```ruby
p "Hello" * 3
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/multiplication){:target="_blank"}
</div>

The order matters, though. See what happens when you try:

```ruby
3 * "Hello"
```

[Read The Error Message (RTEM)](https://learn.firstdraft.com/lessons/7#seriously-please-read-the-error-message){:target="_blank"}!

Does this make sense? `"Hello" * 3` is calling the `String` method `*` with an argument of `3`, which kinda makes sense (add `"Hello"` to itself `3` times).

But `3 * "Hello"` is calling the `Integer` method `*` with an argument of `"Hello"`, which doesn't make much sense (what would it mean to add `3` to itself `"Hello"` times?).

Thus, we can see why the `String` version of `*` and the `Integer` version of `*` both need an integer argument. Again, [the bottom line](https://learn.firstdraft.com/lessons/7#the-bottom-line){:target="_blank"} is — at all times as you are writing Ruby, you should be thinking: "What **class** is this object? What **methods** does _this_ class have available?" Even when there's some syntactic sugar making things _look_ unconventional, don't forget your basics! It's still `noun.verb` under the hood.

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `multiplication.rb`
</div>

----

#### Quiz Question

- The output of this code: `"Hi" * 2 + " you" + "!" * 2` would be...
- HiHi you!!
    - Yes!
{: .free_text #mult_add points="10" answer="1" }

----

#### upcase 

The upcase method returns a copy of the `String` with all lowercase letters replaced with their uppercase counterparts.

```ruby
p "hello".upcase
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/upcase){:target="_blank"}
</div>

#### downcase 

The downcase method returns a copy of the `String` with all uppercase letters replaced with their lowercase counterparts.

```ruby
p "I'M NOT YELLING AT YOU".downcase
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/downcase){:target="_blank"}
</div>

#### swapcase 

The swapcase method returns a copy of the `String` with all uppercase letters replaced with their lowercase counterparts, _and_ vice versa.

```ruby
p "FaMiLy".swapcase # => "fAmIlY
```

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `case.rb`
</div>

#### chomp 

The `chomp` method is mostly used to remove the `"\n"` (newline) character from the end of a string, if it is present:

```ruby
"Raghu\n".chomp # => "Raghu"
"Raghu".chomp # => "Raghu"
```

This seemingly strange task is very common due to the way that getting user input works; usually someone has to type something at a prompt and then they press <kbd>return</kbd> to submit it, and that adds a "newline" (`"\n"`) to the end of the string that they typed. Typically, we want to `chomp` that off the end of their input before we do anything further with it.

`chomp` can also remove other specified character(s) from the end of the string, if they are provided as an argument:

```ruby
"1 apples".chomp("s") # => "1 apple"
"1 apple".chomp("s") # => "1 apple"
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/chomp){:target="_blank"}
</div>

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `chomp.rb`
</div>

#### gsub 

The `gsub` method returns a copy of the `String` it was called on with all occurrences of the first argument substituted for the second argument.

```ruby
a = "Hello"
p a.gsub("ll", "ww")  # => "Hewwo"
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/gsub){:target="_blank"}
</div>

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `gsub.rb`
</div>

#### to_i 

Sometimes you have a string that contains a number, usually input from a user, and want to do math on it. `to_i` will attempt to convert a `String` object into an `Integer` object.

```ruby
p "8".to_i
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/toi){:target="_blank"}
</div>

#### strip 

`strip` removes all leading and trailing whitespace.

```ruby
p "   This has a lot of space on the outside     ".strip
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/strip){:target="_blank"}
</div>

#### capitalize 

capitalize returns a `String` with the first character converted to uppercase and the remainder to lowercase.

```ruby
p "beginning".capitalize
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/capitalize){:target="_blank"}
</div>

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `strip.rb`
</div>

### More on adding strings together

We spend a lot of time composing strings of output for our users, so let's see a few more examples. Try this:

```ruby
number = 6 * 7
message = "Your lucky number for today is " + number + "."
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/String-interpolation){:target="_blank"}
</div>

You'll see that Ruby gets confused (RTEM!), because we are trying to add an integer to a string and it doesn't feel comfortable with that.

The solution is to tell the `Integer` to convert itself to a `String` first using the method called `.to_s`, or "to string". Try this instead:

```ruby
number = 6 * 7
message = "Your lucky number for today is " + number.to_s + "."
```

The above technique for composing strings, adding them together with `+`, is called string addition.

There's another technique for composing strings that I personally find a bit easier; it's called **string interpolation**. Try this instead:

```ruby
number = 6 * 7
message = "Your lucky number for today is #{number}."
```

Basically, inside the string, you place `#{}` where you eventually want your value to go. Inside the curly braces, you can write any Ruby expression without worrying about whether it is a string or not. The expression will be evaluated, converted to a string, and added to the string right in that spot. You can interpolate as many expressions as you want into a single string. Pretty neat!

If you find interpolation confusing, feel free to just use addition.

### Getting strings from users with gets

We can make our programs much more interesting if we allow the users of the program to interact with them by supplying input. We can do this with the `gets` method (pronounced "get S", short for "get string"), which will pause the program and wait for the user to type something in the terminal and press <kbd>return</kbd>. The return value of the `gets` method will be a `String` containing what the user typed, which we can store in a variable and then process further like any other `String`.

For example, rather than saying "Hello, world!", let's have the computer say hello to the user by name instead. When you run this program, it will pause after saying `"What's your name?"` and you will have to type something in and press <kbd>return</kbd>. **Click on the terminal to put focus there**, and then you'll be able to type into it:

```ruby
p "What's your name?"

their_name = gets

p "Hello, " + their_name + "!"
```

<div class="experiment" markdown="1">
   [Click here for a REPL to try it.](https://repl.it/@raghubetina/Hello-gets){:target="_blank"}
</div>

Great! Our first user input. However, you'll notice a couple of things. First of all, there's a `\n` sneaking into the input. `\n` represents a newline character, and it's in there because of the <kbd>return</kbd> that is pressed to submit the input.

#### puts 

If you want to see the newline in action, we can use a different printing method called `Kernel.puts` (pronounced "put S", short for "put string"). `puts` is actually the printing method that is used most when crafting the final output of command-line programs; as opposed to `Kernel.p`, which is used most for _making the invisible visible_ while debugging. Try switching

```ruby
p "Hello, " + their_name + "!"
```

to

```ruby
puts "Hello, " + their_name + "!"
```

and see how the output is different.

You can see that the quotes around the string are removed, which makes sense if you're actually displaying output to a user and not debugging — users should not know or care about the quotes around Ruby string literals. And the newline character causes a line break when a string is printed with `puts`, as it should.

Most of the time, we'll stick with `p`, since it provides more details while debugging; but it's good to know that `puts` exists.

#### gets.chomp 

We almost never want to keep the `\n` that results from the <kbd>return</kbd> keypress that submits the user's input. Fortunately, the handy `.chomp` method we saw above does exactly what we need — if there's a `\n` at the end of a string, it will remove it; if there isn't, it does nothing. So, in practice, when we call `gets` we almost always tack a `.chomp` on to it immediately. Try modifying the program to:

```ruby
their_name = gets.chomp
```

and see how it's different.

<div class="proj" markdown="1">
   Return to the Gitpod `String` project and work through `gets.rb`
</div>

### Conclusion

That's about all we'll need to know about strings to do most anything related to web applications! Next, we'll take a look at numbers, starting with `Integer`.

<span style="font-size: large">**Return to Canvas and head to the next part of the lesson**</span>

----