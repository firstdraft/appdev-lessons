# Refactoring Must See Movies

- Notes:

  - [Original day 6 recording video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=69b47533-78a4-40f4-80a1-aed9010f30f8){:target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/refactoring-MSM-queries.md){:target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/refactoring-msm-queries-1](https://github.com/appdev-projects/refactoring-msm-queries-1){:target="_blank"}

  - Target: [https://msm-queries.matchthetarget.com/](https://msm-queries.matchthetarget.com/){:target="_blank"}

  - Useful chapters:

    - [Refactoring MSM Queries with Methods][Refactoring MSM Queries with Methods]

## Video Segment: Exploring the Target, What is Refactoring?

- Notes:

  - time stamp 00:01:45 to 00:06:57
  - explore target, which is a solution to MSM Queries
  - technical debt, refactoring
  - automated tests with `rails grade`

Here's the plan for today's assignment. First, we're going to look at a project called refactoring MSM queries. The starting point of that assignment is the ending point for MSM queries. So once you set up your workspace you'll have a solution for the homework. 

So the first thing that you should do is look through the starting point for refactoring MSM queries. Compare this solution to your solution. Compare my code to your code and try to think of some questions about the choices that I made. If nothing else, compare my actor details view template and your actor details view template, because there is a lot going on there. 

Practice *reading* the code and reasoning your way through it, line by line; explain it to yourself, or to your rubber ducky. Developers read far more code than we write.

[Here is the assignment](https://github.com/appdev-projects/refactoring-msm-queries-1){:target="_blank"}. As usual:

1. Start the web server by running `bin/server`.
2. Navigate to your live application preview.
3. As you work, remember to navigate to **/git** and *Always Be Committing (ABC)*.
4. Organize your workspace tabs.
5. Run `rails grade` as often as you like to see how you are doing, but make sure you **test your app manually first** to make sure it matches the target's behavior.

**BENP: possible image(s) (better, GIFs?) of starting a workspace, opening /git, organizing tabs, noting the target favicon. But these are probably in a different chapter.**

The target for this project is [here](https://msm-queries.matchthetarget.com){:target="_blank"}. It is the same as MSM Queries, because the functionality is unchanged, just refactored!

A refactoring will not change the visual appearance, or anything related to functionality. On a team, when you go through a refactoring sprint or chunk of work, your users should not be affected.

We're just trying to improve the code base and pay off *technical debt*. A lot of times we know it's not the best way it could be done, we know there's repetitive stuff, so refactoring is when we pause, freeze the functionality and pay off the *technical debt*.

And that's why *automated tests* like `rails grade` are amazing. We've been writing all the automated tests for you and we just run them with Rails. But in a real world setting, refactoring is where automated tests really pay off. If you don't have automated tests, you never pay off that technical debt because you're afraid of breaking something.

We're going to make the code much more modular and re-usable, while keeping the functionality exactly the same. How? By **defining methods** to encapsulate our querying logic.



### Text Companion: Exploring the Target, What is Refactoring?

## Video Segment: Actor Details `show` Page

- Notes:

  - time stamp 00:06:57 to 00:09:14
  - examine view template and `show` action in `app/controllers/actors_controller.rb`
  - reiterate `ActiveRecord::Relation`

Now that we have our `bin/server` running, I'm going to visit an actor details page myself in the browser of my app. If you don't have any data in this brand new project and workspace, open up a new terminal, run `rails sample_data`, and get some stuff to look at.

Once you have data you can click through the list of actors at **/actors** and find Morgan Freeman, then "Show details" to end up on that page with the URL path **/actors/2** (or whatever Morgan Freeman's `id` number is in that second path segment).

You see I have the filmography on the page. So this is a working version MSM Queries to begin with.

Let's zoom in on the actual code by opening the actor details view template:

```html
<!-- app/views/actor_templates/show.html.erb -->

<h1>
  Actor #<%= @the_actor.id %> details
</h1>

...

<dl>
  <dt>
    Name
  </dt>
  <dd>
    <%= @the_actor.name %>
  </dd>

  <dt>
    Dob
  </dt>
  <dd>
    <%= @the_actor.dob %>
  </dd>

  ...

</dl>

...
```

I have this instance variable called `@the_actor`, which I set up in the action that I made in the controller:

```ruby
# app/controllers/actors_controller.rb

class ActorsController < ApplicationController
  def index
    matching_actors = Actor.all
    @list_of_actors = matching_actors.order({ :created_at => :desc })

    render({ :template => "actor_templates/index.html.erb" })
  end

  def show
    the_id = params.fetch("path_id")

    matching_actors = Actor.where({ :id => the_id })
    @the_actor = matching_actors.at(0)
      
    render({ :template => "actor_templates/show.html.erb" })
  end
end
```
{: mark_lines="11-18"}

I did this standard dance, which we're going to be doing a lot, which is get the `id` number out of the path. This is the dynamic segment of the path: `path_id`. And then look up the actors where that value appears in the `id` column. That `.where` method returns an `ActiveRecord::Relation` in the `matching_actors` variable. `ActiveRecord::Relation`s contain some number of records, which match the search criteria that we put in.

If you're searching an `id` column, of course we know there's only going to be one record and that's unique. Or there might be zero records in case we provide an `id` that doesn't exist. There's only going to be zero or one. But we still have to get that first element out of the relation, so we use `.at(0)` to get the `@the_actor` instance variable for the view template.



### Text Companion: Actor Details `show` Page

## Video Segment: `ActiveRecord::Relation` Review

- Notes:

  - time stamp 00:09:14 to 00:12:05
  - `rails console` to explore `ActiveRecord` objects

To review, an `ActiveRecord::Relation` is very similar to an array, but in this case the only thing they can contain are individual `ActiveRecord` objects, which are rows in the table. These rows then have attributes (column values) that we can get data from using the *column accessor method*. For instance, at the `rails console`:

```ruby
pry(main)> m = Movie.all
  (0.1ms)  SELECT COUNT(*) FROM "movies"
=> Movie::ActiveRecord::Relation (array with 52 Movie instances inside)
```

`.all` returns an array-like object with 52 movie instances, and when I get the first one out:

```ruby
pry(main)> x = m.first
  Movie Load (0.2ms)  SELECT "movies".* FROM "movies" ORDER BY "movies"."id" ASC LIMIT ?  [["LIMIT", 1]]
=> #<Movie:0x000055ba1a471588
 id: 1,
 title: "The Shawshank Redemption",
 year: 1994,
 duration: 142,
:
```

Now I have a single instance of `Movie`, which I can call methods on to get column values:

```ruby
pry(main)> x.title
=> "The Shawshank Redemption"
pry(main)> x.year
=> 1994
```

We can note some similarities to hashes for our `x` instance of `Movie`:

```ruby
pry(main)> x.fetch(:title)
=> "The Shawshank Redemption"
pry(main)> x[:title]
=> "The Shawshank Redemption"
```

but these are *not* hashes, because we can call methods like `.title` from the table columns directly on them.



### Text Companion: `ActiveRecord::Relation` Review

## Video Segment: Actor Details Filmography

- Notes:

  - time stamp 00:12:05 to 00:15:31
  - `ActiveRecord::Relation` objects in `app/views/actor_templates/show.html.erb` to query from `Actor` to `Character`, `Character` to `Movie`, and `Movie` to `Director` on

So we look at this details page view template:

```html
<!-- app/views/actor_templates/show.html.erb -->

...

<dl>
  <dt>
    Name
  </dt>
  <dd>
    <%= @the_actor.name %>
  </dd>

  <dt>
    Dob
  </dt>
  <dd>
    <%= @the_actor.dob %>
  </dd>

...
```

So first, we're using the instance variable, the `@the_actor` objects, and we're saying `.name`, `.dob`, etc., which you can do because these columns exist. So we get a method for each column, a column acts as a method for free from `ActiveRecord`, we didn't have to define them.

Then I get down to the filmography part of the page lower down:

```html
<!-- app/views/actor_templates/show.html.erb -->

...

<h2>Filmography</h2>

<table border="1">
  ...

  <% a_id = @the_actor.id %>

  <% matching_characters = Character.where({ :actor_id => a_id }) %>
  
  <% matching_characters.each do |a_character| %>
    <% m_id = a_character.movie_id %>

    <% matching_movies = Movie.where({ :id => m_id }) %>

    <% the_movie = matching_movies.at(0) %>

    <tr>
      <td>
        <%= the_movie.title %>
      </td>

      ...

  <% end %>
</table>
```
{: mark_lines="10-19"}

If you remember the domain model here, `actors` and `movies` are in a many-to-many relationship and they're joined by `characters`. These tables have associated classes in our Rails app in the `app/models/` folder, and the classes are named `Actor`, `Movie`, and `Character`. 

If we recall by looking at **/rails/db**, our visual database browser, and navigating to the `characters` table, then we see there is a `movie_id` and `actor_id`. 

So first I got the current actor ID because we are on the page of `@the_actor`:

```html
<% a_id = @the_actor.id %>`
```

which is just a column like any other column, so I get this accessor method `.id`. Then I looked at the records in the `characters` table with a matching `actor_id`:

```html
<% matching_characters = Character.where({ :actor_id => a_id }) %>
```

Now I have an `ActiveRecord::Relation` of characters, and each of these have a `movie_id`. Then I'm going to do a `.each` on the `matching_characters`, and for each of these rows, put it in a block variable `a_character`, pull out the `movie_id` from the row, and look up this movie in the `movies` table to iteratively fill the table with movie information, like `the_movie.title`, in my loop:

```html
<% matching_characters.each do |a_character| %>
    <% m_id = a_character.movie_id %>

    <% matching_movies = Movie.where({ :id => m_id }) %>

    <% the_movie = matching_movies.at(0) %>

    <tr>
      <td>
        <%= the_movie.title %>
      </td>
```

If we look further down in the filmography section, to show the director of the movie:

```html
<!-- app/views/actor_templates/show.html.erb -->

...

<h2>Filmography</h2>

<table border="1">
  ...
  <td>
    <% d_id = the_movie.director_id %>
    
    <% matching_directors = Director.where({ :id => d_id }) %>
    
    <% the_director = matching_directors.at(0) %>
    <%= the_director.name %>
  </td>
  ...
</table>
```
{: mark_lines="10-15"}

I need to use the `director_id` column from my current movie:

```html
<% d_id = the_movie.director_id %>
```

and look that director up in the `directors` table:

```html
<% matching_directors = Director.where({ :id => d_id }) %>

<% the_director = matching_directors.at(0) %>
```

then call `.name` on the row to get my table value:

```html
<%= the_director.name %>
```

We're jumping through all four tables here! `Actor` to `Character`, `Character` to `Movie`, and `Movie` to `Director`!

That's how pretty much all database relationships work. If we can do this, we can do anything.



### Text Companion: Actor Details Filmography

## Video Segment: Defining Instance Methods in the Model

- Notes:

  - time stamp 00:15:31 to 00:22:09
  - define `title_with_year` in `app/models/movie.rb`
  - see [Refactoring MSM Queries with Methods][Refactoring MSM Queries with Methods] section "Instance method review"
  - use of `self.` in model method
  - apply new method to `app/views/movie_templates/show.html.erb`

Let's look at some techniques that we use to make this much easier on ourselves and more efficient for our teams.

Let's take the `Movie` class. All we do when we want to start using `ActiveRecord`, is we create the model. We put it in the `app/models/` folder, named after the table singular `movie.rb`, define the class there inheriting from `ApplicationRecord`, and then boom, magically, we get a whole bunch of methods. 

And this is still `app/models/movie.rb` file is still empty.

But, the power of *object oriented programming*, which is what Ruby is, is that we can add our own methods to this class and encapsulate frequently used logic in a nicely named method. So we don't have to keep doing it over and over again. 

For example, let's just say in the movie details view template page: 

```html
<!-- app/views/movie_templates/show.html.erb -->

<h1>
  Movie #<%= @the_movie.id %> details
</h1>

<a href="/movies">
  Go back
</a>
...
```
{: mark_lines="4"}

Right now I have the movie ID number in the page heading. Let's say I want to replace that with the movie title, and next to it I want the year it was released in parantheses:

```html
<!-- app/views/movie_templates/show.html.erb -->

<h1>
  <%= @the_movie.name %> (<%= @the_movie.year %>)
</h1>

<a href="/movies">
  Go back
</a>
...
```
{: mark_lines="4"}

That works if you visit a given movie details page like **/movies/1**. And I could repeat this pattern all over the place. But that's not great. What if I just want to have that string pre-assembled? In our `rails console` that we opened previously using string interpolation:

```ruby
pry(main)> "#{x.title} (#{x.year})"
=> "The Shawshank Redemption (1994)"
```

I can create a method in my model! Let's create this:

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
  def title_with_year
    return "howdy!"
  end
end
```
{: mark_lines="16-18"}

**BENP: have we ever up to this point seen a function with a `return` statement?**

Note the `# == Schema Information` in the header of this file. This is the same as the "Schema" tab that we say previously on **/rails/db**, and it serves as a nice reference for what is contained in the table `movies` associated with the file `movie.rb`, and the `Movie` class contained therein. 

Now in our view template we can say:

```html
<!-- app/views/movie_templates/show.html.erb -->

<h1>
  <%= @the_movie.title_with_year %>
</h1>

<a href="/movies">
  Go back
</a>
...
```
{: mark_lines="4"}

And if you reload the browser page with your movie details, you will see "howdy!" at the top. The point is, you can define whatever method you want in the model file. And then you can call those methods on any movie wherever you have that movie object. So now I can do something better, like:

```ruby
# app/models/movie.rb

...
  def title_with_year
    return "#{self.title} (#{self.year})"
  end
...
```
{: mark_lines="5"}

We get the title and year from whichever movie this method is being run on, and that is what the keyword `self.` is for. When you're defining an instance method, and you need to call some other instance method, in order to make this instance method work, the `self.` keyword gives us a way to call the other instance method within the definition of this instance method. 

**BENP: this is somewhat confusing wording. needs to be stated clearly and maybe linked to previous material. Right now there is a very long section called [Instance method review][Instance method review] in [Refactoring MSM Queries with Methods][Refactoring MSM Queries with Methods] that goes into this.**

Try to reload the movie details page at **/movies/1**. You should see the title and year instead of "howdy!".

So now I have this method that my whole team can use for the next ten years, saving us from tons of duplication and potential bugs!



### Text Companion: Defining Instance Methods in the Model

## Video Segment: `Movie#director`

- Notes:

  - time stamp 00:22:09 to 00:29:19
  - define `director` in `app/models/movie.rb` to get rid of query in view templates and replace with `@the_movie.director`
  - apply new method to `app/views/movie_templates/show.html.erb`
  - 1-N association

Let's define a really handy one now. Currently, if I want to get the director in the **/movies/1** page, I need to do something like:

```html
<!-- app/views/movie_templates/show.html.erb -->

<h1>
  <%= @the_movie.title_with_year %>
</h1>

<% d_id = @the_movie.director_id %>
<% matching = Director.where({ :id => d_id }) %>
<% d = matching.at(0) %>
<h1>
  Directed by <%= d.name %>
</h1>

<a href="/movies">
  Go back
</a>
...
```
{: mark_lines="7-12"}

I need to use the column accessor method to get the ID number of the director, then I need to store it, then I need to look up the director by searching within the ID column, then I store that, then I get the first element, and finally I have the director record which I can call the name on and place in an HTML tag. This should all work and we can now see the director on the page.

Sure this works, but it's pretty annoying. What if I just had a method I could call that looked like `@the_movie.director`, which just returns the director record (`d` above), and I can avoid several lines of embedded code?

Let's do it. 

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  def title_with_year
    return "#{self.title} (#{self.year})"
  end

  def director
    the_director = Director.where({ :id => self.director_id }).at(0)
    return the_director
  end
end
```
{: mark_lines="9-12"}

Again, we are using `self.` to get the `director_id` of the object that this method is called on, which is an instance of the `Movie` object (`@the_movie` on our view template page). Then we look up this ID in the `directors` table in the `id` column using the `Director` model that we defined. And now we can just return this single record! 

So now in our view template, we can replace the previous multiline code with:

```html
<!-- app/views/movie_templates/show.html.erb -->

<h1>
  <%= @the_movie.title_with_year %>
</h1>

<h1>
  Directed by <%= @the_movie.director.name %>
</h1>

<a href="/movies">
  Go back
</a>
...
```
{: mark_lines="8"}

We get our `@the_movie.director` object, which is a whole row of the `directors` table, and we can get the `name` using our attribute accessor method for that object. We could even do `@the_movie.director.dob` or `@the_movie.director.bio` to get other information about the director in that row. 

Reload **/movies/1** and you will see the intended result! 

Our new instance method encapsulates the *one-to-many* association between `movies` and `directors`, and we (and our team) can use it anywhere. It dramatically simplifies our work. If you take the time, especially for these one-to-many and many-to-many associations, which we work with a lot, and define a method, then it makes other things much easier.



### Text Companion: `Movie#director`

## Video Segment: `Director#filmography`

- Notes:

  - time stamp 00:29:19 to 00:33:34
  - other side of 1-N association
  - define `filmography` in `app/models/director.rb` to get rid of query in view templates and replace with `@the_director.filmography`
  - apply new method to `app/views/director_templates/show.html.erb`

We make these associations a lot, so it's convention after we have our models in our Rails app, to encapsulate them in instance methods immediately. And we call the method the singular of the other table like `def director`, if it's the one-side of a one-to-many relationship.

Of course there's another side of this one-to-many relationship: a director can have many movies. 

On my director details view template in the filmography section, I will find a bit of code like:

```html
<!-- app/views/director_templates/show.html.erb -->

...
  <% the_id = @the_director.id %>
  <% matching_movies = Movie.where({ :director_id => the_id }) %>
  
  <% films = matching_movies.order({ :year => :asc }) %>
  <% films.each do |a_movie| %>
...
```

This is a similar but inverse procedure from before. Before, we started with the foreign key and looked up the primary key, and here it is the opposite. We start with the record `@the_director`, get the primary key `id` of that, look up this primary key in the foreign key column of `movies`, and then loop through the resulting records in `matching_movies`. In this case, we also sorted the resulting records into chronologically ascending order with the `year` column prior to looping.

What we want instead here is a method that looks like: `@the_director.filmography`, that will give us back the `matching_movies` variable, and avoid all these lines of code.

Well, let's now go into our `director.rb` model and code in this method:

```ruby
# app/models/director.rb

...
class Director < ApplicationRecord
  def filmography
    the_films = Movie.where({ :director_id => self.id }).order({ :year => :asc })
    return the_films
  end
end
```
{: mark_lines="5-8"}

Again, we see the opposite logic from last time when we wanted the director of a movie. Here we have the primary key from the director (`self.id`), and we want to look up all similar ids in the foreign key of the `movies` table. Again, we are chaining an `.order` method here, so the returned records are chronologically ordered for our looping step.

Armed with this new method we can replace the all the previous code in our view template with just one line:

```html
<!-- app/views/director_templates/show.html.erb -->

...
  <% @the_director.filmography.each do |a_movie| %>
...
```



### Text Companion: `Director#filmography`

## Video Segment: Additional Association Accessor Methods

- Notes:

  - time stamp 00:33:34 to 00:59:46
  - work independently to define additional 1-N associations

**BENP: recording is just class working independently for most of this time**

All of this is what we call *association accessor methods*, and we do it at the beginning of every project. The first step is we create our data model, we figure out our columns, our tables, our one-to-manys and our many-to-manys. Then, as soon as we start writing code, as soon as we create our model files, we first write these methods on both sides of the relationship that need them to make querying much easier.

We have some other association accessor methods that we need to define our current data model. There are three 1-N associations::

```ruby
# Director => Movie
# Movie => Character
# Actor => Character
```

You should try to define the six methods needed:

```ruby
# Director#filmography (we did this!)
# Movie#director (and this!)
# Movie#characters
# Character#movie
# Actor#characters
# Character#actor
```

Defining these last four is your job. Try and do this on your own based on the two sides of the 1-N that we defined, and run `rails grade` and **/git** commit as you get things working!

Keep in mind there is some reference (written notes) for this project [here](https://chapters.firstdraft.com/chapters/843){:target="_blank"}, including a section [reviewing instance methods](https://chapters.firstdraft.com/chapters/843#instance-method-review){:target="_blank"}.

### Text Companion: Additional Association Accessor Methods

## Video Segment: Additional Association Accessor Methods Solved

- Notes:

  - time stamp 00:59:46 to 01:05:57
  - finish 1-N association accessor methods in the models

First, we can solve the 1-N relationship for movies to characters:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  def title_with_year
    return "#{self.title} (#{self.year})"
  end

  def director
    the_director = Director.where({ :id => self.director_id }).at(0)
    return the_director
  end

  def characters
    the_characters = Character.where({ :movie_id => self.id })
    return the_characters
  end
end
```
{: mark_lines="14-17"}

By convention we define the method as `characters` (the name of what we want plural), unless we have a better, more descriptive name in mind (like when we used `filmography`). I am filtering the `characters` table above by the primary key of the currenty movie, in the foreign key column of that table. We get back potentially multiple rows, so we don't need a `.at(0)`.

On the other side of this relationship in `character.rb`, we can do:

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  def movie
    return Movie.where({ :id => self.movie_id }).at(0)
  end
end
```
{: mark_lines="5-7"}

And now we go to the `movies` table with our foreign key from the current character, and filter the primary keys to get the one movie that matches with `.at(0)`.

And now for the last 1-N, we start with the many characters that can be associated to one actor:

```ruby
# app/models/actor.rb

...
class Actor < ApplicationRecord
  def characters
    return Character.where({ :actor_id => self.id })
  end
end
```
{: mark_lines="5-7"}

And back in our `character.rb`, the one actor associated with a given character:

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  def movie
    return Movie.where({ :id => self.movie_id }).at(0)
  end

  def actor
    return Actor.where({ :id => self.actor_id }).at(0)
  end
end
```
{: mark_lines="9-11"}

Are you seeing the patterns and similarities? In many cases we can just copy-paste and change the name of the table!



### Text Companion: Additional Association Accessor Methods Solved

## Video Segment: Applying Association Accessor Methods

- Notes:

  - time stamp 01:05:57 to 01:12:15
  - replace all DB queries with 1-N association accessor methods in the view templates


Any place where we have a database query in one of the 1-N associations, we want to replace it.

Let's begin by going to the director details view template and replacing this:

```html
<!-- app/views/director_templates/show.html.erb -->

...
  <% the_id = @the_director.id %>
  <% matching_movies = Movie.where({ :director_id => the_id }) %>
  
  <% films = matching_movies.order({ :year => :asc }) %>
  <% films.each do |a_movie| %>
...
```

with:

```html
<!-- app/views/director_templates/show.html.erb -->

...
  <% @the_director.filmography.each do |a_movie| %>
...
```

if you haven't already.

Let's go to the movie index view template and replace this:

```html
<!-- app/views/movie_templates/index.html.erb -->

...
      <% matching_directors = Director.where({ :id => a_movie.director_id }) %>
          
      <% the_director = matching_directors.at(0) %>

      <%= the_director.name %>
...
```

with:

```html
<!-- app/views/movie_templates/index.html.erb -->

...
      <%= a_movie.director.name %>
...
```

Let's go to the movie details view template and replace this:

```html
<!-- app/views/movie_templates/show.html.erb -->

...
    <% matching_directors = Director.where({ :id => @the_movie.director_id }) %>
      
    <% the_director = matching_directors.at(0) %>
    
    <%= the_director.name %>
...
```

with:

```html
<!-- app/views/movie_templates/show.html.erb -->

...
    <%= @the_movie.director.name %>
...
```

And now on the actor details page, replace this:

```html
<!-- app/views/actor_templates/show.html.erb -->

...
  <% a_id = @the_actor.id %>

  <% matching_characters = Character.where({ :actor_id => a_id }) %>
  
  <% matching_characters.each do |a_character| %>
  
    <% m_id = a_character.movie_id %>
    
    <% matching_movies = Movie.where({ :id => m_id }) %>
    
    <% the_movie = matching_movies.at(0) %>
...
```

with:

```html
<!-- app/views/actor_templates/show.html.erb -->

...
  <% @the_actor.characters.each do |a_character| %>
     
    <% the_movie = a_character.movie %>
...
```

And below this in the same file replace:

```html
<!-- app/views/actor_templates/show.html.erb -->

...
        <% d_id = the_movie.director_id %>
        
        <% matching_directors = Director.where({ :id => d_id }) %>
        
        <% the_director = matching_directors.at(0) %>
        
        <%= the_director.name %>
...
```

with:

```html
<!-- app/views/actor_templates/show.html.erb -->

...
        <%= the_movie.director.name %>
...
```

This became dramatically simpler here. We have these methods to traverse through all of our tables. 

Let's make sure this all works by manually visiting the pages and checking, and then running our automated tests with `rails grade` to insure that our *refactoring* did not break anything and introduce *regressions*.

We didn't gain any new superpowers as far as new features that we're able to build. But our code base is so much more maintainable now. It's going to be so much easier for us to build new features now that we have these *association accessor methods*.

### Text Companion: Applying Association Accessor Methods

## Finish and Submit Refactoring MSM Queries

---
