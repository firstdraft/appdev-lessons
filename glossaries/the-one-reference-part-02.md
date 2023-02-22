# The One Ruby Reference Part 2: ActiveRecord and Association Helper Methods

This glossary should be used as a quick reference for `ActiveRecord` and association accessor methods (`belongs_to`, `has_many`); for more depth, click through to the "Full Explanation"s.

#### How to interpret this reference

Use the table of contents to find a section that interests you. This reference is arranged in a similar manner to the [first Ruby reference](){:target="\_blank"}. As with that reference, each section describes a Ruby _method_. For example, here's what the section `String#split` looks like:

<!-- ![](assets/the-one-reference/how-to-use-the-one-reference.png) -->
![file](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1677087530/how-to-use-the-one-reference_hseuda.png)

 - `String#split => Array` is called the _method signature_:
    - `String` since the method is defined for that class.
    - `#` since it is an instance method (as opposed to a class method, in which case the notation would be `.`).
    - `=> Array` since the _return value_ of this method is an instance of the class `Array`.
 - Then a description of the method.
 - Then examples.
 - Then, usually, a link to the longer explanation from the original chapter where the method was first introduced.

Please let us know if you find errors, omissions, or have any other suggestions or comments. Thank you!

## ActiveRecord_Relation (array of records)

### All Array methods

