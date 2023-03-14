## Hash

`Array` is a very good structure for containing multiple objects, but it's not the only one. In some situations, another structure is a better tool for the job: `Hash`.

Suppose we have instructors and students:

```ruby
instructors = ["Raghu", "Logan", "Jelani"]
students = ["Jocelyn", "Arthur", "Tom", "Lindsey"]
```

Suppose we want add last names and roles?

```ruby
person1 = ["Raghu", "Betina", "Instructor"]
person2 = ["Jocelyn", "Williams", "Student"]
# etc

p person1.at(0) + " is an " + person1.at(2)
p person2.at(0) + " is a " + person2.at(2)
```

This may suffice if the list of attributes is small, but six months later when you come back to this code, do you really want to remember which index number was last name and which was first name and which was role? Not to mention always dealing with the array-indexes-begin-with-0-and-not-1 thing in your head.

There's a better way: rather than having `Array`s automatically number each piece of data, _we_ can give them meaningful labels in a `Hash`.

### A brief interlude: Symbols

There is one datatype that we haven't discussed until now that will come in handy: `Symbol`s.

`Symbol`s are like `String`s: a sequence of characters. However, `Symbol`s follow the same rules as variable names:

 - Cannot contain spaces.
 - Can only contain lowercase letters, underscores, and numbers.
 - Cannot begin with a number.

Otherwise, they are just like strings, and we can use them to hold text data:

```ruby
"hello" # I am a String
:hello  # I am a Symbol
```

`Symbol`s are created by starting them off with a colon. You don't need a closing colon, since they cannot contain spaces; Ruby can figure out where they end.

`String`s are usually used to contain copy for the user or input from the user; whereas `Symbol`s are mostly used when we, the developers, need to label something internally in our code. That's why they can't contain spaces, etc; we're not going to use them to hold user input. Accordingly, `Symbol`s don't have as many methods for transforming their contents, like `.reverse`.

So, that's that. `Symbol`s are lightweight strings that we, the developers, use when we need to label things. Let's continue.

----

#### Quiz Question

- Which of these is a valid `Symbol`?
- `"my_symbol"`
    - No, that's a string
- `:my_symbol`
    - Yes!
- `:MySymbol`
    - No, we only use lowercase letters to create a symbol
- `: my_symbol`
    - No, look out for extra whitespace
- `:my symbol`
    - No, look out for extra whitespace that should be an underscore
{: .choose_best #symbol_syntax points="10" answer="2" }

----

### Creating hashes and storing values

Back to the problem of storing a list of attributes about a person effectively, without mixing them up.
`Hash`es are like `Array`s, except each cell isn't automatically numbered — **we get to label each cell ourselves**. So instead of representing a person with an Array like `["Raghu", "Betina", "Instructor"]`, we instead can use a `Hash` like this:

```ruby
person1 = Hash.new
p person1

person1.store(:first_name, "Raghu")
p person1

person1.store(:last_name, "Betina")
p person1

person1.store(:role, "Instructor")
p person1

p person1.fetch(:role)
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/hash-hash-new){:target="_blank"}
</div>

Click "Run" and see what it looks like to build up a `Hash`. A few things to note:

 - Ruby represents a `Hash` with curly brackets, `{}`, as opposed to the square brackets (`[]`) of an `Array`.
 - We use the `.store` method to add elements to a `Hash`, as opposed to the `.push` method of `Array`.
 - The `.store` method takes _two_ arguments, not one: the first argument is the label, or **key** to store the element under; and the second argument is the piece of data itself, or the **value**.
 - Ruby represents each key/value pair by separating them with a `=>`, known as a "hash rocket" (Rubyists are weird).
 - As in `Array`s, elements in the list (each element is one key/value _pair_) are separated by commas.
 - If the key already exists when you try to `.store` something under it, its value will be replaced.

### fetch

To retrieve a piece of data from a `Hash`, we use the `.fetch` method (as opposed to `Array`'s `.at`):

```ruby
person1 = Hash.new
person1.store(:first_name, "Raghu")
person1.store(:last_name, "Betina")
person1.store(:role, "Instructor")

p person1.fetch(:last_name)
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/hash-fetch){:target="_blank"}
</div>

Beautiful! Now we don't have to remember that position number 1 is last name, position number 2 is role, etc. We can retrieve objects from the list using meaningful labels instead.

Let's put it all together with multiple `Hash`es:

