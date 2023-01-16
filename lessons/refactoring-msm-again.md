# Refactoring MSM Again

- Notes:

  - [Day 7 video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=6da49302-4503-454a-9659-aedf005f678f){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/refactoring-MSM-queries-again.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/refactoring-msm-queries-2](https://github.com/appdev-projects/refactoring-msm-queries-2){target="_blank"}

  - Target: [https://github.com/appdev-projects/refactoring-msm-queries-1](https://github.com/appdev-projects/refactoring-msm-queries-1){target="_blank"}

  - Helper application demo'd in video: https://association-accessors.firstdraft.com/


## Video Segment: `belongs_to`

- Notes:

  - time stamp 00:51:43 to 01:01:06
  - refactor 1-N `Character#movie`, going from the "many" to the "one"
  - why `belongs_to` is better than previous method definitions
  - aside into `.joins` at the `rails console`

If we open the model files in our new project, then we will see that the association accessor methods, like `Movie#director` and `Director#filmography`, have already been defined in the models.

Let's take a look at two side-by-side: `Character#movie` and `Movie#director`:

```ruby
# app/models/character.rb

# == Schema Information
#
# Table name: characters
#
#  id         :integer          not null, primary key
#  name       :string
#  created_at :datetime         not null
#  updated_at :datetime         not null
#  actor_id   :integer
#  movie_id   :integer
#
class Character < ApplicationRecord
  def movie
    key = self.movie_id

    matching_set = Movie.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end
end
```

```ruby
# app/models/movie.rb

# == Schema Information
#
# Table name: movies
#
#  id          :integer          not null, primary key
#  description :text
#  duration    :integer
#  image       :string
#  title       :string
#  year        :integer
#  created_at  :datetime         not null
#  updated_at  :datetime         not null
#  director_id :integer
#
class Movie < ApplicationRecord
  def director
    key = self.director_id

    matching_set = Director.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end
end
```

Both of these methods are from a 1-N association and represent going from the "many" back over to the "one" that it belongs to. If I am a `Movie`, I contain a foreign key, the `director_id` column, and I want to take that value, go to the ID column of `Director`, find the matching record, and return it. The same goes for `Character#movie`.

All of our association accessor methods follow the same pattern! What if we want to define the `Character#actor` 1-N association?

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  def movie
    key = self.movie_id

    matching_set = Movie.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end

  def actor
    key = self.actor_id

    matching_set = Actor.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end
end
```
{: mark_lines="15-23"}

Compare the `movie` and `actor` method. They are almost identical with just a difference in a few names.

Defining association accessor methods is incredibely important for a good, maintainable code base. And, because of how formulaic this is, Rails makes it easy to automate! The "Pit of Success" of Rails! **BENP: link or define pit of success**

There are three things that changed between `movie` and `actor`: the name of the method, the name of the foreign key column, and the name of the class that we search in.

There's a meta method called `belongs_to()`, which can be used outside of the method definitions directly in the model. This method will define our association accessor for us if we give it just three arguments:

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  belongs_to(:name_that_we_want, { :class_name => "", :foreign_key => "" })

  def movie
    key = self.movie_id

    matching_set = Movie.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end
...
end
```
{: mark_lines="5"}

The first argument is the name of the method we want, then a hash with two key/value pairs containing the name of the class and the foreign key. So if we want a method `.movie` that we can call on `Character`, we can just write (and comment out or delete our old code):

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  belongs_to(:movie, { :class_name => "Movie", :foreign_key => "movie_id" })

  # def movie
  #   key = self.movie_id

  #   matching_set = Movie.where({ :id => key })

  #   the_one = matching_set.at(0)

  #   return the_one
  # end
...
end
```
{: mark_lines="5"}

Try this out. Comment or delete the `def movie` section of the model once you have the `belongs_to()` filled out. Visit in your app browser an actor details page (did you run `rails sample_data` yet?). For instance **/actors/343**. Now if we scroll down to the "Filmography" table, there is a column showing the character name in each movie for the given actor. So everything is still working even though we deleted our previous association accessor method!

**BENP: Why `belongs_to` is Better, starting below, from: 01:01:06 to 01:09:14**

The `def movie` that we wrote out line-by-line and the new `belongs_to` version are producing the same thing. But `belongs_to` is somewhat shorter, and it reads better (is easier to understand at a glance).

Moreover, we can look at an example in our Rails console for why this technique is so good. Open a `rails console`. 

What if we asked for all of the characters from movies that are newer than 1994? Until today we couldn't do that! 

We can use a new method called `.joins`, which you give the name of an association that you declared with `belongs_to` (it *must* be declared this way for `.joins` to work). Then you can use `.where` and the association accessor with another hash that searches over a specific range specified by another column:

```ruby
pry(main)> Character.joins(:movie).where("movies.year > 1994")
```

Note here that when using `joins`, `where` takes its argument as a string rather than a hash. That will return an `ActiveRecord::Relation` with all of the movies of interest.

It is very common to query one table with the columns of another. And if we look at the SQL issued by the relatively simple Ruby command above, then we see it is getting pretty tricky to write, and `ActiveRecord` just does that for us.

Yet another reason that `belongs_to` is great, is that we can write: 

```ruby
belongs_to(:movie, { :class_name => "Movie", :foreign_key => "movie_id" })
``` 

as simply

```ruby
belongs_to(:movie)
``` 

We can delete most of the code because the method `belongs_to` will follow a well defined pattern of naming! So as long as the function, table, and foreign key columns share the same name (with only capitalization difference), then we can write a very short, explicit, and clear association accessor method.

If you prefer to write out the entire thing, you are welcome to, but this is just another shortcut in your toolbox.



### Text Companion: `belongs_to`

## Video Segment: `has_many`

- Notes:

  - time stamp 01:09:14 to 01:13:08
  - refactor 1-N `Movie#characters`, going from the "one" to the "many"
  - aside into method syntax for `Director#filmography`

### Text Companion: `has_many`

As opposed to `belongs_to(:movie)` in `Character` (`Character#movie`), we also want to have a `Movie#characters` method, which is the other side of the relationship, the many to the one. We could define this ourselves like so:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  def characters
    key = self.id
    the_many = Character.where( {:movie_id => key })
    return the_many
  end

  def director
    key = self.director_id

    matching_set = Director.where({ :id => key })

    the_one = matching_set.at(0)

    return the_one
  end
end
```
{: mark_lines="5-9"}

This is a different method compared to the one to the many. Of course, the `director` method could already be replaced with just `belongs_to(:director)`! But how can we replace `def characters`? 

`belongs_to(:characters)` won't work, that will write the wrong method in this case, because our new method does not follow the expected pattern for a one to a many. 

We need to use the method `has_many`, which has a similar form:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  belongs_to(:director)
  has_many(:characters, { :class_name => "Character", :foreign_key => "character_id" })

  # def characters
  #   key = self.id
  #   the_many = Character.where( {:movie_id => key })
  #   return the_many
  # end
...
end
```
{: mark_lines="6-7"}

All we did was provide the method with the three pieces of information that we expect to vary: the name of the method, name of the class, and name of the foreign key. And then `has_many` writes an association accessor method for us of the form that we put together in `def characters`.

Similar to `belongs_to`, if the three arguments match, we can write:

```ruby
has_many(:characters, { :class_name => "Character", :foreign_key => "character_id" })
``` 

as simply

```ruby
has_many(:characters)
``` 

This shortcut only works if the names match! For instance, in our `Director` class, we have an association accessor method called `filmography`. 

We could have called this `movies`, which would have allowed us to write `has_many(:movies)`, but if we wrote `has_many(:filmography)`, then Rails would look for a class called `Filmography`, and a foreign key column called `filmography_id`, neither of which exist!

So in the case where we selected our own, non-conventional names, then we need to be explicit and write: 

```ruby
has_many(:filmography, { :class_name => "Movie" })
``` 

We can still omit the foreign key, because now the method will know to call the foreign key `movie_id` based on the `:class_name`.



## Video Segment: Other Relationships and Wizard

- Notes:

  - 01:13:08 to 01:26:00
  - classroom work using https://association-accessors.firstdraft.com/

```
Define all 6 1-Ns using belongs_to and has_many: Actor#characters, Character#actor, Movie#characters, Character#movie, Director#filmography, Movie#director
```

**BENP: the end of the video is classwork and then showing off the app https://association-accessors.firstdraft.com/. This could be a separate video, not going to transcribe this for now. Might be best as just video content?**

## Finish and Submit Refactoring MSM -- Again!