`ActiveRecord_Relation`s [inherit](https://chapters.firstdraft.com/chapters/769#inheritance){:target="_blank"} from `Array`, so all `Array` methods work:

- [`.each`](#looping-through-arrays){:target="_blank"}
- [`.at()` (and its aliases `[]`, `.first` for `.at(0)`, `.last` for `.at(-1)`)](#at){:target="_blank"}
- [`.count`](#count){:target="_blank"}
- [`.reverse`](#reverse-Array){:target="_blank"}
- [`.sample`](#sample){:target="_blank"}
- [`.shuffle`](#shuffle){:target="_blank"}

### .where

ActiveRecord_Relation#where(Hash) ⇒ ActiveRecord_Relation

Call `.where` on an `ActiveRecord_Relation` to filter the array of records based on some criteria.

`where` returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"} based on the given `Hash`. 

-   `.where` returns an `ActiveRecord_Relation` **regardless of how many results there are**. In particular, even if there is only one result, _the return value will still be another `ActiveRecord_Relation`_.

-   The argument to `.where` is usually a `Hash`:

    -   Filtering by an exact match within a column:

        ```ruby
        { :id => 42 }
        ```

    -   Filter by multiple columns at once:

        ```ruby
        { :photo_id => 23, :user_id => 42 }
        ```

    -   Filter using an `Array` (results will match _any_ of the values in the `Array`):

        ```ruby
        { :owner_id => [4, 8, 15 ] }
        ```

    -   Filtering within a range of values:

        ```ruby
        { :dob => (1.year.ago..Date.today) }
        ```

        ```ruby
        { :last_name => ("A".."C") }
        ```

    -   If you _really_ want to, you can omit the curly brackets around the `Hash` for brevity, and Ruby will figure out what you mean. So, ultimately, you can write something like this:

        ```ruby
        Contact.where(:last_name => ("A".."C"))
        ```

          instead of this:

        ```ruby
        Contact.where({ :last_name => ("A".."C") })
        ```

Related Methods: `.where.not`, `.or`, `.limit`, `.order`

[Full explanation](https://chapters.firstdraft.com/chapters/770#where){:target="_blank"}

### where.not

`ActiveRecord_Relation#where.not(Hash) ⇒ ActiveRecord_Relation`

Call `.where.not` on an `ActiveRecord_Relation` to filter the array of records to _exclude_ records based on the given `Hash`. `.where.not` will return an `ActiveRecord_Relation`.

```ruby
Contact.where({ :last_name => "Mouse" }).where.not({ :first_name => "Mickey" })
```

-   Returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"}.
-   The acceptable arguments to `.not` are the same as to `.where`; see that method for a list.

Related methods: `.where`, `.order`, `.limit`

[Full explanation](https://chapters.firstdraft.com/chapters/770#wherenotthis){:target="_blank"}

### .or

`ActiveRecord_Relation#or(ActiveRecord_Relation) ⇒ ActiveRecord_Relation`

Call `.or` on an `ActiveRecord_Relation` to _combine_ the array of records with another array of records:

-   Returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"}.
-   The argument to `.or` must be another `ActiveRecord_Relation` _from the **same** table_.
-   _Broadens_ the result set.

```ruby
Contact.where({ :first_name => "Mickey" }).or(Contact.where({ :last_name => "Betina" }))
```

[Full explanation](https://chapters.firstdraft.com/chapters/770#wherethisorthat){:target="_blank"}

### .order

`ActiveRecord_Relation#order(Hash) ⇒ ActiveRecord_Relation`

or

`ActiveRecord_Relation.order(Symbol) ⇒ ActiveRecord_Relation`

Call `.order` on an `ActiveRecord_Relation` to sort the array based on one or more columns. This method returns an `ActiveRecord_Relation`.

```ruby
Contact.all.order({ :last_name => :asc, :first_name => :asc, :date_of_birth => :desc })
```

-   Returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"}.

-   The argument to `.order` is usually a `Hash`.

    -   The keys in the `Hash` must be [`Symbol`](#Interlude:-Symbol){:target="_blank"}s that match names of columns in the table. These are the columns that will be used for sorting. If there are multiple keys, the order in which they are provided will be used to break ties.
    -   The value associated to each key must be either `:asc` (for ascending order) or `:desc` (for descending order).

-   The argument to `.order` can also just be one `Symbol`, a column name.

```ruby
Contact.all.order(:last_name)
```

In that case, `:asc` order is assumed.

[Full explanation](https://chapters.firstdraft.com/chapters/770#order){:target="_blank"}

### .limit

`ActiveRecord_Relation#limit(Integer) ⇒ ActiveRecord_Relation`

Call `.limit` on an `ActiveRecord_Relation` to cap the number of records in the array.

-   Returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"}.
-   The argument to `.limit` must be an `Integer`.

```ruby
Contact.where({ :last_name => "Mouse" }).limit(10)
```

[Full explanation](https://chapters.firstdraft.com/chapters/770#limit){:target="_blank"}

### .offset

`ActiveRecord_Relation#offset(Integer) ⇒ ActiveRecord_Relation`

Call `.offset` on an `ActiveRecord_Relation` to discard the first few records in the array:

-   Returns an [`ActiveRecord_Relation`](#activerecord_relation-array-of-records){:target="_blank"}.
-   The argument to `.offset` must be an `Integer`.

```ruby
Contact.where({ :last_name => "Mouse" }).offset(10).limit(10)
```

[Full explanation](https://chapters.firstdraft.com/chapters/770#offset){:target="_blank"}

### .map_relation_to_array

`ActiveRecord_Relation#map_relation_to_array(Symbol) ⇒ Array`

Call `.map_relation_to_array` on an `ActiveRecord_Relation` to retrieve the values stored in _just one column_ of the records, and discard all other data.

-   `.map_relation_to_array` returns a regular Ruby [`Array`](#array){:target="_blank"} of scalar values in the column.

    -   _Not_ a single value, even if there was only one record in the `ActiveRecord_Relation`.
    -   _Not_ an `ActiveRecord_Relation`, so you can no longer use methods like `.where`, `.order`, etc. You can use `Array` methods like `.sort`, `.sample`, etc.

-   The argument to `.map_relation_to_array` must be a `Symbol` that matches the name of a column in the table.

-   You cannot call `.map_relation_to_array` on an individual ActiveRecord row. If you want the value in a column for an individual row, simply call the accessor method directly:

```ruby
Contact.all.map_relation_to_array(:last_name) # => ["Betina", "Mouse", "Woods"]
```

```ruby
# for an array of records
people.last_name # undefined method for array; bad
people.map_relation_to_array(:last_name) # => ["Betina", "Woods"]; good
```

[Full explanation](https://chapters.firstdraft.com/chapters/770#map_relation_to_array){:target="_blank"}

### .maximum

`ActiveRecord_Relation#maximum(Symbol) ⇒ Object`

Call `.maximum` on an `ActiveRecord_Relation` to grab and return the biggest value of a particular column.

```ruby
User.all.maximun(:age)
# => 102
```

-   Returns a value from an `ActiveRecord` column.

[Full explanation](https://chapters.firstdraft.com/chapters/770#maximum){:target="_blank"}

### .minimum

`ActiveRecord_Relation#minimum(Symbol) ⇒ Object`

Call `.minimum` on an `ActiveRecord_Relation` to grab and return the smallest value of a particular column.

```ruby
Photo.all.minimum(:caption) 
# => "... a mind needs books as a sword needs a whetstone, if it is to keep its edge."
```

-   Returns a value from an `ActiveRecord` column.

[Full explanation](https://chapters.firstdraft.com/chapters/770#minimum){:target="_blank"}

### .sum

`ActiveRecord_Relation#sum(Symbol) ⇒ Integer` or `⇒ Float` or `⇒ String`

Call `.sum` on an `ActiveRecord_Relation` to find the sum of the values in a single column:

```ruby
@poem.scores.sum(:points)
```

-   Returns an [`Integer`](#integer) or [`Float`](#integer) (or even a [`String`](#string)){:target="_blank"}, depending on datatype of the column that was summed.
-   The argument to `.sum` must be a `Symbol` that matches the name of a column in the table.

[Full explanation](https://chapters.firstdraft.com/chapters/770#sum){:target="_blank"}

### .average

`ActiveRecord_Relation#average(Symbol) ⇒ Integer` or `⇒ Float`

Call `.average` on an `ActiveRecord_Relation` to find the mean of the values in a single column:

```ruby
@restaurant.reviews.average(:rating)
```

-   Returns an [`Integer`](#integer) or [`Float`](#float){:target="_blank"}, depending on datatype of the column that was averaged.
-   The argument to `.average` must be a `Symbol` that matches the name of a column in the table.

[Full explanation](https://chapters.firstdraft.com/chapters/770#average){:target="_blank"}

## `ActiveRecord` (A single record)

### All column names

You get a method for every column in the table; for example, if you have retrieved an individual record from the `Contact` table, you can call `.first_name`, `.last_name`, etc, on it.

This means that every `ActiveRecord` object will have methods `.id`, `.created_at`, and `.updated_at`, since every table has those columns.

[Full explanation](https://chapters.firstdraft.com/chapters/770#attribute-getter-methods){:target="_blank"}

### Any other instance methods you define in the class

It's often helpful to define your own instance methods in the model file; for example, you might want to define a method `.full_name`:

```ruby
class Contact < ApplicationRecord
  def full_name
    return self.first_name + " " + self.last_name
  end
end
```

You would then be able to call `.full_name` anywhere in the application that you wind up with an individual `Contact` object.

[Full explanation](https://chapters.firstdraft.com/chapters/769#defining-instance-methods){:target="_blank"}

## Association Helper Methods

### belongs_to

`belongs_to(Symbol, Hash) ⇒ ActiveRecord`

Let's say I have a movie in a variable `m`. It is annoying and error prone to, whenever I want the director associated with a movie, have to type

```ruby
d = Director.where({ :id => m.director_id }).at(0)
```

Wouldn't it be great if I could just type

```ruby
d = m.director
```

and it would know how to go look up the corresponding row in the directors table based on the movie's `director_id`?

Unfortunately, I can't, because `.director` isn't a method that `Movie` objects automatically know how to perform — the method would be undefined. (`Movie` objects know how to perform `.director_id` because we get a method for every column in the table.)

We could define such an instance method in the model ourselves without too much trouble. But, fortunately, since domain modeling and associations are at the heart of every application's power, Rails gives us a shortcut. Go into the `Movie` model and add a line like this:

```ruby
belongs_to(:director, { :class_name => "Director", :foreign_key => "director_id" })
```

This line tells Rails:

-   `belongs_to`: We only one result (not an array of results).
-   `:director`: Define a method called `.director` for all movie objects.
-   `:class_name => "Director"`: When someone invokes `.director` on a movie, go fetch a result from the directors table.
-   `:foreign_key => "director_id"`: Use the value in the `director_id` column of the movie to query the directors table for a row.

This is exactly what we would do if we defined the instance method by hand:

```ruby
def director
  return Director.where({ :id => m.director_id }).at(0)
end
```

Either way, we now can utilize this handy shortcut anywhere in our application when we have a movie `m` and we want to get the record in the directors table associated with it:

```ruby
m.director
```

Even better, if you've named your method and foreign key column conventionally (exactly matching the name of the other table), you can use the super-shorthand version:

```ruby
belongs_to(:director)
```

-   If you omit specifying the `:class_name`, Rails assumes that the table that you want to query is named the same thing as the method you are defining.

-   If you omit specifying the `:foreign_key`, Rails assumes that the foreign key column is named the same thing as the method plus `_id`.

-   If either of those things happens to not be true, then just include the `Hash` as the second argument to `belongs_to` and spell it all out:

    ```ruby
    belongs_to(:owner, { :class_name => "User", :foreign_key => "poster_id" })
    ```

    This would give us a method called `.owner` that returns a `User`, even though the foreign key column is called `poster_id`. We still have complete control, if we need to depart from conventional method/foreign key names for some reason.

### has_many

`has_many(Symbol, Hash) ⇒ ActiveRecord_Relation`

Let's say I have a director in a variable `d`. It is annoying and error prone to, whenever I want the films associated with the director, have to type

```ruby
f = Movie.where({ :director_id => d.id })
```

Wouldn't it be great if I could just type

```ruby
f = d.movies
```

and it would know how to go look up the corresponding rows in the movies table based on the director's `id`?

Unfortunately, I can't, because `.movies` isn't a method that `Director` objects automatically know how to perform — the method would be undefined.

We could define such an instance method in the model ourselves without too much trouble. But, fortunately, since domain modeling and associations are at the heart of every application's power, Rails gives us a shortcut. Go into the `Director` model and add a line like this:

```ruby
has_many(:movies, { :class_name => "Movie", :foreign_key => "director_id" })
```

This line tells Rails:

-   `has_many`: We want many results in an array.
-   `:movies`: Define a method called `.movies` for all director objects.
-   `:class_name => "Movie"`: When someone invokes `.movies` on a director, go fetch results from the movies table.
-   `:foreign_key => "director_id"`: Use the `director_id` column of the movies table to filter using the `id` of the director.

This is exactly what we would do if we defined the instance method by hand:

```ruby
def movies
  return Movie.where({ :director_id => self.id })
end
```

Either way, we now can utilize this handy shortcut anywhere in our application when we have a director `d` and we want to get the records in the movies table associated with it:

```ruby
d.movies
```

Even better, if you've named your method and foreign key column conventionally (exactly matching the name of the other table), you can use the super-shorthand version:

```ruby
has_many(:movies)
```

-   If you omit specifying the `:class_name`, Rails assumes that the table that you want to query is named the same thing as the method you are defining.

-   If you omit specifying the `:foreign_key`, Rails assumes that the foreign key column is named the same thing as this model plus `_id`.

-   If either of those things happens to not be true, then just include the `Hash` as the second argument to `belongs_to` and spell it all out:

    ```ruby
    has_many(:filmography, { :class_name => "Movie", :foreign_key => "director_id" })
    ```

    This would give us a method called `.filmography` that returns `Movie`s. We still have complete control, if we need to depart from conventional method/foreign key names for some reason.

### has_many/through

`has_many(Symbol, Hash) ⇒ ActiveRecord_Relation`

After you have established all of your one-to-many association helper methods, you can also add many-to-many helper methods with the `:through` option on `has_many`:

```ruby
class Movie < ApplicationRecord
   has_many(:characters)
   has_many(:actors, { :through => :characters, :source => :actor })
end

class Character < ApplicationRecord
  belongs_to(:movie)
  belongs_to(:actor)
end

class Actor < ApplicationRecord
   has_many(:characters)
   has_many(:movies, { :through => :characters, :source => :movie })
end
```