```ruby
person1 = Hash.new
person1.store(:first_name, "Raghu")
person1.store(:last_name, "Betina")
person1.store(:role, "Instructor")

person2 = Hash.new
person2.store(:first_name, "Jocelyn")
person2.store(:last_name, "Williams")
person2.store(:role, "Student")

p person1.fetch(:first_name) + " is a " + person1.fetch(:role)
p person2.fetch(:first_name) + " is a " + person2.fetch(:role)
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/hash-second-person){:target="_blank"}
</div>

----

#### Quiz Question

- What happens when you try to `.fetch` on `person1` using a string like `"role"` or a key that isn't there like `:middle_name`?
- `"role"` still returns the role, `:middle_name` returns `nil`
    - Really? Did you try it?
- `"role"` returns an error, `:middle_name` returns `nil`
    - Really? Did you try it?
- `"role"` returns an error, `:middle_name` returns an error
    - Yes!
- `"role"` returns `nil`, `:middle_name` returns `nil`
    - Really? Did you try it?
{: .choose_best #hash_error points="10" answer="3" }

----

#### fetch fallback

Get used to error messages when you're working on fetching from `Hash`es. You're going to see them a _lot_.

Sometimes you may want to call `.fetch` using a key that may not be present in the `Hash`, and you don't want the program to crash with the "key not found" error message. In that case, you can provide a second argument which will be used as a fallback return value:

```ruby
person1 = Hash.new
person1.store(:first_name, "Raghu")
person1.store(:last_name, "Betina")
person1.store(:role, "Instructor")

p person1.fetch(:first_name, "None provided")
p person1.fetch(:middle_name, "None provided")
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/hash-fetch-with-fallback){:target="_blank"}
</div>

### Hash literals

Like `String` and `Array`, there's a shortcut to creating `Hash`es: rather than formally instantiating a new `Hash` with `Hash.new` and then building it up from scratch one key/value pair at a time with `.store`, you can type out the **hash literal** directly into your code:

```ruby
person1 = { :first_name => "Raghu", :last_name => "Betina", :role => "Instructor" }
person2 = { :first_name => "Jocelyn", :last_name => "Williams", :role => "Student" }
```

Like with `String` and `Array`, this is the style that we're going to use the vast majority of the time.

In particular, `Hash`es are very often used as the arguments to methods, because they let us pass in a list of inputs with nice labels. When we get to Ruby on Rails, especially, we will very often type hash literals directly into the parentheses of method arguments, things like:

```ruby
Movie.where({ :title => "The Shawshank Redemption" })
```

----

#### Quiz Question

Consider the hash:

```ruby
feeding_time = { :bear => "salmon", :zebra => "grass", :monkey => "banana" }
```

- Check all that apply
- The symbols `:bear`, `:zebra`, and `:monkey` are the values, and `"salmon"`, `"grass"`, and `"banana"` are the keys
    - No, please re-read the previous section
- The strings `:bear`, `:zebra`, and `:monkey` are the keys, and `"salmon"`, `"grass"`, and `"banana"` are the values
    - No, is `:bear` a string?
- The symbols `:bear`, `:zebra`, and `:monkey` are the keys, and `"salmon"`, `"grass"`, and `"banana"` are the values
    - Yes!
- We should have used square brackets `[]` to make the `Hash`!
    - No, please re-read the previous section
- We could add another key/value pair with the code `feeding_time.store("cereal", :human)`
    - No, please re-read the previous section
