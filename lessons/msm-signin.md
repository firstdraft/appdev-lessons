# Must See Movies Signin

- Notes:

  - [Day 8 long video](https://uchicago.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=0325615f-63d3-473f-be6b-ae4b00eaec85){target="_blank"} transcription copied below is in [here](https://github.com/firstdraft/appdev-chapters/blob/benp-edits/MSM-signin.md){target="_blank"}

  - Project (graded): [https://github.com/appdev-projects/msm-signin](https://github.com/appdev-projects/msm-signin){target="_blank"}

  - Target: [https://msm-signin.matchthetarget.com/](https://msm-signin.matchthetarget.com/){target="_blank"}

  - Useful chapters:
    - [draft:resource generator][draft:resource generator]
    - [draft:account generator][draft:account generator]

**BENP: There is a lot of draft generator stuff at the beginning. This is applied examples, so it *is* transcribed. There is still a need for bite-size draft gen videos from thus far un-transcribed content.**

**BENP: the README was zipped in here, as it naturally came up throughout the video**

**BENP: MSM should be written out when possible (similar to RPS)**


## Video Segment: Exploring the Target

- Notes:

  - time stamp 00:01:08 to 00:03:07
  - show off signin, out, up, and **/bookmarks** in the [target](https://msm-signin.matchthetarget.com)

This version of MSM - Must See Movies **BENP: this is like the first time this acronym was said maybe?**, is the final form of our app.

Instead of just a directory of movies like IMDB, in this version we can sign up for an account. In the [target](https://msm-signin.matchthetarget.com){target="_blank"}, visit the **/user_sign_up** URL (or click the navbar link), and try to create an account with a random email ("alice@example.com"), a first ("Alice") and last ("Smith") name, and a password ("password").

After you signup, you should be redirected to the homepage with a notice of "User account created successfully" at the top of the page. And now, when we browse around to a given movie details page like **/movies/1**, the key difference we note is that there is now a "Bookmark this movie!" button. If we click this button as our user "Alice", then we are brought to the URL path **/bookmarks**, showing *only* Alice's personal bookmarked movies.

We have all the tools we need to build this application: HTML, Ruby, RCAV, `params`, forms, databases, and now, finally cookies for signin and signout! Photogram Signin is actually very similar to this project. But today we're going to see some shortcuts that will speed up our development by automating some boilerplate code.



### Text Companion: Exploring the Target

## Video Segment: Creating `movies` with `generate model`

- Notes:

  - time stamp 00:03:07 to 00:06:27
  - run `rails generate model movie` in our blank app
  - explore file in `db/migrate/`
  - run `rails db:migrate`
  - visit **/rails/db**

If we navigate to our new app, we will see it is totally empty right now:

```ruby
# config/routes.rb

Rails.application.routes.draw do

end
```

This is a brand-new Rails app. No routes, no models, no controllers, no views. We don't even have a database prepared.

To begin from scratch, with our target in mind, step one is to figure out the data model. That means domain modeling by making sketches. But assuming that we already did that and we have a list of our tables and columns, then the first step is to create our tables.

Let's create our tables one-by-one: `movies`, `directors`, `actors`, and `characters`. For this, we will use `draft` at the command-line. So go to your GitPod workspace, and open a fresh terminal window to work in. 

To create a table for `movies`, the command is:

```
rails generate model movie title:string description:text director_id:integer
```

The command is `rails generate model`, the fourth input on the line (first input to the command) is the name of the table we want (singular, `movie`). Following this are the names of the columns we want (e.g., `title`), followed by their datatype (e.g., `:string`).

When we enter that command, the output will look like:

```
Running via Spring preloader in process 1714
    invoke  active_record
    create    db/migrate/[TIME OF CREATE]_create_movies.rb
    create    app/models/movie.rb
```

Rails created two files here, `db/migrate/[TIME OF CREATE]_create_movies.rb` and `app/models/movie.rb`. The first `db/migrate/` file is a Ruby class that, when executed, will issue the SQL to the database to actually create the table. Let's have a look at that file:

```ruby
# db/migrate/[TIME OF CREATE]_create_movies.rb

class CreateMovies < ActiveRecord::Migration[6.0]
  def change
    create_table :movies do |t|
      t.string :title
      t.text :description
      t.integer :director_id

      t.timestamps
    end
  end
end
```

This class inherits from methods from `ActiveRecord::Migration`, like `create_table`. If we instantiate this class `CreateMovies` and call its method `change`, then it creates this table with those listed columns. If we forgot anyting from our terminal command, we can add it directly to this file, like adding a column or some default values to a column:

```ruby
# db/migrate/[TIME OF CREATE]_create_movies.rb

class CreateMovies < ActiveRecord::Migration[6.0]
  def change
    create_table :movies do |t|
      t.string :title, :default => "Some title"
      t.text :description
      t.integer :director_id
      t.string :image_url

      t.timestamps
    end
  end
end
```
{: mark_lines="6 9"}

In this case, a default on the `title` column doesn't make much sense. Numerical columns are often where we put default values of "0", so that `nil` doesn't mess with any mathematical operations. 

If we feel good about the migration, then we can go back to the terminal and run it with:

```
rails db:migrate
```

This command will go into `db/migrate/`, look for any of the classes that haven't already been run, instantiate them, and call their method. The output of the command looks like

```
== [TIME OF CREATE] CreateMovies: migrating =====================
-- create_table(:movies)
   -> 0.0019s
== [TIME OF CREATE] CreateMovies: migrated (0.0024s) ============

Annotated (1): app/models/movie.rb
```

We can now visit **/rails/db** in our app browser, and we will see this `movies` table with our specified columns.



### Text Companion: Creating `movies` with `generate model`

## Video Segment: Creating `movies` with `generate draft:resource`

- Notes:

  - time stamp 00:06:27 to 00:24:23
  - run `rails db:rollback` then `rails generate draft:resource movie`
  - explore `config/routes.rb` to view CRUD routes
  - explore `app/controllers/movies_controller.rb` to view CRUD actions
  - explore generated view templates
  - run `rails db:migrate`
  - aside into `schema.rb` and migration versioning

This is a quick way to generate our tables. And what would be the next step? We would probably start building out the RCAVs for our movie pages, like the standard index (**/movies**) and show pages (e.g., **/movies/1**) and *all* of the routes, actions, and view templates associated with them, not to mention the create, update, and destroy actions. That's straightforward, but it is quite a bit of work to type out all of this, and we've done it so many times already! 

**BENP: at this point in video, there is a long RCAV dance to get movies index and show pages going. Not including this in transcript, very boilerplate stuff just to make the point that this is tedious.**

Well, let's see another way. Back at the terminal, try:

```
rails db:rollback
```

This command is going to undo all of the work we just did to get our `movies` table in the database. This is the opposite of `db:migrate`, it undoes the *most recent* migration. If we look back in **/rails/db**, we'll see the table is gone. If you made progress on any of the RCAVs for the movie CRUDing, then you can "discard changes" on the **/git** tab. Now we are back to square one.

Instead of `rails generate model`, there's another generator that we want to use:

```
rails generate draft:resource movie title:string description:text director_id:integer
```

The command is `rails generate draft:resource`. The other command-line inputs are the same as before. This, and many other generators prepared for this course, are available as an open-soruce gem on GitHub at [https://github.com/firstdraft/draft_generators](https://github.com/firstdraft/draft_generators){target="_blank"}. 

Now, when we enter that command, the output will look like:

```
Running via Spring preloader in process 2681
    create  app/controllers/movies_controller.rb
    invoke  active_record
    create    db/migrate/[TIME OF CREATE]_create_movies.rb
    create    app/models/movie.rb
    create  app/views/movies
    create  app/views/movies/index.html.erb
    create  app/views/movies/show.html.erb
     route  RESTful routes
    insert config/routes.rb
```

Wow! It did a bunch of stuff. It `create`d files for me, and it `insert`ed a bunch of routes into my `config/routes.rb` file:

```ruby
# config/routes.rb

Rails.application.routes.draw do

  # Routes for the Movie resource:

  # CREATE
  post("/insert_movie", { :controller => "movies", :action => "create" })

  # READ
  get("/movies", { :controller => "movies", :action => "index" })

  get("/movies/:path_id", { :controller => "movies", :action => "show" })

  # UPDATE

  post("/modify_movie/:path_id", { :controller => "movies", :action => "update" })

  # DELETE
  get("/delete_movie/:path_id", { :controller => "movies", :action => "destroy" })

  #------------------------------

end
```

This file was empty before. These are exactly the five routes that we need to CRUD `movies`. Most of the time, we are going to want these routes for our tables. And this is all going to look very similar between tables (e.g., just replace `movie` with `director` above). We may decide to remove some routes if it doesn't make sense to have them (e.g., a details page for a comment), but we can do that manually after they are generated. All of the *conventions* that we have seen for naming routes, controllers, and actions have been used. We can change the code however we want after the fact. It is all *very* formulaic.

In addition to these routes, the generator also made the `app/controllers/movies_controller.rb` controller file, and fills it in with the actions:

```ruby
# app/controllers/movies_controller.rb

class MoviesController < ApplicationController
  def index
    matching_movies = Movie.all

    @list_of_movies = matching_movies.order({ :created_at => :desc })

    render({ :template => "movies/index.html.erb" })
  end

  def show
    ...
  end

  def create
   ...
  end

  def update
    ...
  end

  def destroy
    ...
  end
end
```

These actions are almost always the same between tables, so it is again *very* formulaic, and can easily be automated. Of course, we may need to modify all of this code to suit our purposes, but the boilerplate is there for us. 

Similar to the above examples, we can also see there are view templates for `views/movies/index.html.erb` and `views/movies/show.html.erb` generated for free! There are even forms there.

To actually get this `movies` table in our database, we still need to go to the terminal and run:

```
rails db:migrate
```

That will run any unrun `db/migrate/` files. If you haven't run `rails db:migrate` yet (you have pending migration files), then Rails will throw a "Migrations are pending" error when you try to visit your app browser.

Now we can go to our app browser and manually navigate to **/movies**. We see that we can add a movie with the form here, and once on the details page, there is a form to edit the movie and a "Delete movie" link. All of this works, try it out. CRUD!

**BENP: based on student Q there is a diversion to the `schema.rb` file to show migration versioning. I'm not transcribing this, hard to see where it fits in, maybe too much aside here. The student followup Q also leads you to show deleting migration files, or dropping tables. Showing `rails db:drop` (risky). 00:20:30 to 00:23:53**

This shortcut gets us up and running fast, but when you use it, you *own that code*, and need to be prepared to modify it accordingly. Likely, it won't be exactly what you want.



### Text Companion: Creating `movies` with `generate draft:resource`

## Video Segment: `generate draft:resource` for Entire Database

- Notes:

  - time stamp 00:24:23 to 00:27:00
  - run `rails db:rollback` then `rails generate draft:resource` and `rails db:migrate` for all tables in database

Let's undo and redo these steps with the proper tables and columns:

```
rails db:rollback
```

This drops our most recent migration of the `movies` table. And we can also "Discard changes" on the **/git** tab.

The proper command we want for all of our tables are:

```
rails generate draft:resource movie title:string year:integer duration:integer director_id:integer description:text image:string
```

Enter this to generate the RCAV and CRUD code, and then run a `rails db:migrate` to create the table and columns in our database. Once you do this, visit the new URL paths in your app browser to see if everything looks okay. If it looks good, then definitely do a **/git** commit, because generators write so much code that if there is a mistake it will be difficult to undo them without the ability to jump back to an earlier snapshot..

Once you've done this, repeat these steps for the other three tables and routes in our database:

```
rails generate draft:resource actor name:string dob:date bio:text image:string
```

Then `rails db:migrate`, check it out, and **/git** commit.

```
rails generate draft:resource director name:string dob:date bio:text image:string
```

Then `rails db:migrate`, check it out, and **/git** commit.

```
rails generate draft:resource character name:string actor_id:integer movie_id:integer
```

Then `rails db:migrate`, check it out, and **/git** commit.

**BENP: at 00:27:00 to 00:29:52 there is another aside into spinning up an app from scratch with base-rails and generators, not transcribing this**



### Text Companion: `generate draft:resource` for Entire Database

## Video Segment: Association Accessor Methods

- Notes:

  - time stamp 00:31:03 to 00:34:40
  - use `belongs_to` and `has_many` on the table models
  - can use https://association-accessors.firstdraft.com

Now that we have all our model files, we should add the association accessor methods for all of our 1-N and N-N relationships. You can use the [association accessors tool](https://association-accessors.firstdraft.com){target="_blank"}, or just type it out if you remember how it works for each of our models, starting with `Movie`:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  belongs_to :director
  has_many :characters
end
```
{: mark_lines="5-6"}

Then `Director`:

```ruby
# app/models/director.rb

...
class Director < ApplicationRecord
  has_many :filmography, :class_name => "Movie"
end
```
{: mark_lines="5"}

Note, that since we didn't give the method for the movies a director is associated with the formulaic name of `movies`, but rather `filmography`, we needed to be explicit about the class name.

Then `Actor`:

```ruby
# app/models/actor.rb

...
class Actor < ApplicationRecord
  has_many :characters
  has_many :filmography, :through => :characters, :source => :movie
end
```
{: mark_lines="5-6"}

**BENP: have `through` and `source` been introduced on video or just in a reading?**

Because we used a method `movie` contained in the `Character` model for the `filmography` method here (it is an indirect N-N association, so we use `has_many` with `through` and `source` **BENP: is that correct, added this note later**), we need to make sure that is also set up:

```ruby
# app/models/character.rb

...
class Character < ApplicationRecord
  belongs_to :movie
  belongs_to :actor
end
```
{: mark_lines="5-6"}

And we can actually go back to `Movie` now, and establish a `cast` method that lists the actors in a movie with this new connection:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  belongs_to :director
  has_many :characters

  has_many :cast, :through => :characters, :source => :actor
end
```
{: mark_lines="8"}

In the above accessors, we are just going straight away into some different Ruby syntaxes than we may be used to. You can re-read [this](https://chapters.firstdraft.com/chapters/787){target="_blank"} for reference. As you go out and begin reading StackOverflow or blog posts to figure things out, you need to be aware of and comfortable with the common syntaxes used.

We should definitely make another **/git** commit now.



### Text Companion: Association Accessor Methods

## Video Segment: Nav Links and `sample_data`

- Notes:

  - time stamp 00:34:40 to 00:37:23
  - add links to `app/views/layouts/application.html.erb`
  - run `sample_data`
  - point out [loading data from a CSV](https://chapters.firstdraft.com/chapters/791) and [adding a `sample_data` rake task](https://chapters.firstdraft.com/chapters/852)

Let's quickly add a navbar so we can click around in our app without manually entering URLs. As usual, this will go in the `app/views/layouts/application.html.erb` file:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    <title>MSM SIGNIN</title>
    <%= csrf_meta_tags %>

    <!-- Expand the number of characters we can use in the document beyond basic ASCII 🎉 -->
    <meta charset="utf-8">

    <!-- Make it responsive to small screens -->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <%= csp_meta_tag %>
    <%= stylesheet_link_tag    'application', media: 'all' %>
  </head>

  <body>
    <ul>
      <li>
        <a href="/movies">Movies</a>
      </li>
      <li>
        <a href="/directors">Directors</a>
      </li>
      <li>
        <a href="/actors">Actors</a>
      </li>
      <li>
        <a href="/characters">Characters</a>
      </li>
    </ul>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="19-32"}

Now that the app is looking good with a navbar, the next step is to run `rails sample_data` to get some random data into MSM. This is just like before. 

But for your own work, you would need to write this `sample_data` script yourself to get test data. There are two chapters to help you with that: [loading data from a CSV](https://chapters.firstdraft.com/chapters/791){target="_blank"} and [adding a `sample_data` rake task](https://chapters.firstdraft.com/chapters/852){target="_blank"}. 

**BENP: this sample_data stuff comes up again later for random user data? or is that in the Bootstrap Task List?**



### Text Companion: Nav Links and `sample_data`

## Video Segment: `validates` and Summarize Startup

- Notes:

  - time stamp 00:37:23 to 00:40:25
  - add `validates :title, :presence => true` to `app/models/movie.rb`
  - summarize starting from scratch steps

To summarize, the standard setup steps when building any app is: first domain modeling, then generating resources once the table names and columns are defined, and then adding associations add validations (we skipped this, but there is a reading [here](https://chapters.firstdraft.com/chapters/845){target="_blank"}).

Let's return to validations, which are ways of checking that only "good" data is entered into our database. We can add a validation to the `Movie` class:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  validates :title, :presence => true

  belongs_to :director
  has_many :characters

  has_many :cast, :through => :characters, :source => :actor
end
```
{: mark_lines="5"}

This added code is saying that a movie *must* have a title, or it will not be added to the database. The SQL will not be issued by `.save` on a `Movie` instance without a value in this column. (Recall that errors on a given instance of a class can be accessed with the method `.errors` or `.errors.full_messages` to get any array of strings for printing and showing the user.) 

It is up to you to put boundaries on your data using `validates`, but it is generally a very good idea to do so frequently to keep your database in good shape.

Back to the summary:

 - we domain modelled,
 - generated resources, 
 - added association accessors, 
 - added validations, 
 - wrote and ran a `sample_data` task
 - and gave ourselves a navbar. 
 
These are standard steps we do for all of our projects!

Once you have them all done, be sure to **/git** commit.



### Text Companion: `validates` and Summarize Startup

## Video Segment: `generate draft:account`

- Notes:

  - time stamp 00:47:13 to 01:02:15
  - getting `users` table with `draft:account`
  - explore new CRUD routes, models, and actions

Let's talk about the next table, `users`. In our [target](https://msm-signin.matchthetarget.com){target="_blank"}, the new functionality is that a signed in user can bookmark movies, so we need accounts, and we're going to need a `bookmarks` table.

We can model this in firstdraft and then use co-pilot to get the generator code. **BENP: from 00:47:40 to 00: there is a brief show-and-tell of domain modeling in firstdraft with a users table and bookmarks table and then using co-pilot to get the command line code. There is also an aside into trying to generate the users with draft:resource and why that doesn't work. Not transcribing this, because it is very visual.**

Our `users` table is not going to have the typical CRUD RCAVs that our other tables did, so `draft:resource` is not going to work. We probably don't want to show a list of all users, nor do we want a link to "Delete user" (rather a signout), and we also want password encryption handling, just to name a few differences to our other database tables. 

Because this is so different (but still formulaic between apps), there is a very specific command-line tool for this `users` table:

```
rails generate draft:account user first_name:string last_name:string
```

The new tool is `draft:account`. The arguments are the table name and the columns we want, *excluding* email and password, which will automatically be added as `username` and the encrypted `password_digest` column, respectively. 

What did running that tool do in our routes?

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get("/", { :controller => "movies", :action => "index" })

  # Routes for the User account:

  # SIGN UP FORM
  get("/user_sign_up", { :controller => "user_authentication", :action => "sign_up_form" })
  # CREATE RECORD
  post("/insert_user", { :controller => "user_authentication", :action => "create" })

  # EDIT PROFILE FORM
  get("/edit_user_profile", { :controller => "user_authentication", :action => "edit_profile_form" })
  # UPDATE RECORD
  post("/modify_user", { :controller => "user_authentication", :action => "update" })

  # DELETE RECORD
  get("/cancel_user_account", { :controller => "user_authentication", :action => "destroy" })

  # ------------------------------

  # SIGN IN FORM
  get("/user_sign_in", { :controller => "user_authentication", :action => "sign_in_form" })
  # AUTHENTICATE AND STORE COOKIE
  post("/user_verify_credentials", { :controller => "user_authentication", :action => "create_cookie" })

  # SIGN OUT
  get("/user_sign_out", { :controller => "user_authentication", :action => "destroy_cookies" })
  
  ...

end
```
{: mark_lines="4"}

(We added the **/** route above, so the new signup route will have somewhere built to redirect to.)

This tool added all of the signup, signin, signout stuff that we needed for our user accounts! This is what you wrote by hand for the final Photogram project. The tool also generated all of the controllers and view templates associated with these routes.

If we now `rails db:migrate`, all of the routes will work! For instance, try out the URL path **/user_sign_up** to make a new account. Boom! You can go look at **/rails/db** and you will see the new `users` table with the account you added and an encrypted password in the "Password digest" column.

We can look at the new model as well:

```ruby
# app/models/user.rb

...
class User < ApplicationRecord
  validates :email, :uniqueness => { :case_sensitive => false }
  validates :email, :presence => true
  has_secure_password
end
```

And we see that validations have been added, and the `has_secure_password` method from the `bcrypt` gem is also there. That gives us the `.password` and `.password_confirmation` method that we would find in our `create` action in the controller:

```ruby
# app/controllers/user_authentication_controller.rb

class UserAuthenticationController < ApplicationController
  ...
  def create
    @user = User.new
    @user.email = params.fetch("query_email")
    @user.password = params.fetch("query_password")
    @user.password_confirmation = params.fetch("query_password_confirmation")
    @user.first_name = params.fetch("query_first_name")
    @user.last_name = params.fetch("query_last_name")

    save_status = @user.save

    if save_status == true
      session[:user_id] = @user.id
   
      redirect_to("/", { :notice => "User account created successfully."})
    else
      redirect_to("/user_sign_up", { :alert => @user.errors.full_messages.to_sentence })
    end
  end
...
end
```
{: mark_lines="8-9 15"}

Nice! All of the stuff you did in the Photogram Signin homework is automated now. We also see that the generator is placing the user ID into the cookies, so that we can tailor the app experience for the signed in user: `session[:user_id] = @user.id`.

Again, you need to *own the code* that was generated so that you can modify things, but it's a major shortcut. If you want to change things, remember to use "Inspect" in your browser to find the routes you want to modify. You can also use the server log in the GitPod terminal running `bin/server` to figure out what you want to change and where in the code it is.



### Text Companion: `generate draft:account`

## Video Segment: Conditional Links, Alerts, and Notices

- Notes:

  - time stamp 01:02:15 to 01:10:40
  - control flow showing of links in `app/views/layouts/application.html.erb` using `if session.fetch(:user_id) == nil`
  - explore `:alert` and `:notice` in `app/controllers/movies_controller.rb`
  - add alerts and notices to application layout

Now that our account pages are ready, we can again add some links to the navbar to avoid all the manual entering of URLs:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <ul>
      <li>
        <a href="/movies">Movies</a>
      </li>
      <li>
        <a href="/directors">Directors</a>
      </li>
      <li>
        <a href="/actors">Actors</a>
      </li>
      <li>
        <a href="/characters">Characters</a>
      </li>

      <li>
        <a href="/user_sign_up">Sign up</a>
      </li>
      <li>
        <a href="/user_sign_in">Sign in</a>
      </li>
      <li>
        <a href="/user_sign_out">Sign out</a>
      </li>
    </ul>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="24-32"}

However, we want these links accessible only under certain *conditions* depending on the status of a visitor. We can use the cookies, which our generator put in the `session` hash, to do this:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <ul>
      <li>
        <a href="/movies">Movies</a>
      </li>
      <li>
        <a href="/directors">Directors</a>
      </li>
      <li>
        <a href="/actors">Actors</a>
      </li>
      <li>
        <a href="/characters">Characters</a>
      </li>

      <% if session.fetch(:user_id) == nil %>
        <li>
          <a href="/user_sign_up">Sign up</a>
        </li>
        <li>
          <a href="/user_sign_in">Sign in</a>
        </li>
      <% else %>
        <li>
          <a href="/user_sign_out">Sign out</a>
        </li>
      <% end %>
    </ul>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="24-35"}

**BENP: this is being presented as new here, but it was shown before (or is that just in the homework Photogram Signin?)**

Right now, it's difficult to tell what is happening when we signin, signout, create a record, etc. We would like some kind of notifications to alert the user to the success or failure of various clicks. We don't want to do this with a bunch of new view templates, because we are using `redirect_to` for a lot of these clicks.

If we look in a given action (like `update` for our `movies` table), we will see a tool for showing these notices and alerts:

```ruby
# app/controllers/movies_controller.rb

class MoviesController < ApplicationController
  ...
  def update
    the_id = params.fetch("path_id")
    the_movie = Movie.where({ :id => the_id }).at(0)

    the_movie.title = params.fetch("query_title")
    the_movie.year = params.fetch("query_year")
    the_movie.duration = params.fetch("query_duration")
    the_movie.director_id = params.fetch("query_director_id")
    the_movie.description = params.fetch("query_description")
    the_movie.image = params.fetch("query_image")

    if the_movie.valid?
      the_movie.save
      redirect_to("/movies/#{the_movie.id}", { :notice => "Movie updated successfully."} )
    else
      redirect_to("/movies/#{the_movie.id}", { :alert => the_movie.errors.full_messages.to_sentence })
    end
  end
...
end
```
{: mark_lines="18 20"}

When a movie is successfully updated and saved (because it was deemed `valid`, another new method), then the `redirect_to` has a second hash argument with a `notice` and a message. On the other hand, if the new movie is invalid and not saved, the second hash argument to `redirect_to` contains an `alert` and a message. This `alert` message is coming from the `Movie` object that we are trying to save, which is called `the_movie`, and the method to get the error message is `.errors`. We make the message look nicer for printing in the browser as well with `.full_messages.to_sentence`.

Now, where should those alerts go? We could put them directly on the view template page. Better yet, we can put them in the layout file so they appear on every page when they exist!

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <ul>
      <li>
        <a href="/movies">Movies</a>
      </li>
      <li>
        <a href="/directors">Directors</a>
      </li>
      <li>
        <a href="/actors">Actors</a>
      </li>
      <li>
        <a href="/characters">Characters</a>
      </li>

      <% if session.fetch(:user_id) == nil %>
        <li>
          <a href="/user_sign_up">Sign up</a>
        </li>
        <li>
          <a href="/user_sign_in">Sign in</a>
        </li>
      <% else %>
        <li>
          <a href="/user_sign_out">Sign out</a>
        </li>
      <% end %>
    </ul>

    <p style="color: green"><%= notice %></p>

    <p style="color: red"><%= alert %></p>

    <%= yield %>
  </body>
</html>
```
{: mark_lines="38 40"}

Our helper variables `notice` and `alert` (that we defined in the `redirect_to` hash argument), are also styled here with a green and red color, respectively. Now they will be on any page and we don't need to copy-paste that code onto all our view templates where we might need them.

Once you get all of this together, it's a good time to **/git** commit.



### Text Companion: Conditional Links, Alerts, and Notices

## Video Segment: Bookmark

- Notes:

  - time stamp 01:10:40 to 01:28:20
  - run `rails generate draft:resource bookmark`
  - tailoring user experience by allowing them to add records to a join table
  - create `action="/insert_bookmark"` form in `app/views/movies/show.html.erb`
  - use the provided CRUD action, changing parameter names to matchup

We also need to make sure that we have the user bookmarks join table in our app. We can do that by running our familiar `draft:resource` generator:

```
rails generate draft:resource bookmark user_id:integer movie_id:integer
```

Then executing a `rails db:migrate` to get the table in our database. 

You should also re-run `rails sample_data` as this point, because it will also create some users and bookmark data. Now the trick is going to be getting a "Bookmark this movie!" button on the movie details pages, and getting a list of personalized bookmarks to show to the signed in user.

Before we proceed, we can ask `rails grade` for the specific requirements for the project to see what's left to do. There's still a lot of work left to be done on the bookmarks!

We will walk through this process, because it's important. If you can do this, you can build just about any app with user accounts and a tailored CRUD experience. The steps are always the same: 

  - A user signs in
  - They create stuff, often by creating a record in a join table to connect themselves to another entity
    - This can be liking a photo, bidding on an item, commenting on something 
  - We give the user the ability to un-join from the entity (destroy the join table record)

So how do we do this? 

Let's identify what CRUD actions are happening in the database when a user clicks the "Bookmark this movie!" button in our [target](https://msm-signin.matchthetarget.com){target="_blank"}. In this case, a record is being created in the `bookmarks` table that has a value for the signed in user's ID and for the movie's ID, which we called `user_id` and `movie_id`.

Even though there's nothing for the user to fill out, since we are creating a record, we will use a form in our movie details view template for this:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>
    
    <form action="/">
      <input type="text">

      <input type="text">
      
      <button>Bookmark this movie!</button>
    </form>
  ...
  </div>
</div>
...
```
{: mark_lines="9-15"}

The boilerplate for this form would work if we had the user's type into the first input box a valid user ID and the second input box a valid movie ID, then have the action take those IDs and add them as a record in `bookmarks`. 

There are a few ways to do this. We could do the most straighforward RCAV to finish this by defining a new route like `action="/add_bookmark"`, create a form that will take `type="hidden"` inputs (the two IDs) from our cookies (`session.fetch(:user_id)`) and current movie page ( and `@the_movie.id`), save a new `Bookmark` instance in the action associated with the new route, and redirect the user somewhere. **BENP: at this point you spend awhile showing the basic RCAV steps outlined above, but then a student asks why not use what was pre-built, and you switch to that. I am not transcribing the whole basic RCAV part because it goes unused. The missing transcription is 01:18:10 to 01:23:30** Our form in the end might look something like:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>
    
    <form action="/add_bookmark">
      <input type="hidden" name="the_user_id", value="<%= session.fetch(:user_id) %>">

      <input type="hidden" name="the_movie_id", value="<%= @the_movie.id %>">
      
      <button>Bookmark this movie!</button>
    </form>
  ...
  </div>
</div>
...
```
{: mark_lines="9-10 12"}

And if we wired up the action associated with `"/add_bookmark"` correctly in our routes and controller file, then it should save a bookmark.

But we can use another method here! If we look in our routes, we see there is already an action defined in the bookmarks section that does what we intend:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  ...

  # Routes for the Bookmark resource:

  # CREATE
  post("/insert_bookmark", { :controller => "bookmarks", :action => "create" })

  # READ
  get("/bookmarks", { :controller => "bookmarks", :action => "index" })
  # get("/bookmarks", { :controller => "bookmarks", :action => "user_index" })

  get("/bookmarks/:path_id", { :controller => "bookmarks", :action => "show" })

  # UPDATE

  post("/modify_bookmark/:path_id", { :controller => "bookmarks", :action => "update" })

  # DELETE
  get("/delete_bookmark/:path_id", { :controller => "bookmarks", :action => "destroy" })

  #------------------------------
  ...
end
```
{: mark_lines="9"}

And it even uses the `post()` method to keep the input out of the query string. Let's look at the action that was generated:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  ...
  def create
    the_bookmark = Bookmark.new
    the_bookmark.user_id = params.fetch("query_user_id")
    the_bookmark.movie_id = params.fetch("query_movie_id")

    if the_bookmark.valid?
      the_bookmark.save
      redirect_to("/bookmarks", { :notice => "Bookmark created successfully." })
    else
      redirect_to("/bookmarks", { :alert => the_bookmark.errors.full_messages.to_sentence })
    end
  end
...
end
```

This looks nice, but we just need to be sure that we use *exactly* the same parameter names in our new form and the generated action if we want it to work:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>
    
    <form action="/insert_bookmark" method="post">
      <input type="hidden" name="query_user_id", value="<%= session.fetch(:user_id) %>">

      <input type="hidden" name="query_movie_id", value="<%= @the_movie.id %>">
      
      <button>Bookmark this movie!</button>
    </form>
  ...
  </div>
</div>
...
```
{: mark_lines="9-10 12"}

But there's a problem. If we go to a movie details page as a signed in user and inspect the source code in our browser, the savvy user can manually change the user ID `value` in the `"hidden"` form field!

We can modify our form (remember `session` is available in any action in our app) to eliminate this issue. Let's remove the user ID input from the form:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>
    
    <form action="/insert_bookmark" method="post">
      <input type="hidden" name="query_movie_id", value="<%= @the_movie.id %>">
      
      <button>Bookmark this movie!</button>
    </form>
  ...
  </div>
</div>
...
```
{: mark_lines="9-13"}

And modify our action:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  ...
  def create
    the_bookmark = Bookmark.new
    #the_bookmark.user_id = params.fetch("query_user_id")
    the_bookmark.user_id = session.fetch(:user_id)
    the_bookmark.movie_id = params.fetch("query_movie_id")

    if the_bookmark.valid?
      the_bookmark.save
      redirect_to("/bookmarks", { :notice => "Bookmark created successfully." })
    else
      redirect_to("/bookmarks", { :alert => the_bookmark.errors.full_messages.to_sentence })
    end
  end
...
end
```
{: mark_lines="7-8"}

Now the user can't tamper with the user ID in the form!



### Text Companion: Bookmark

## Video Segment: Un-Bookmark

- Notes:

  - time stamp 01:28:20 to 01:34:42
  - add conditional flow to bookmark action with `Bookmark.where({ :movie_id => @the_movie.id, :user_id => session.fetch(:user_id) })`
  - add `href="/delete_bookmark/<%= the_bookmark.id %>"` link

When we click on "Bookmark this movie!" our app still shows us the button, even if the signed in user already has it bookmarked. What we want, is an "un-bookmark" button, which will destroy the record in our join table `bookmarks`.

Back in our view template for a movie details page, we can add some conditional behavior to get this working. In pseudo-code:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>

    <% if .... %>  
      <form action="/insert_bookmark" method="post">
        <input type="hidden" name="query_movie_id", value="<%= @the_movie.id %>">
        
        <button>Bookmark this movie!</button>
      </form>
    <% else %>
      Un-bookmark
    <% end %>
  ...
  </div>
</div>
...
```
{: mark_lines="9-17"}

What should our condition be? We want to know if the currently signed in user has the current movie bookmarked. We do this by looking in the `bookmarks` table for the record that meets this condition using `.where` and two conditions. This can be done in a chained format:

```ruby
Bookmark.where({ :movie_id => @the_movie.id }).where({ :user_id => session.fetch(:user_id) })
```

or, as two arguments in the hash to filter by multiple columns:

```ruby
Bookmark.where({ :movie_id => @the_movie.id, :user_id => session.fetch(:user_id) })
```

This `.where` will return the bookmark for the current movie if it exists, and we can use that result to decide what button to show the user:

```html
<!--- app/views/movies/show.html.erb --->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>

    <% current_user_bookmarks = Bookmark.where({ :movie_id => @the_movie.id, :user_id => session.fetch(:user_id) }) %>
    <% the_bookmark = current_user_bookmarks.at(0) %>

    <% if the_bookmark == nil %>  
      <form action="/insert_bookmark" method="post">
        <input type="hidden" name="query_movie_id", value="<%= @the_movie.id %>">
        
        <button>Bookmark this movie!</button>
      </form>
    <% else %>
      <a href="/delete_bookmark/<%= the_bookmark.id %>">Un-bookmark</a>
    <% end %>
  ...
  </div>
</div>
...
```
{: mark_lines="9 11-12 19"}

Note that we used the already available delete route generated for us in the `href=""` attribute to the "Un-bookmark" link! We just needed to be sure that we embedded the current bookmark ID number into the second segment of that route.

Try to bookmark and un-bookmark some movies as a signed in user, does everything work as expected? Hopefully so!

The conditional pattern that we put in our view template is a very common pattern. We want to tailor the experience for a user depending on who they are and what they've done in the app.

Let's make a **/git** commit if everything is working.



### Text Companion: Un-Bookmark

## Video Segment: Bookmark Index for Current User

- Notes:

  - time stamp 01:47:22 to 01:51:35
  - conditional flow to application layout for showing bookmarks
  - modify `index` action in `app/controllers/bookmarks_controller.rb`
  - three primary uses of `session.fetch(:user_id)` cookie
  - define association accessor methods in user, bookmark, and movie models

In the target, we want **/bookmarks** to be a personalized list of bookmarks, not all of the bookmarks in the `bookmarks` table as it is now in our app. Let's start on this by altering the layout view template, to make a link to the bookmarks only visible for a signed in user:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <ul>
      ...

      <% if session.fetch(:user_id) == nil %>
        <li>
          <a href="/user_sign_up">Sign up</a>
        </li>
        <li>
          <a href="/user_sign_in">Sign in</a>
        </li>
      <% else %>
        <li>
          <a href="/bookmarks">My bookmarks</a>
        </li>
        <li>
          <a href="/user_sign_out">Sign out</a>
        </li>
      <% end %>
    </ul>

    ...

    <%= yield %>
  </body>
</html>
```
{: mark_lines="21-23"}

Now if the user is signed out, then the link will not be visible to them. You should test this in the app yourself to make sure it worked.

The link is still showing everyone's bookmarks, so let's make the controller filter the table to *only* show the signed in user's bookmarks. That means modifying the `index` action in the controller:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  def index
    matching_bookmarks = Bookmark.where({ :user_id => session.fetch(:user_id) })

    @list_of_bookmarks = matching_bookmarks.order({ :created_at => :desc })

    render({ :template => "bookmarks/index.html.erb" })
  end
  ...
end
```
{: mark_lines="5"}

Now we filter by the `user_id` contained as a cookie in `session`. When we visit the user's bookmark page, it should now only show these records.

**BENP: important point below**

There are three primary things that you will do with the `session.fetch(:user_id)` cookie:

 1. Populating foreign key columns
 1. Conditionally hiding and showing content in the view template
 1. Filtering down queries

We just showed an example of this third option.

Our modification to the action is working, but it would be nicer if we could just write `matching_bookmarks = current_user.bookmarks` rather than `matching_bookmarks = Bookmark.where({ :user_id => session.fetch(:user_id) })`. We want to avoid writing queries like these all over our app. We want association accessor methods that we can call on `User` objects.

Let's define such an accessor in the `User` model:

```ruby
# app/models/user.rb

...
class User < ApplicationRecord
  validates :email, :uniqueness => { :case_sensitive => false }
  validates :email, :presence => true
  has_secure_password

  has_many :bookmarks
  has_many :movies, :through => :bookmarks
end
```
{: mark_lines="9-10"}

The second method `movies` that we defined isn't necessary, but we might as well add it in case we need it later. While we're at it, you should also be sure your association accessor methods have been defined in the `Bookmark` model:

```ruby
# app/models/bookmark.rb

...
class Bookmark < ApplicationRecord
  belongs_to :user
  belongs_to :movie
end
```
{: mark_lines="5-6"}

And we can also add the bookmark associations to the `Movie` model:

```ruby
# app/models/movie.rb

...
class Movie < ApplicationRecord
  validates :title, :presence => true

  belongs_to :director
  has_many :characters

  has_many :cast, :through => :characters, :source => :actor

  has_many :bookmarks, 
  has_many :bookmarkers, :through => :bookmarks, :source => :user
end
```
{: mark_lines="12-13"}

With our association accessor methods sorted, we can return to our bookmarks controller and modify the `index` action:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  def index
    # matching_bookmarks = Bookmark.where({ :user_id => session.fetch(:user_id) })

    @current_user = User.where({ :id => session[:user_id] }).at(0)
    matching_bookmarks = @current_user.bookmarks

    @list_of_bookmarks = matching_bookmarks.order({ :created_at => :desc })

    render({ :template => "bookmarks/index.html.erb" })
  end
  ...
end
```
{: mark_lines="5 7-8"}

Now if you revist the user's bookmark page, everything should still work as before, but we've made the code more robust with our accessors.



### Text Companion: Bookmark Index for Current User

## Video Segment: `@current_user`

- Notes:

  - time stamp 01:51:35 to 02:00:20
  - add `load_current_user` action to `app/controllers/bookmarks_controller.rb` to get `@current_user`
  - use `before_action(:load_current_user)` in `app/controllers/application_controller.rb` to get `@current_user` everywhere
  - apply `@current_user.bookmarks` in bookmarks `index` action

If you are building an app with accounts and authentication, almost every page is going to be somehow tailored to the current user. As a small example, the top of the bookmarks page shouldn't say "List of all bookmarks", but rather "[CURRENT USER]'s bookmarks". 

We would like an instance of `User` we can use all over our app (called `@current_user`) without needing to constantly use the `session` cookie to filter the `users` table. One way of doing this would be to put something like `@current_user = User.where({ :id => session[:user_id] }).at(0)` at the top of *every* action in our app. Pretty annoying!

There's another way to get this variable available in all of our actions and view templates:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  def load_current_user
    @current_user = User.where({ :id => session[:user_id] }).at(0)
  end

  def index
    # matching_bookmarks = Bookmark.where({ :user_id => session.fetch(:user_id) })

    # @current_user = User.where({ :id => session[:user_id] }).at(0)
    self.load_current_user

    matching_bookmarks = @current_user.bookmarks

    @list_of_bookmarks = matching_bookmarks.order({ :created_at => :desc })

    render({ :template => "bookmarks/index.html.erb" })
  end
  ...
end
```
{: mark_lines="4-6 11-12"}

We defined a new method `load_current_user` that would filter the `users` table and get the `@current_user` variable, and now we just need to call that other instance method from within the `index` action using `self`. This is more concise than querying over and over again, but we would still need to put `self.load_current_user` at the top of every action. Still not great.

But there's yet another way of avoiding this repetition. There's a special feature inherited from `ApplicationController` that allows us to call any instance method before any other action in the controller, `before_action()`:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController

  before_action(:load_current_user)

  def load_current_user
    @current_user = User.where({ :id => session[:user_id] }).at(0)
  end

  def index
    # matching_bookmarks = Bookmark.where({ :user_id => session.fetch(:user_id) })

    # @current_user = User.where({ :id => session[:user_id] }).at(0)
    # self.load_current_user

    matching_bookmarks = @current_user.bookmarks

    @list_of_bookmarks = matching_bookmarks.order({ :created_at => :desc })

    render({ :template => "bookmarks/index.html.erb" })
  end
  ...
end
```
{: mark_lines="5 15"}

All we need to give this is the name of one of the methods we defined. It will automatically call that method before any action is executed. So we no longer need the `self.load_current_user` in our actions. `@current_user` will always be available when we call an action in our controller.

If no one is signed in then `User.where({ :id => session[:user_id] }).at(0)` will return `nil`, and thus `@current_user` will be `nil`. 

This code should really go in *every* controller, not just bookmarks. That would again mean a lot of repetition. But, as usual, there's a shortcut! Since we want this to run in every controller, we can put it in the *parent* controller `ApplicationController` from which every *child* controller inherits:

```ruby
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  before_action(:load_current_user)

  # Uncomment line 5 in this file and line 3 in UserAuthenticationController if you want to force users to sign in before any other actions.
  # before_action(:force_user_sign_in)

  def load_current_user
    the_id = session[:user_id]

    @current_user = User.where({ :id => the_id }).first
  end

  def force_user_sign_in
    if @current_user == nil
      redirect_to("/user_sign_in", { :notice => "You have to sign in first." })
    end
  end

  def homepage
    render(template: "navigation/homepage")
  end
end
```

We did not even need to add any of this code, it was already there! Because the `draft:account` generator added it for us. Nice. So `@current_user` has been available to us this whole time.

As an example usage, what if in the navbar we wanted the user's first name in the link to their bookmarks? We can easily write:

```html
<!--- app/views/layouts/application.html.erb --->

<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    <ul>
      ...

      <!-- <% if session.fetch(:user_id) == nil %> -->
      <% if @current_user == nil %>
        <li>
          <a href="/user_sign_up">Sign up</a>
        </li>
        <li>
          <a href="/user_sign_in">Sign in</a>
        </li>
      <% else %>
        <li>
          <a href="/bookmarks"><%= @current_user.first_name %> bookmarks</a>
        </li>
        <li>
          <a href="/user_sign_out">Sign out</a>
        </li>
      <% end %>
    </ul>

    ...

    <%= yield %>
  </body>
</html>
```
{: mark_lines="13-14 23"}

We also removed the `session.fetch(:user_id)` and replaced it with simply `@current_user`. We don't really need to use `session.fetch(:user_id)` anywhere other than the `ApplicationController` file now.

And back in our bookmarks controller, we don't need the code we had built up anymore, so we can clean it up:

```ruby
# app/controllers/bookmarks_controller.rb

class BookmarksController < ApplicationController
  def index
    matching_bookmarks = @current_user.bookmarks

    @list_of_bookmarks = matching_bookmarks.order({ :created_at => :desc })

    render({ :template => "bookmarks/index.html.erb" })
  end
  ...
end
```
{: mark_lines="5"}

Account authentication and signin is so common and so important to apps, that we usually just use automated generators like here. We rarely mess with that code at all. We want our accounts to be secure, so we trust the community and use available resources (gems!) that everyone else does.



### Text Companion: `@current_user`

## Video Segment: Bookmark Drop-Down Form

- Notes:

  - time stamp 02:00:20 to end
  - create a drop-down form on `app/views/bookmarks/index.html.erb`
  - using `<select name="query_movie_id">` with `<option value="<%= a_movie.id %>">`
  - hiding ID keys from user

The last thing to discuss together is the add a new bookmark form on a user's bookmarks page. In the target, there is a drop-down menu with all of the movies in our database and a button "Bookmark this movie!". In our app, there is a much worse form that involves inputing ID numbers, which we already had to find a way around on the movie details page earlier.

The current form in the view template for the list of bookmarks looks like:

```html
<!--- app/views/bookmarks/index.html.erb --->

...
<div>
  <div>
    <h2>
      Add a new bookmark
    </h2>

    <form action="/insert_bookmark" method="post">
      <div>
        <label for="user_id_box">
          User
        </label>

        <input type="text" id="user_id_box" name="query_user_id">
      </div>

      <div>
        <label for="movie_id_box">
          Movie
        </label>

        <input type="text" id="movie_id_box" name="query_movie_id">
      </div>

      <button>
        Create bookmark
      </button>
    </form>
  </div>
</div>
```

We have `<input>`s for the user to fill in. Well, we already know from our movie details form work that `action="/insert_bookmark"`, is doing the right thing and getting the current user ID, so we can delete the "User" field:

```html
<!--- app/views/bookmarks/index.html.erb --->

...
<div>
  <div>
    <h2>
      Add a new bookmark
    </h2>

    <form action="/insert_bookmark" method="post">

      <div>
        <label for="movie_id_box">
          Movie
        </label>

        <input type="text" id="movie_id_box" name="query_movie_id">
      </div>

      <button>
        Create bookmark
      </button>
    </form>
  </div>
</div>
```
{: mark_lines="11"}

But we still need to enter a valid movie ID. We want a drop-down menu with the movie title instead. We will use some new HTML tags for that:

```html
<!--- app/views/bookmarks/index.html.erb --->

...
<div>
  <div>
    <h2>
      Add a new bookmark
    </h2>

    <form action="/insert_bookmark" method="post">

      <div>
        <label for="movie_id_box">
          Movie
        </label>

        <input type="text" id="movie_id_box" name="query_movie_id">

        <select>
          <% Movie.all.order(:title).each do |a_movie| %>
            <option>
              <%= a_movie.title %>
            </option>
        </select>
      </div>

      <button>
        Create bookmark
      </button>
    </form>
  </div>
</div>
```
{: mark_lines="19-24"}

In a form, `<select></select>` and `<option></option>` is basically the same as an unstructured list `<ul></ul>` and `<li></li>`, but it renders as a drop-down menu rather than a bulleted list of items. 

If you visit the bookmark's page for a user now, then you will see a drop-down menu! But the form still doesn't work and still has a field for movie ID, which we would need to fill in. Let's fix that:

```html
<!--- app/views/bookmarks/index.html.erb --->

...
<div>
  <div>
    <h2>
      Add a new bookmark
    </h2>

    <form action="/insert_bookmark" method="post">

      <div>
        <select name="query_movie_id">
          <% Movie.all.order(:title).each do |a_movie| %>
            <option value="<%= a_movie.id %>">
              <%= a_movie.title %>
            </option>
        </select>
      </div>

      <button>
        Create bookmark
      </button>
    </form>
  </div>
</div>
```
{: mark_lines="11 13 15"}

Now we made sure that our selection from the list went into the `params` hash under the key `query_movie_id`, we got rid of the previous input and label, and we made sure that the `value` for the selected movie was not the title, which is shown, but rather the movie ID, which is hidden from the user. 

*Always hide primary and foreign keys from your users in your view templates*.

Now would be a time for a `rails grade` and a **/git** commit!

**BENP: there is some additional cleanup that seems rather thrown in in the last ~10 minutes. It also leads to writing some more validations. I'm not transcribing that bit. It seemed a bit accidental, and things the students should maybe be solving on their own at this point?**

### Text Companion: Bookmark Drop-Down Form

## Finish and Submit MSM Signin