- We could add another key/value pair with the code `feeding_time.store(:human, "cereal")`
    - Yes!
{: .choose_all #feeding_time points="10" answer="[3,6]" }

----

#### Quiz Question

- In the previous `feeding_time` variable, how would you retrieve the string `"grass"`?
- feeding_time.fetch(:zebra)
    - Yes!
- .fetch(:zebra)
    - Yes!
- fetch(:zebra)
    - Yes!
{: .free_text #feeding_fetch points="10" answer="[1,2,3]" }

----

### fetch shorthand, []

Much like `Array`'s shorthand for `.at`, `[]`, `Hash` also a shorthand for retrieving elements with `.fetch`: `.[]` (and the associated syntactic sugar). So we _could_ write:

```ruby
person1 = { :first_name => "Raghu", :last_name => "Betina", :role => "Instructor" }

p person1[:last_name]
```

_However_, unlike with `Array`, `Hash`'s `.[]` method and `.fetch` method do _not_ do the exact same thing. Experiment with them and see if you can find the difference:

```ruby
person1 = { :first_name => "Raghu", :last_name => "Betina", :role => "Instructor" }

p person1.fetch(:last_name)
p person1[:last_name]
```

<div class="experiment" markdown="1">

  [Click here for a REPL to try it.](https://repl.it/@raghubetina/hash-fetch-shorthand){:target="_blank"}
</div>

Were you able to find the difference between the two methods?

---

`Hash`'s `.[]` method, when used with a key that is not present in the hash, _returns `nil` rather than throwing an error_.

I personally prefer getting the descriptive error message if the key is not present in the hash, because it means that I probably made a typo or some other mistake, and I prefer being alerted to that fact rather than the program proceeding quietly only to fail elsewhere. In the rare case that it should be possible for a key to be optionally present in a hash, then I can use a fallback second argument to `.fetch`, as described above.

That said, out on the internet, using `.[]` is the most prevalent style of accessing hashes, so you should be familiar with it. But in this text, I will stick with `.fetch`.

### store shorthand, []=

Similar to the shorthand for `.fetch` above, there's a shorthand for `.store`: `[]=`

```ruby
person1 = Hash.new
person1[:first_name] = "Raghu"
person1[:last_name] = "Betina"
person1[:role] = "Instructor"

p person1
# => { :first_name => "Raghu", :last_name => "Betina", :role => "Instructor" }
```

This syntactic sugar makes it _feel_ like we're doing variable assignments to keys within the `Hash`, but under the hood it's identical to `.store(:key, :value)`.

<div class="proj" markdown="1">

  Open the Gitpod [`Hash` project](https://github.com/appdev-projects/ruby-project-hash-1){:target="_blank"} on Canvas that follows this reading and start with the exercise `person.rb`.

  For a Gitpod refresher, see [this section](https://learn.firstdraft.com/lessons/9#start-the-gitpod-project){:target="_blank"} in `String`, where we opened our first workspace.
</div>

### Use .keys to explore

A very important method to use when you're dealing with `Hash`es that you didn't create yourself is `.keys`:

```ruby
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
h.keys       #=> ["a", "b", "c", "d"]
h.fetch("b") # => 200
```

The `.keys` method returns an `Array` showing all of the keys that are present in the `Hash`, so that we know what we can `.fetch`.

This helps tremendously when dealing with a data structure that we didn't create ourselves, especially when it's deeply nested (a hash containing arrays which might contain other hashes, etc).

### keys can be anything

The keys in a `Hash` can be any class — `String`, `Integer`, whatever — but we almost always use `Symbol`s as keys to our `Hash`es. (I like using symbols as the keys simply because since the values are usually strings, syntax highlighting makes keys stand out from values in our code.)

### values can be anything

Similarly, the value stored under a key can be an object of any class. This means that you can have a `Hash` that contains an **entirely separate** `Hash` or `Array` object. Take this example:

```ruby
dictionary = {
  :colors => ["red", "green", "blue"],
  :person => {
    :name => "Jenna Parker",
    :age => 32
  }
}
```

In order to retrieve the value `"green"` from this `Hash`, we first need to access the `Array` under the key `:colors`.

```ruby
colors_array = dictionary.fetch(:colors)
# =>  ["red", "green", "blue"]
```

----

#### Quiz Question

- Now that we have `colors_array`, how can we get the string `"green"`?
- `colors_array.at(1)`
    - Yes!
- `colors_array.at(2)`
    - No, remember zero indexing
- `colors_array.fetch("green")`
    - No, we're dealing with an `Array` object, how do we fetch from that?
- `colors_array.fetch(1)`
    - No, we're dealing with an `Array` object, how do we fetch from that?
{: .choose_best #get_green points="10" answer="1" }

----

Similarly, to retrieve `32` from the `Hash`, we first need to access the inner `Hash` under the key `:person`.

```ruby
person_hash = dictionary.fetch(:person)
# => { :name => "Jenna Parker", :age => 32 }
```

----

#### Quiz Question

- Now that we have the inner `Hash` (`person_hash`), how can we get the integer `32`?
- `person_hash.at(1)`
    - No, we're dealing with a `Hash` object, how do we fetch from that?
- `person_hash.at(2)`
    - No, we're dealing with a `Hash` object, how do we fetch from that?
- `person_hash.fetch(:name)`
    - No, which key do we want to fetch?
- `person_hash.fetch(32)`
    - No, which key do we want to fetch?
- `person_hash.fetch("age")`
    - No, we want to fetch on a symbol as the key
- `person_hash.fetch(:age)`
    - Yes!
{: .choose_best #get_age points="10" answer="6" }

----

<div class="proj" markdown="1">

  Return to the Gitpod `Hash` project and work through `dig.rb`
</div>

### key

The `.key` method is sort of the inverse of `.fetch`: given an object, `.key` searches through each value in the hash and returns the key where it resides or `nil` if it doesn't exist in the hash.

```ruby
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
h.key(100)   #=> "a"
h.key(200)   #=> "b"
h.key(300)   #=> "c"
h.key(400)   #=> "d"
h.key(500)   #=> nil
```

<div class="proj" markdown="1">

  Return to the Gitpod `Hash` project and work through `find_value.rb`
</div>

<div class="proj" markdown="1">

  Finally, in the Gitpod `Hash` project work through `list.rb`
</div>

### Conclusion

`Array`s are very useful for storing a list of things that are all basically the same, and for lists that are of unknown length, and so it's nice for Ruby to automatically number them for you.

But when you are storing a list of things that are categorically different from one another and you'd rather label them yourself, then `Hash`es are a better choice. That's about it!

The last intro topic to cover in the next section is creating our own classes in Ruby.

<span style="font-size: large">**Return to Canvas and head to the next part of the lesson**</span>

----