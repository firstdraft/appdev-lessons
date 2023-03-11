# AD2 Getting Started

**BENP: Document based on everything from 45 min on of modified descript transcription of AD2 WS 2023 Day 1 recording.**

## Starting our Workspace 00:45:00 to 00:48:00

The first project for this course is called [AD2: Getting started](https://github.com/appdev-projects/ad2-getting-started). As usual from AD1, we need to open the Gitpod workspace for our project. If you need, refresh yourself on setting up Gitpod workspaces with the [AD1 technical material](https://learn.firstdraft.com/lessons/29). 

Once your workspace is up, do a `bin/setup` to ensure all the setup is run.

In AD1, we used a slimmed down Rails project that didn't include all the out-of-the-box Rails features. We didn't need them, and they slow down the setup process. But, in AD2 we're including more in our projects. Specifically, we'll use the [vanilla-rails](https://github.com/appdev-projects/vanilla-rails) repository. Setup might take a little longer and we're just going to have to to get used to that.

When the `bin/setup` command finishes, do a `bin/server` and check out the app with the app preview in a new tab. 

## `draft:resource` 00:48:00 to 00:57:30

The homepage of the app is just the blank Ruby on Rails welcome page. We can see if there are any routes in our app by checking in on `config/routes.rb`:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```
{: mark_lines=""}

and we'll see that this is actually just an empty app.

We're going to use this empty space to review things, and think about where we're headed. 

As a first step, we have a couple of big references of all the Ruby stuff that we encounted in AD1: [here](https://learn.firstdraft.com/lessons/33) and [here](https://learn.firstdraft.com/lessons/34). You may want to scan through these and make sure that it mostly makes sense to you.

Feel good about basic Ruby methods, syntax, etc.? Good, then the first thing we want to do in our blank app is generate a resource, examine that code, and make sure that we feel pretty good about what's happening when we invoke `draft:resource`.

This command essentially represents the culmination of what we learned in AD1:

```bash
rails generate draft:resource movie title:string description:text released:boolean
```

Copy this command and run it in a terminal tab.

Uhoh. RTEM!

```bash
Running via Spring preloader in process 1045
Could not find generator 'draft:resource'. 
Run `bin/rails generate --help` for more options.
```

Why couldn't Rails find the generator? That's because _we_ wrote the `draft:resource` generator and it doesn't come with Rails out of the box!

We wrote it in order to make it easier to learn in AD1. But, moving forward, I don't want you to use the `draft:resource` generator anymore. We're going to learn more powerful generators that come with Rails. _So this is the last time where I'm going to generate one of these._

Because we aren't going to be using this generator anymore, we didn't include it in the [base app that you cloned](https://github.com/appdev-projects/vanilla-rails). That means we're going to have to actually pull that generator in ourselves.

Let's head over to our `Gemfile`, which is located in the root folder, and pull in the `draft_generator` gem:

```ruby
# Gemfile

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '3.0.3'

gem "draft_generators", :github => "firstdraft/draft_generators"

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails', branch: 'main'
...
```
{: mark_lines="8"}

Note that we also needed to include the Github repository path where the gem can be found. 

Now, back in a terminal tab, run 

```bash
bundle install
``` 

(Or just `bundle` for short.) 

This command will go get all the gems from our `Gemfile` and install them. And that's how we add gems. TIL!

Again, ideally this is the last time we're going to use the `draft:resource` generator, so try to avoid doing this in the future. I know it's tempting because we're very comfortable with the draft generators, but we want to try and force ourselves to level up now.

Now try again the command:

```bash
rails generate draft:resource movie title:string description:text released:boolean
```

And this time it ought to work, since we pulled in that gem from GitHub:

```bash
Running via Spring preloader in process 1372
      create  app/controllers/movies_controller.rb
      invoke  active_record
      create    db/migrate/20230310220332_create_movies.rb
      create    app/models/movie.rb
      invoke    test_unit
      create      test/models/movie_test.rb
      create      test/fixtures/movies.yml
      create  app/views/movies
      create  app/views/movies/index.html.erb
      create  app/views/movies/show.html.erb
       route  RESTful routes
      insert  config/routes.rb
```

Let's go check out some of these files that were created, starting back with our `routes.rb`: 

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

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```
{: mark_lines=""}

And we check this out in our live app preview by visiting one of the URLs, like **/movies**.

But wait! Another error! RTEM: `Mirgrations are pending... run rails db:migrate...`

Of course! I forgot to migrate the new `movies` table to my database. As of Rails 6, there's actually a button on the error message that you can click to run that migration. Or you can always go back to the terminal on Gitpod and run:

```bash
rails db:migrate
```

Now, back on **/movies**, we see the `index` action page, where there is a form to add things to the table in our database.

Try to add one. What happens? An error we haven't encountered before: `ActionController::InvalideAuthenticityToken`.

## Reviewing RCAV 00:57:30 to 01:00:00

Before we solve this new error, let's shake off some rust. What's even happening on the **/movies** page in this form?

The generator wrote these routes for us, and we're trying to visit one of them: 

```ruby
# config/routes.rb

Rails.application.routes.draw do
  # Routes for the Movie resource:

  # CREATE
  post("/insert_movie", { :controller => "movies", :action => "create" })
          
  # READ
  get("/movies", { :controller => "movies", :action => "index" })
  
  ...

end
```
{: mark_lines="10"}

Our app is running on the live server, so when we try to visit the **/movies** path, the `get("/movies"...)` method says: let me go to the `MoviesController` and find the method (a.k.a., `:action`) called `index`:

```ruby
# app/controllers/movies_controller.rb

class MoviesController < ApplicationController
  def index
    matching_movies = Movie.all

    @list_of_movies = matching_movies.order({ :created_at => :desc })

    render({ :template => "movies/index.html.erb" })
  end

  ...

end
```
{: mark_lines="4 10"}

Rails then runs that `index` method. Remember, all of these files were generated for us by our `draft:resources` command.

`Movie` is the model (find it in `app/models/movie.rb`) that we use to interact with our `movies` table. That's why we can call the `.all` instance method on `Movies` in the first line of the `index` action. Then we `.order` the movies by their `created_at` field, and render the instance variable `@list_of_movies` with a `.each` loop in our view:

```html
<!-- app/views/movies/index.html.erb -->

<div>
  <div>
    <h1>
      List of all movies
    </h1>
  </div>
</div>

...

      <% @list_of_movies.each do |a_movie| %>
      <tr>
        <td>
          <%= a_movie.id %>
        </td>

...

```
{: mark_lines="13"}

Remember, this is an embedded Ruby `.html.erb` file, so we can use the tags `<% %>` for hidden Ruby and `<%= %>` to render things on the page.

Our `movies` table is empty right now, so there is nothing rendered on the **/movies** page (we are `.each` looping on an empty array). But, once we add some movies, that will create a table row per movie in the form on our view page, and that's not working right now.

## HTTP POST Authenticity 01:00:00 to 01:12:30

Now that we've reviewed some RCAV, let's have a look at that form on top of the **/movies** view template:

```html
<!-- app/views/movies/index.html.erb -->

...

    <form action="/insert_movie" method="post">

        ...

    </form>

...

```
{: mark_lines="5"}

The `action` for this form is visiting the **/insert_movie** URL, which we can find in our routes:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  # Routes for the Movie resource:

  # CREATE
  post("/insert_movie", { :controller => "movies", :action => "create" })
...
```
{: mark_lines="7"}

It's using a `method` of `post`, which is the key part here. This is something we learned towards the end of AD1. 

There's a few different HTTP verbs. In AD1, we started out by using GET for everything. Then we evolved to using POST when we were adding or updating records, or deleting records sometimes. If we wanted to do something like a file upload, or if we have some sensitive information like passwords, we don't want to use GET, because it'll put the password right in the query string and the URL. Meaning it'll be visible to anyone!

On the other hand, POST puts all of the inputs into a different part of the request so that they're not visible. You can have file uploads, passwords, anything you want, and you can have arbitrary length. 

In AD1, we were actually not using POST entirely correctly. We left a security hole! Happily, Rails and tens of thousands of companies that use Rails, have encountered these security holes and performance issues and built solutions for them. It requires a little bit of extra work to use these solutions built into Rails. In AD1, we actually disabled them all to make it simpler to get something up and running. But now, in AD2, we've re-enabled all of those default protections. 

**Here's what's going on here:** When I submitted the form, it did a POST to `"/insert_movie"`. Now that we are using POST for our update and create actions to _modify our database_, Rails is going to expect that POST to come along with a password. That guarantees that the form was created by us and not by a malicious third party.

If we just blindly accepted that HTTP request, somebody could put this form on their own website, but have it point to _our_ website (e.g., by replacing the `<form>` `action` attribute with: `action="https://our-app-domain.com/insert_moview`). Then they would be able to modify our database!

That's called **cross-site request forgery**. It was a really common attack that happened a lot in the early 2000s until frameworks like Rails started building in protections against it.

What's the solution? In the form, we're going to put a hidden input that has a "password", and Rails is going to randomly generate a password every time we draw this form:

```html
<!-- app/views/movies/index.html.erb -->

...

    <form action="/insert_movie" method="post">
        <input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
        ...

    </form>

...

```
{: mark_lines="6"}

Let's break down what we did. We added a new form `<input>` with some attributes. First, we set the `type="hidden"`, so the input is not displayed to the user. Then we gave the input a `name="authenticity_token`. Finally, we fill it in with a `value`, which is a rendered Ruby method `<%= form_authenticity_token %>`.

The method `form_authenticity_token` is known as a **helper method** and it comes with Rails out of the box. This is the method that uses cryptography to generate and return a long string token that acts as our "password" for Rails to check and make sure the request is from _us_ and not an outside source. The string is scrambled going into and out of Rails, so even if someone did an "Inspect" on the browser view of our page, the token would not be useful for getting into our database.

We need this token in our `params` hash, so we gave it a name. `authenticity_token` is the name in the `params` that Rails will automatically look for to extract the token, so we had no choice but to name it so.

With this one-line addition to the form code, try and re-submit a new movie on the **/movies** page.

Boom. Error message begone. All of a sudden we have **CSRF** protection. One of the many things that we would never have thought of building until we got hacked. Rails just has this out of the box so that you can't even _build_ forms without solving this problem first!

Again, we did this all with the **helper method** `form_authenticity_token` that comes with Rails. We actually already saw some other Rails helper methods, for instance, remember `time_ago_in_words`? There's a whole bunch of these helper methods that we need to learn to level up our codebase.

## RESTful Routes 01:12:30 to 01:20:00

Here's another improvement that I want to make to our code. Look at our routes:

```ruby
# config/routes.rb

...
  # CREATE
  post("/insert_movie", { :controller => "movies", :action => "create" })
          
  # READ
  get("/movies", { :controller => "movies", :action => "index" })

  get("/movies/:path_id", { :controller => "movies", :action => "show" })
  
  # UPDATE
  post("/modify_movie/:path_id", { :controller => "movies", :action => "update" })
  
  # DELETE
  get("/delete_movie/:path_id", { :controller => "movies", :action => "destroy" })
...
```
{: mark_lines="5 15"}

During AD1, we started with **/movies** for the `index` page, and for the details of an individual movie (`show`), we did **/movies/ID**, with the dynamic route segment `"/movies/:path_id"`. We expected the ID number to appear and then we showed the details of one thing. Then we added **/insert_movie** as a way to trigger an action that `create`s it when we started.

All of these were originally GET methods (`get` in Ruby on Rails), and we only later evolved the `create` path to a POST (`post` in Ruby on Rails). We named these paths in a way that made it really obvious to us what the intention was. We specifically _chose_ names that revealed our intentions for what action was supposed to trigger on these URL paths.

In the real world, professional developers don't do this! 

The way we name our URLs shouldn't have to include what we're trying to do with the resource. The path should only identify the resource that we're trying to work with (here, `movies`). And then the **HTTP verb** (`get`, `post`, etc.) is supposed to tell us what operation to perform on it.

`get` (GET) indicates reading. So the route:

```ruby
get("/movies", { :controller => "movies", :action => "index" })
```

is good, because our path doesn't say `read movie`, or something like that, it just says `movie`, which is the resource (a.k.a. table in our database) we want to read from. `get` tells us our intention. 

This is a topic that you may have heard of. You might have come across this acronym called REST or REST API or [RESTful API](https://restfulapi.net/resource-naming/).

That term is kind of squishy these days. What it means is: If your routes are RESTful, then they're adhering to the naming convention that most other web developers use. 

That means, *we don't use which CRUD function is being performed in the URL itself, rather the request method should be used to indicate which CRUD function is happening.*

In practice, it's fairly simple. All of our routes are going to start with slash and then the plural version of the table name. So our `# READ` routes are good:

```ruby
# READ
get("/movies", { :controller => "movies", :action => "index" })

get("/movies/:path_id", { :controller => "movies", :action => "show" })
```

But, we need to change the `# CREATE` route, so it doesn't say `"/insert_movie"`:

```ruby
# CREATE
post("/movies", { :controller => "movies", :action => "create" })
```

Now, even though our movie index page with the `index` action and our insert movie page with the `create` action share the same URL path (**/movies**), Rails won't get confused, because they are using different HTTP verbs to specify what type of request is being made (GET / `get` vs. POST / `post`).

We also need to change the `# UPDATE` route: 

```ruby
# UPDATE
patch("/movies/:path_id", { :controller => "movies", :action => "update" })
```

We changed the route name to start with our resource of interest (`"/movies/"`), and we changed the **HTTP verb** to a new method `patch` (a.k.a. PATCH).

And again, even though our movie details page with the `show` action and our update movie page with the `update` action share the same URL path the difference in HTTP verbs will prevent any confusion (GET / `get` vs. PATCH / `patch`)

Similarly, to delete a movie, we're going to use the HTTP verb DELETE (a.k.a. `delete`):

```ruby
# DELETE
delete("/movies/:path_id", { :controller => "movies", :action => "destroy" })
```

Despite all the similar URL paths in our routes (`"/movies/ID"`), none of them will get mixed up because they have different verbs!

We do need to update the URLs now anywhere else they appear in our app. For instance, in the `index` page form, we need to change this:

```html
<form action="/insert_movie" method="post">
```

to this:

```html
<form action="/movies" method="post">
```

And we don't need to worry about confusion, because Rails will look for the route with the matching `method` (here, that's POST, or `post`).

But what if we manually type in **/movies** to the address bar? Which operation will be performed. Well, the browser can _only_ perform GET requests! So that method will be used and the index of movies will be shown.

## No .at for ActiveRecord 01:20:00 to 01:22:30

One quick thing we need to fix. On the **/movies** index page, try to click on the "Show details" link for the movie you added.

We get an error message `undefined method 'at' for #<ActiveRecord:Relation...`, pointing to this line in our `MoviesController`:

```ruby
# app/controllers/movies_controller.rb

class MoviesController < ApplicationController
  ...
  def show
    the_id = params.fetch("path_id")
    
    matching_movies = Movie.where({ :id => the_id })
    
    @the_movie = matching_movies.at(0)
    
    render({ :template => "movies/show.html.erb" })
  end
  ...
```
{: mark_lines="10"}

Back in AD1, I told you all to just think of an `ActiveRecord:Relation` (here the `matching_movies` from our `movies` table, which were accessed a `.where` query on the `Movie` model) like an array, and to use the familiar array methods (like `.at`). But, it's not actually an array! Sorry! In the real world, `.at` is not defined for `ActiveRecord:Relation`, we just added it to make it more familiar for us beginners. From now on, when you have an `ActiveRecord:Relation`, and you're trying to get a single element out of it, you could do square bracket syntax:

```ruby
@the_movie = matching_movies[0]
```

or you could do `.first`:

```ruby
@the_movie = matching_movies.first
```

These methods are shared between arrays and `ActiveRecord:Relation`s. Square brackets are very common on the internet (and in other programming languages), so I recommend getting used to that. 

Try the "Show details" link again after you make this change. Working? Great! Be sure to make this change everywhere else you find a `.at(0)` in your controller.

## DELETE 01:22:30 to 01:25:00

Now, on the details page for a movie is working, try to click "Delete movie". What's the error telling us?

```
No route matches [GET] "/delete_movie/1"
```

Right, we changed that route to be RESTful using the `delete` method, so in our `show.html.erb` view template, we need to change the link:

```html
<!-- app/views/movies/show.html.erb -->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>

    <div>
      <div>
        <a href="/movies">
          Go back
        </a>
      </div>

      <div>
        <a href="/delete_movie/<%= @the_movie.id %>">
          Delete movie
        </a>
      </div>
    </div>
```
{: mark_lines="17"}

to this:

```html
    <a href="/movies/<%= @the_movie.id %>">    
```

Make that change and try to "Delete movie" again. Nothing happens. Because this is _still a GET request_. And if you do `get("/movies/:id"...)`, our routes indicate that this should call the `show` action. So now we have a conflict between the two. How do we fix it?

We need to make this `<a>` link tag submit a DELETE request instead of a GET request. Sadly, we can't just add an attribute to the `<a>` tag `method="delete"`. HTML only has POST and GET, because the people who wrote HTML are different than the committee who wrote HTTP, and they apparently didn't share the memo.

Fortunately though, Rails includes some fanciness that will let us fake this pretty easily. Change the link to:

```html
    <a href="/movies/<%= @the_movie.id %>" data-method="delete">    
```

Now go back and try the "Delete movie" link once more. It worked! (Unless you forgot to change `.at(0)` to `[0]` in the controller.)

With Rails, we can just add this attribute onto a link, and Rails will add some stuff in the background that makes it appear like a DELETE request to our server.

## PATCH 01:25:00

Now let's fix the "Edit movie" form that we use to update a database entry. This form is at the bottom of the `show` page:

```html
<!-- app/views/movies/show.html.erb -->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>

    ...

    <form action="/modify_movie/<%= @the_movie.id %>"  method="post" >
      <div>
        <label for="title_box">
          Title
        </label>

        <input type="text" id="title_box" name="query_title" value="<%= @the_movie.title %>">
      </div>
    ...
```
{: mark_lines="11 18"}

Right away, we know we can switch the `action` to point to the correct URL:

```html
    ...
    <form action="/movies/<%= @the_movie.id %>"  method="post" >
    ...
```

And now we're going to have the same conflict issue that we did with the delete method. We wish we could just change the `method` to `"patch"`, but that's not an option in plain HTML. We also can't just use `data-method="patch"`, similar to how we did it with the delete link.

Well, let's start by adding the authenticity token to our `post` request so it would actually work:

```html
    ...
    <form action="/movies/<%= @the_movie.id %>"  method="post" >
        <input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
    ...
```
{: mark_lines="3"}

Now we need to add the following:

```html
    ...
    <form action="/movies/<%= @the_movie.id %>"  method="post" >
        <input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">

        <input type="hidden" name="_method" value="patch">
    ...
```
{: mark_lines="5"}

Another hack! Once again, this bit of code is just some Rails fanciness to trick the HTTP server into making a PATCH rather than a POST request. We _have_ to name the new hidden input `"_method"` because Rails will be looking for that key in the `params` hash. 

There's no need to memorize this oddity, because soon we'll use some advanced helper methods to generate all of this automatically. 

Now we have RESTful routes for create, read (index and show), update, and delete. CRUD.

We're going to help you get stuck. We now have nice restful rounds. Please go back to Sure.[01:28:30] 

Underscore has no special significance. It's just the name in the PRM slash that Rails is looking for, and if it finds that, then it'll use this value to change the type of the request from a post to a patch when it's looking through Rosta RV for a match. So when I look at it [01:29:00] here in the server, when I did.

Authenticity token when we did that one, we can see that that actually showed up in the PRM slash like our other key value pairs, right? Yeah. The OnCore method one doesn't show up in the PRMs, but that's what changed the request up here from opposed into a patch. The presence of that key value pair [01:29:30] looking for literally Rails is looking in the, in the incoming parameters.

In the in requests. It's looking for a key underscore method. If I had just method that it wouldn't work cuz it'd show up just as a regular but underscore method is supposed to be a way to like make sure it doesn't complete with any actual parameter. Method is like kind a common thing. Somebody might actually make an input method so they just put underscore in front to reduce the probability of somebody accidentally using that key.[01:30:00] 

We use X and image. Uh, so for these two we pretty much always use hidden. I was just doing text so that we had something to look at. But you should use it.

Yeah. Make right now we should keep getting to the point where database, yes, that's it. And edit and everything. Everything should be back to working. So basically the goal is [01:30:30] we've switched our routes to be restful. Yeah. And now we need to make it all work together cause we broke everyth.

So,

[01:31:00] oh,

so we did three things, right? First and foremost, we switched the action to point to our new arrest. Then we have to include this in order to get through [01:31:30] the cross-site request order protection. And then we had to include this to change to kind of fake a patch request because forms don't have the ability to just say, patch, your honor.

So this is how we can make it patch with a patch in.

This is we. So yeah, we, you have to use this name. We don't get to pick Rails is going to look for specifically. [01:32:00] A parameter that has the name underscore method. And if it sees one of those, then it'll interpret. Even though actually the request is a post coming to Rails for routing purposes, Rails is like, okay, because I see this in the pram hash, we're going to interpret it as a patch when we figure out which route it hits.

Yeah. And this is sort of a, it's just best [01:32:30] practices. So we're just learning best practices now. We're becoming pros. So it's time to start using best practices, but it, it is going to pay, it seems like kind of our journey, extra work right now. Trust me. What we get to the end of this sequence, by, by next week, you're going to see that by adhering to all these injections, we're going to be able to do what we did in after one, using like 75 lines code.

It's going to come down to like 10 once we adopt all these con, but then they always compound on each other and let us shorten our code [01:33:00] line. So the, for, uh, all of these changes that we've made, we never had to, um, make, um, like sort of the parallel changes to the label tag. Oh, you're right, actually, um, well, we haven't changed.

So for these two, because they're hidden inputs, we actually didn't even put labels in. Right. Labels are for people to see and for people to click on for accessibility purposes. But since we intend to just hide these anyway, we need them, but the users never see them or know that they. [01:33:30] We don't need labels.

Now we are going to start to modify these as well eventually. And then we're going to have to update the labels to match. Like we're not going to do this today, but generally speaking we just use the name of the value here. So this is all, this is going to be titled, that's going to be titled, and this is going to be title.

We named them all different nata one to help us keep, keep it straight, what matches with what. But in a conventional code base, those are all just going to be the same thing as the column. [01:34:00] So we're going to make all those changes eventually, but not yet. Yeah. Does it matter where in the form put this input Now it doesn't matter.

I mean, generally speaking this is not, not just for these two, but for any inputs, order doesn't matter. But if you happen to have two inputs with the same name, which you shouldn't, that's a bug. But if you do, the last one is the one that will, will actually make it through the frame session. But you should never have two inputs with the same name anyway.

Almost never there's,[01:34:30] 

okay, good. Let's make two more quick changes and then we're going to take a break and then we're going to keep going. So the quick changes are in here we have path id. So this is the name that we chose for this dynamic route segment. And I made this name up path Id just because I wanted an easy way to talk about the fact.

That is something that's going to [01:35:00] appear in the browser address bar or in the request in that spot of the path so that when we see it in the PRM slash we know where it's coming from as opposed to something that's coming to us from a query strip, for example. Now in the real world, the developers just call it idn.

We can call it ID zebra or whatever, as long as we know what it is, then in the controller we use that to fetch it. It's up to us. But I just want to let you know in a real Rails code [01:35:30] base, everybody just calls this id.

So we're going to start to do that again. You have to, you have to remember yourself, that when you, when this is going to go into the PR hash and you need to fetch it, and it's coming from the url, not from the, uh, from the path and not the query string. So let's switch those to id and if it's id, then we're going to go to controller.

Wherever we have [01:36:00] path id, we need to update that to just ideally to match. You can just find and replace if you want to as well,

delete some of this stuff here. Is there a question? Yeah. That's to replace everything. So what I just did here was, uh, I selected the first instance of it. And then I get command D [01:36:30] and I kept, I hold the command and I keep pressing D or it's control D on windows. Then you get a cursor at every spot and then when you type, it repeats everywhere until you click somewhere with your mouse.

You'll have a cursor at all those places. Or you can command shit f or uh, the replace dialogue over here. And then you can find and replace and change things like all across the entire app and all the files. I just, one, if you're going to do this mass finding [01:37:00] replacer even before you do this, find and replace in a single file, usually a good idea to make a gig commit first.

Cuz I then really mess myself up big time by finding, replacing and getting it wrong. And then I'm picking through hundreds of files for the next follows. Okay, cool. So we're going to do that and I think that's good. So as long as you don't have any anymore. At zeros we have dot first or square brackets. We have [01:37:30] IDs.

Our, our, our routes now are done. They're like industrial grade. This is what a proper restful API would look like. Alright, let's pause there. The next thing we're going to do is build pages separately for, uh, add and edit instead of having them on the show page and on the next page. But let's take a break first and.[01:38:00] 

We'll get started again at 7 55.[01:38:30] 

That's

taken, but I'm pretty sure what happens.[01:39:00] 

I think U is, that link is not keep rolling. No, it just.

It just like not the expected[01:39:30] 

somewhere. I'm not sure what it'll actually read out here. You'd have to add like a text what it was doing, but just the expectation, like buttons going to perform

all the websites that I know, or News link, but they, [01:40:00] they probably, they're accessible. They probably just have a button. Like the actual underlying element is that could be true, but I doubt so I, as far as I'm just world Yeah. The world, that world that exists

conform to the world that exists. Right. And I would expect with the prevalence of like, you know, it's an amazing thing to read though, [01:40:30] um, I forget, is in one of, she has you. It's aor incredible

element, but only like you have to use a screen to listen to how, when it's focusing and that experience of even just that one little exercise. I didn't,[01:41:00] 

he already offered me a pretty solid discount for the CSS

to get, but hopefully maybe he'll bundle both of.

Do you know how much I paid? Um, I paid

it's less,[01:41:30] 

which is good.

Okay.

To refresh.[01:42:00] [01:42:30] [01:43:00] 

So[01:43:30] 

filter.

Status duct.[01:44:00] [01:44:30] [01:45:00] 

Let's say they have[01:45:30] [01:46:00] 

for the colors and everything.[01:46:30] 

Oh,

you too.[01:47:00] 

More safe than.[01:47:30] 

But that's awesome. So did you.[01:48:00] 

Also do the same thing,[01:48:30] 

and that just lets me figure out the hard parts and then I just, I don't actually give them.[01:49:00] 

Hopeful you'll be able to go a little bit further in the[01:49:30] 

say, good to see you. Um, so

up until chapter five going, well, the tests make sense

back into it. [01:50:00] Testing.

Okay. But as usual,[01:50:30] 

Yeah, I actually started the, this past week I was thinking about actually. Okay. I was like, oh man. Like yeah.

Yeah. And like you explain like I can figure out the logic.

Movies complicated. I dunno where the logic is coming from. Write yourself.

[01:51:00] Yeah, we're, that's one of the things,

you going to hit the path and go, go bus sellable. Have to

charging. So, okay. And then the other routes are io it's charging through. Oh, I [01:51:30] do that too. . I mean, depending on how much time you try, like I'll be hosting three resources in both and we'll be talking in class a little bit each day about both things. Both

slacks you, you.[01:52:00] [01:52:30] 

Integrated, there's,[01:53:00] 

it would've just after you opened it up for a little bit. The greatest, yeah. Three Wonder Canvas. Yeah,[01:53:30] 

possible should be fine for this. Um, probably an email if there's no,[01:54:00] 

I have a good sign email. What did I get?

You think great on it. Like I didn't think about this. That's the actual Okay. I'm not sure about [01:54:30] your

Oh, yeah, yeah.

Alright, everyone, we're going to get started again. You could get back. To where we were at and I realize now looking at the notes that I totally skipped a step, which was, there's a section here that says the goal [01:55:00] and I wanted to give you a preview of why we're doing all of this cuz I know it seems a little bit arbitrary right now.

Like why do we have to switch the methods and why do we have to use all that? Here's why. So if you copy this command, which is very similar, it's Rails generate. Then there's a name model and columns. But the difference is right here, the name of the generator we choose is Scaffold. This like the model generator and the controller generator are just built into Rails.

Let's take a look and [01:55:30] see what happens with this generator. We're going to it in, run it. And

unlike the `draft:resource` generator, I didn't have to add a gem to get this to run. It's just built in out of the box. It's sticking a while. It's kinda surpris. Kinda wonder whether might workspace shut. I wasn't paying [01:56:00] attention.

Is that hanging for you guys too? I got [01:56:30] it.

Well, if it worked for you, I want you to just take a second and take a, so it's going to say down here all the files that were generated by this, just take a look at. So first of all, if you, if you Rails DB migrate, do the same thing, navigate to slash books, you'll see that you have a fully functional CRUD resource just like before.

Then take a look at Routes nrb, take a look at the books controller, take a look at [01:57:00] the view templates and try and like just compare the code with what we learned how to write Nap dev one.

Um, this wouldn't override anything cause it's different[01:57:30] 

adding a second database.[01:58:00] [01:58:30] [01:59:00] 

All right, so while they're waiting for my gift pod workspace set up, which is taking a long time, what, if any differences are you puzzled by here? Yeah, there are no routes. There's no routes. But you can visit Flash books though, and it works. So the routes do exist. Let me try to do this here, see if it works this time.

Okay, cool. [01:59:30] Migrate and server, and I don't know if you remember, but there's a tool here, kind of like there's slash Gid and slash Rails db. There's another tool called slash Rails info.

My servers running slash Rails slash info. This is the path that you can always visit in development mode, and it lists out all the routes that exist [02:00:00] in Roths dot rb, and you can even search them here and filter them. So here's all the movie related ones, and if I search for a book, there are like slash get to slash books and post to slash books.

Those routes exist somehow and I'm able to visit them, oops. Books, and I can add a book.

It's [02:00:30] created and I can see it and destroy all the usual stuff. So this created a full resource for me. But if I looked around,

There's no, where is the routes? Wait there look,

it added this one line, this help, this method resources. If you give it [02:01:00] the name of the database table that you want to build a front interface around, it writes all seven routes and it writes them restfully week and it does a whole bunch of other stuff that we'll talk about. I know, right? But imagine if, and I one, like what if I introduce this on day two, like, Hey guys, right then, and that's actually how a lot of people learn Rails.

So hopefully this is a little bit easier, but by the time we get to this, you have to be able to understand that [02:01:30] it's just wrapping up all of this. And the convention in the community is to name our routes restfully and therefore that helper method generates restfully named routes given the database state, right?

So this is why we're bothering all this. What's that? I guess you'll get to question. Well, what is it? Just if I want to delete one. Right. Okay. So yeah, great point. Like a lot of times we don't want all, all of these rocks, like maybe we don't want people to delete whatever it is. You can [02:02:00] customize this here with a hash and it would be like only, and then you provide an array of the ones that you want.

Or you can say, accept. And exclude the ones that you don't want. Okay? And there's like a ton more power. Like this is where rail starts to shine actually for what we learned, app to have one, we don't actually need Rails. We could have used a much simpler and lighter weight, lighter weight framework. But when you [02:02:30] get to building industrial grade applications, Rails, the, the tens of thousands of companies like GitHub and Airbnb and Twitter who use Rails have come across every single like use case like that.

Like, oh, what if I don't need all seven? I just want six. That has been encountered and solved in the best way that these brilliant lines could think of. And we just get to take advantage of it. So one little example. Okay, so here's the routes. We go to the controllers, books controller, [02:03:00] like look at, look at the edit.

Actually look at some of these actions, like they're so short. Where's all the code? Well, once we adopt the conventional names for our actions, our view templates, our variables, and everything else, all that code that the boiler plate code that we just have to repeat and it, but it's the same for every controller.

The only thing that's changing is the name of the table [02:03:30] Rails will just, if we leave it out, like you can see here, where's the render state? How does it know what template to render? If the template is named the same thing as the action, which we usually do to make it easy for us to find an abuse folder, if the folder is named the same thing as the controller, then you don't have to say, render template books show erb.

First of all, [02:04:00] HTML ERB is a default. So we can leave that out and if this matches this, we can leave that out. And if this matches this, we can leave that out. And Rails will just try that by default before it throws the no template error. If you want to name it something else, then you have to type it all out.

And sometimes we do want to name it something else, but most of the time we don't. And therefore we can stop. We don't have to include the code. It adds cognitive [02:04:30] overhead. So for beginners, they all have no idea what's going on, but once you've built five or six apps, you're sick of typing that over and over.

It's like, okay, get it already. You can just start to leave it out. All right, so there's that and there's a whole bunch of other stuff. This whole, here's an example of where it actually added code that we didn't write. And the reason for that is this generator includes responses for multiple formats besides just H T M L.

So [02:05:00] let's suppose we're ready to add an I format to our app. Our app is taken off and it's time to. iPhone or Android apps on top. Step one is we have to split the front end and the back end and we have to have a J S O API and then our iPhone and Android app will consume the JS O api. Well, in Rails we have a book or two

back [02:05:30] Rails rather. Cool. Now we want to start to add adjacent api. Well, I implicit, whenever we've been visiting a an url, we haven't been including it, but there's a dot html on the end that if you omit Rails, just assumes you're asking for the HTML page cuz that's the most common. But you can now, Rails makes it really easy to add different formats that you respond to.

For [02:06:00] example, if I do do JS O now, so already out of the box with the scaffold generator, there's a JS O API that we can then start to pull from with our iPhone Android app. Now there's a lot more work we have to do to make it really root robust and add authentication and all bunch of other stuff, but at least it's a start.

So that's why in this case it made our code longer, but it's because we have support now [02:06:30] for json. So we'll, we'll talk about that when we get to later. All right, so. This is the point. It might seem like what we're doing for the next week or two is like arbitrary and it's like, okay, we're changing the names of routes that were already working and we're actually making the names look less understandable by changing the, the, the paths.

But the benefit is eventually we'll get to use all these shortcuts and Rails, gets to do a bunch of workforce, which speeds us up, lets us avoid typos and bugs by typing less code. And that's the main [02:07:00] benefit. So good. Okay, so let's get back to it then. One thing that we will see is on the index page of a scaffold, we don't have a form to add a new book.

Instead there's a link here and conventionally the form to add a new record to this table is located at a path that is just slash new after the [02:07:30] name of the resource that we fill it out over here. Similarly, the edit, the edit form doesn't show up right on the details page. Right. I think that's pretty rare for the edit form to be on the details page.

Typically have to click a link to get to another page that has the edit form. Okay, let's do that. We're going to update our movies to be kind of like that. I don't, I want to move this form into its own page. So let's go to, first of all, Rossby [02:08:00] and add.

Get slash movies slash new, and then controller goes to movies. Then let's make an action called let's add a new action called New,

which is the conventional name for that action. And then we have to do the same old things. Think way back, we have to connect Route controller [02:08:30] Action and creative view template. So defined slash new or a method called new

and render a template. Okay, I'm going to, let's pause for one second and I am now going to finally start to stop typing out the longest version of everything. So the way that I always did this after one was parenthesis for the arguments, [02:09:00] then a hash here, and then template here, movies, new H, right? However, we saw that there's a bunch of different styles that you can write.

Movie, this is the most explicit, but we're going to start to adopt some of the more idiomatic ways of doing it. First of all, when we have a hash, the hash is the last argument to a method. We can [02:09:30] drop the curly brackets. Around the hash. Literal the only one. It's the last argument to a method. No other time.

So if we just have a hash out here

like this, you can't just drop the curls out in space. Now it's a syntax error. But when it's the last argument to a method, which en Rails is like all the time, [02:10:00] right? With routes, with dot wear, with render Rails, methods are designed in this way where there's usually a hashes. The last thing that lets you supply a whole bunch of different options.

You can drop the curls or we're going to start doing that. The other thing we're going to start to do is when the key in the hashes a symbol as of Ruby 1.9, they added the ability to move the coal into the end and drop the hash rocket. [02:10:30] When you're typing this out a thousand times, this saves you a lot of trouble.

Sorry guys. Uh, so from now on in class two, I'm just going to start typing in hash literals out this way instead of the long way, and then unwrapping it. The last thing we can do is with methods you are allowed to drop the parentes. [02:11:00] Around the arguments. If there's no order of operations, care issues, my can mention is only when there's one method on the line.

And if the method is just being called without a receiver, so no object dot before it, which basically is render the routing methods like get, when I'm printing stuff with the puts method, I'll drop the parenthesis cuz there's nothing, there's no possible order of operations conflicts there. This is what you're [02:11:30] going to see now.

Like when you go out and start reading blog posts and stack overflow, this is the syntax that you're going to see and you just have to kind of unwind it in your head to put it back into a form that feels more familiar. Okay, so let me now try and visit slash new and we got to the right place and it says missing template.

Let's create that template

and [02:12:00] copy this form. Everything from this page two, line 13 all the way down to the closing form tag. Just copy it over Going to, um, our auto format's not working in this workspace, but we'll fix it. Um, then if I refresh this, we should have this. If I had a movie, does it work? Second [02:12:30] works. We didn't have to do anything else except just copy it over because the action still stays the same and the methods the same.

Everything else is the same. You just put it in its own page

and just test to make sure that it works. Can you check real quick with homework,

any questions on this new form? [02:13:00] If not, try to do the edit as well. I want edit forms to appear at Movies slash ID number slash edit. That's the typical location, so at a route to allow for this, and then on that page, put the edit form.[02:13:30] 

Actually copy the form to create movie, which previously was on the index pamphlet. It just moved it over and it worked. The edit form is not going to work with just copy pasting, but tried to figure out how to make it work.[02:14:00] [02:14:30] 

Um, you're just trying to, this one is just, you're just kind direct to the, to the page itself.[02:15:00] 

Oh,[02:15:30] 

basically.

Okay. Um, yeah, let's go back to their officers. [02:16:00] Um,

yeah, we creating a wheel route for edit. Yep. Okay. Want now [02:16:30] something like this to work? So, oh. Looks like you have a little spin on the, this should display a form to edit whatever.

Syntax. Do we not need to? Yeah, there we,

oh actually, well, okay. Great question. No, [02:17:00] because the purpose of this to just explain the form, it's not actually updating a database record. So we're getting the page that has to pull on Do we have to keep using the rocket or we move that? Yeah, I mean you should actually try to shorten it up so you could drop the front seats, drop the cur symbol, drop the half.

Yeah. [02:17:30] Um, can you go back?

Okay, let's go back to,

so one thing we want do is direct to Yeah. We're do something.[02:18:00] 

No, we want keep that cuz you doing two considered going to separate things. This one is just getting the age that's going to show the report and the other actions going to actually allow us create.[02:18:30] 

The concept,[02:19:00] 

we'll get to it later, but

I'm going to start to step through this. Sorry if you didn't finish yet, but we're running a little short on time, so I want to make sure we get to what you need to for the homework. I think we'll, we'll get to like, alright, so what I want is, rather than edit form being right on the details [02:19:30] page, I'd like to have a separate route that looks like this and the edit page will be there.

So I added a route movie slash id slash edit. Also, let me point out that. This get slash movie slash new. It's higher up in the routes file above get movie slash ID if you put it lower below this. Now these two are in [02:20:00] conflict. They're the same verb and slash new will count as a dynamic passing. So now this route will never be reached.

So watch out for that. If you ever have a static route that matches the same pattern as a dynamic route, make sure that it's above so it doesn't get caught at the dynamic route. Does that make sense? Otherwise, you're going to go to the show action. It's going to look for a movie with the idea of new, and then it's going to crash, saying that doesn't [02:20:30] exist, right?

So let's move this up. And we need now to do movies such ID slash edit. I made the route, let me implement the action goes, copy the new action and change that to edit and then create a new template. I just duplicated the new form

and just to get it working. [02:21:00] I have some stuff in there. Uh, I just duplicated the new page. But of course, I need this to be an edit form, which means this form should be prepopulated. With the details from movie number four so that I can just change whatever I want to change and then update. So I already have an form on the show page, so I could go copy that I'm feeling lazy, look at this, go to my edit page, [02:21:30] paste this in, say update.

And if I try this, I get an error right here because we're trying to call that ID in that form. And this instance rate well at the league doesn't exist in this action. So what we need to do is look up the movie [02:22:00] based on the brands,

just like we did in the show action. I'm just doing it all on online now. And that should then make the form work, I hope, make sure, okay, so now I have this and I think if I update, it should work. It works, the formal works as long as we supply the right instance [02:22:30] variable that that other template was using, that it should.

Does that make sense? What do you think? Yeah, the, when you're fetching from the branch, you can either put the colon in the front or you can use the same name. But quotes is that is one the bird I see fetching here. Yeah. Here I use a symbol. You also see me a lot of times using the string. Yeah. And this is after I harped on you a bunch of times saying those two are not interchangeable.

However, the prams [02:23:00] hash is some special hash Rails. It's not actually a hash, it's a subclass of hash that Rails created. And it is, it's called a hash within different access. And you can use both symbol string. Most of the time you're going to see symbols. Here we use strings in active one because if you look at the perhaps hash of the server lock, everything is actually a string keys and values.

But from now on we'll use symbols here.[02:23:30] 

Okay. Any questions about getting, moving this edit over to its own page? Edit form?

You know, typically you don't have the edit form right On the details page you have to click to get to it. Yep. I uh, if you navigate slash edit now, we should still get an error cause we don't have anything on, we do haves cuz of this, the four. And then in my [02:24:00] route I had that dynamics, the second segment is dynamic.

So that's how that got into the

Okay. One last thing. I'm not sure if we're going to have time for it, but I want to talk about the experience when I fill out the form. But like, [02:24:30] what if somebody submits a movie with a blank title? Typically we don't want to allow that. So let's look at, I'm going to take a quick look at what happens with the scaffold that I generated.

So here's the scaffold that books. Does anybody remember how, what was our tool for preventing somebody from creating a book with the blank title? Validation validations. Validations are this very [02:25:00] excellent, uh, technique. If you need a refresher, there's a chapter number 43 currently on chapters@firstchapter.com.

But basically we can go into the model, we go book model, we're going to add, uh, Valenti dates, and then we say the title or the column that we want to put a rule on. And then, so I'm using the short syntax sound, so [02:25:30] not using the curls around that, moving the column in the end. Not using the parentheses, but with this now the book model will not allow a dot saved unless there's a value in that.

So that means if I try this format right now, it didn't let it, then let it work. And check out the UI here. Error to this book from being saved. Title can't be blank and even highlighted the [02:26:00] input should be cool. So if I add another one here, let's say validates the description, I submit. Now it's like both of them.

If I hire fill one,

that one's good now, but okay, great. That's a great experience. What did we do in act one? So if I can go add these validations to the movie model, [02:26:30] and then if I try to create, just read the code here. In Act one, we sheet a new record. We take columns from the form, sign them to the columns we call in if the movie do valid, which returns true or false based on whether all the validation rules pass or not.

If it is valid, we save. We're redirecting, it's not valid. [02:27:00] We're also redirecting. The only difference is we have different notice on an alert here. So that means right now if I try to go to slash movies and you know, movie slash new, I should give myself a link to make my life a lot easier. Go here, the link to movie slash note just cause I don't want to keep typing that over and over.[02:27:30] 

And then if I leave it til both blank and I click on create, it didn't create, that's good, but it just redirected to the next page. And I don't actually know what happened here. Now we did set an alert, but we don't, we haven't displayed in this application, we didn't do anything with the notice in the alert.

Again, typically what we do is we go to the application layout file because we want those alert notice and alert to show up [02:28:00] on every page if you get redirected to that page with the notice and alert. So we would add this comment that notice an alert, some kind markup so that I try

submitted

okay. At least the value there in the alert [02:28:30] because, We used this errors dot messages dot two sentence to transform the validation failures into like a human readable blurb of text. Alright, so there's a lot of stuff there. Do you remember notice and redirects and notices? Do you remember the dot errors collection that we had on the object after we got saying that it didn't work?

Errors tell us which validations failed and then we're taking the full messages strings, [02:29:00] joining them together and display the what questions?

Adding a new book. It looked like there was bootstraps added to it and there was like, uh, it looked like a . Yeah, the css. It wasn't just a standard like times new Roman ui, right? One of the things that was generated when we did the scaffold generator was in the app style asset style sheets. [02:29:30] There's a scaffolded stop css, which has some very basic styles in there.

Now I don't love these. Usually I delete this file, but it's something to get started with. It's not actually bootstrap, it's just this very basic style sheet here. It's not very long. It's like 60 lines. Okay. So yeah, we will add bootstrap eventually. All right, so this is, this is all right. But that other, that other one, that other experience.[02:30:00] 

With books. It's so much better cuz like we come back to the same form when I fill it, when I fill out the form partially correct and then submit it. At least the part that I got right stays put as opposed to like wiping it all out and I have to fill it all out again. What if there was 30, 30 columns in this?

That would be terrible to have to do. I mean, even if it tells us when we're wrong, I don't want to [02:30:30] fill out all 30 again just to fix one of 'em. Okay? So we can dramatically improve the experience of submitting this one. Here's how it goes. This is, this is a lot of dots to connect here, but it's worth it and we're going to do it for every form from that one.

So let's figure this out. First of all, when if the movie is not valid, so here we don't want to redirect to slash movies. We should at least some slightly better [02:31:00] would be to redirect back to the page that has the form on it, right? Movie slash new. So now at least if I fail to build this out, I bring it back to the form with like a helpful message being displayed in the alert.

That's a little bit better. That's like a nice thing to do. But if I type something in one but not the other. So if I fix one of these issues, It takes me back. It tells me what the issue is now, but it wiped down the form cuz we're just rendering the whole thing from [02:31:30] scratch again. Okay. Had anybody tried to invent a solution to this problem?

So instead of wiping out all the values, I would like to show the form that has all the stuff that they just tried prepopulated and then they just have to modify one thing rather than filling out all the appeals again. What do you think? Any ideas? Yeah, [02:32:00] the values and just reapply it. Ooh, interesting.

That's great idea. So we could store all the values in a cookie.

I like that. So we could do cookies and then we can store the key and title and take this,

you don't have to type this because I'm going to show you another way in a second, but [02:32:30] I do like this, so let's make it work, right? So we're going to store all three values in the cookies, and then how would I make it sharp in the page? So let's just prove that this works. I'm going to open up my dev tools. Go get my application tab so I can look at the cookies right there.[02:33:00] 

And when I fill out this form right now, say whatever create, if it worked, didn't work, is missing with the phone because of the the checkbox. This is always annoying. I'm going to comment this time. Check boxes are always tricky. Okay, so I submitted that and now there's the description and there's the title right there.

So the values that they typed in into the form [02:33:30] are stored in the cookies. Now I have them in the cookie sash. How can I make them appear here in the input? How do I pre-populate inputs? It's attribute form. It's an attribute in the form. That's right. So I go back to my new, and then here, here's the input for title.

Remember to pre-populate, we use the value attribute just like we did up here. [02:34:00] And I'm going to use the cookie sash and get the value.

And I can do the same thing before description

now. Oh, that.

Great text area, you don't need the value because it's just the content of the element for the text area. Great. So I've got [02:34:30] this. If I change this and go a description down here, all goes well. Course. Nice. That's a good solution.

I, I've never had that suggested before. I like that. I kind of actually almost like this better than the solution that I'm going to show you. Uh, but let me show you another solution here. [02:35:00] The solution that I'm going to show you is

this variable, this movie, when I do do save, and the validations failed, as we see here, this object gains an array, which has all the things that went wrong in it. And this object already has [02:35:30] the values that the user typed. We already stored those values in the attributes of this new object that we just instantiated.

So actually, this thing has all the information that we need to draw the helpful form. However, when we redirect to a new page, redirect is the same as the user just typing the same into their address bar and we don't [02:36:00] have access to any, anything from this action. So to hold to our cap starting from the top.

And we only have, once we, once we route the user go through the routing process again, we end up, up here and we only have any instance variables or whatever is set up over here. So that means that object from the create action that had the error messages and had all the values that they typed, we don't have it up in the new action.

So I'm going to say, you know what? [02:36:30] I think rather than redirecting, I'm going to render. So I'm going to, I'm going to turn this into an instance variable.

So this is now an instance variable and I'm going to render a template just like we used to. So let's render template and then say with errors[02:37:00] 

leaving out at that hrv, because if I do Rails, we'll just assume that as the default. Okay? So I'm rendering a template, I'm going to. Call it with errors, HWB. Now, in this template I have access to instant strangles.

And so now let's see [02:37:30] what happens. I submit this form, I'm rendering a template that has the movie, it didn't get saved and the idea is still no, it's got the attributes that they typed. And that means since I have this contract, I can also do

errors messages

Ruby added. [02:38:00] So now I'm rendering a template. I've got the movie object with all the information I need to prepopulate the inputs. And I also have the errors collection that I need to draw. Nice sample, hence for the user. So the solution here, even though I love this cookie solution, we're going to comment it out

and we're just going to render a template that's dedicated to showing them the form again, but with a bunch of powerful [02:38:30] stuff. I'm going to copy the form from the new template cuz it's basically the same.

And here. Instead of cookies title, we're going to use the movie title

here. We'll use movie description and we'll deal with that checkbox in a second.[02:39:00] 

Try to, we'll submit it and kind works. So lemme try this and shape into a title create. So it's rendering the form, it's displaying the previously filled out attributes. Let me also add something at the top that will display the error messages at the [02:39:30] movie, errors

messages, that's an array. And then to make it look nice, I'm going to do a each just throw into a list. So for now

it's a little better

sign.[02:40:00] 

Switch that description. Switch that. All right. And then if I actually submit them both, hopefully now it gets happy and it goes to the other branch where it just gets added. I try adding it again. This is showing up because of the cookie, so I should delete that cookie. It's kinda confusing right now.

Method that we did.[02:40:30] 

Okay, so cool. Uh, let's think about this. We changed this branch, the SAT branch. Instead of redirecting, we're just going to do the normal thing that we do, which is render a template because we're rendering a template from this action. We have, we have access to this variable, which we switched into an instance variable, and with [02:41:00] that, we're able to do whatever we want.

The new template. It's actually, you know, it's, if you think about it, it's the thing that we've been doing forever when it comes to edit forms with an edit form. We already had an object in the database. We looked it up using the id, and then we prepopulated the whole form using value attributes and the object that we looked up out of the database table.

Very similarly here, we're using the object that we attempted to save, but failed to [02:41:30] save to prepopulate. This form here, what do you think? It's a lot of dots to connect. Can you repeat a question? Yeah. Um, I've notice that the

&lt;INAUDIBLE&gt; instead previous study. Yes. Is that addressable or is that It's a great point. That's kind of why I was saying earlier that I liked the Cookies solution, but this is because [02:42:00] the form did a post to slash movies and it was that same action that's rendering this template. Right. So it's a good observation and if there are some disadvantages to it, but we just live with it.

I don't, I don't know anybody who you could, you couldn't change the, your not, but typically we don't bother, like only very tech savvy people would even notice that. So good observation. Usually we just live with it. The benefit is we're on the same action. [02:42:30] So we have the instance variable that has all the info that we need.

Otherwise we'd have to persist it like we did with cookies. So that, that's the way to address it, I guess. Okay. So this is a very good, now here's a little hack that we're going to be using that most Rails app. Use this template that I just created, the Width Arrows template for this specific purpose of reinventing the new form.

[02:43:00] How like this is super similar. To the actual new form, right? Those two templates are almost identical. The difference is there's this errors collection here displaying at the top and there's these value attributes here attempting to prepopulate. Whereas in the new form, of course, those are all just blank.

If you want to be lazy, which Rails developers are, we actually just use the same template. [02:43:30] So I'm going to make this the new temp. I copy pasted it all over it in a new template, and here I'm just going to render the new template from the sad branch of the create action. That way, let's imagine I add a new column to the movies table.

I don't have to go change two forms. I just changed the one form in the new template. So this is nice. Now I try this again, create, [02:44:00] it's working and it's just rendering that one template. I can delete this template if I want to,

and we've just encapsulated that all here. The only issue is let's, if I just go to the top, just navigate to movie slash new. I get an error here. Undefined method errors for Hill cause online five. We're trying to call the errors on. At the movie, but when [02:44:30] I just navigate to movie slash noom for the first time, I'm going to this action.

And there's no instance variable being defined here. This is the danger that you are into Anytime you're reusing the same view template from two different actions, that view template probably depends on some instance variables. And if you're reusing that template, all the actions that are using it have to set up the same instance [02:45:00] variables that it depends upon.

So how do we solve this? While we could just go back and have the two templates that's reasonable, or a hack that Rails developers uses, we just create that. We create the variable that the template wants, just put a blank brand new movie instance in it. We don't try to.save or we don't try to do, or we don't call.save or dot valid, which means the validations don't get run.[02:45:30] 

And that means that when we render this template, now the template is happy because the instance rate exists, we can still call dot errors, but because we never call dot same or dot valid, that errors question is an empty array. So this loop never runs and nothing is displayed. And then down here over pre-populating, we can call dot title and dot description, dot whatever.

It's a valid movie object. [02:46:00] It has those methods, but it's brand new, so it's blank. And so that instance variable satisfies this new template, and when we try to submit it, the same code will work. So this is just a clever hack. We're reusing the same template from these two places, and we kind of massage the template and the action and the, in the names of the instance variables to make it possible to reuse one template from both places.[02:46:30] 

Sometimes you can't get away with that. You just gotta make two different templates. If they, if they diverge sufficiently, just make the two templates and do the two different archives and keep things simple. But for many cases, this works well. What do you think? Can you think of any questions here?

Yeah. Could, could another, uh, method be adding the, the inputs that were [02:47:00] submitted to the query string, and then have the form by default just pull from the query string? Um, the immediate thing that jumps to my mind with that solution, if we just added them all to the query string, is we run into the same problems that caused us to switch to post in the first place, which query strings have a limit on the length.

Hmm. So you can't have arbitrary long content. You can't have file uploads. You don't want sensitive information like passwords, cuz then it'll just be in person's URL when they're filling out the new form. So for [02:47:30] the same reason that we switched to post, I don't love that solution. The cooking solution was nice kind of, but that would also run into the problem of if there's a file load, cookies wouldn't work either.

So yeah. Where is the, where are the values that the user input being held? Like how did it get here? Yeah, so the, the, the flow is, so I'm going to code it slash movies for the first time. It's blank form. [02:48:00] Now, when I fill out one of these and I click create, it goes into the create action, right? So the, the form sends me here with all the info in the pr slash we instantiated a movie and then we assign all the values to the movie object.

That movie Object has values even before we save it, right? Let me show you how this works in the Rails console real [02:48:30] quick.

So if I do em post movie new and then m title equals something, and then if I look at them, that object. We've assigned the attribute to the object, even though we haven't saved it yet, we're getting ready to save it, but I can get it back out, right? So the Ruby object that's stored in M [02:49:00] has those attributes, even though it hasn't been saved into the database yet.

Now, if I try to have not saved, it's like no. And now if I do M errors, full messages, it'll tell me why. But so m, even though it hasn't been saved, it still has all the information on it, including the errors collection. So now, because we turn that into an instance variable here, [02:49:30] like any action, we can render a template and the instance variables are available to us in the In the view, right?

That's how we started doing acad in the first place. Before we got to redirect, we always had a view template and that view template had access to any instance variables defined in the action. Now, in that mute template, we can prepopulate the form and display datas collection with some nice markup around it.

Tricky. Like I said, it doesn't [02:50:00] always work, but when it works, it lets us avoid having a whole other template to display the error page. Alright,

very good. We'll leave it there for today. The last thing maybe we want to do is do the same thing for the update action and make it so that we have a nice errors collection and we, we render a template here, uh, but we don't have time to do that right now. I'll let you kind of chew on that [02:50:30] over during the week.

Uh, the homework, let me make sure I didn't get anything. One second. So we added, added, dedicated, added edit pages. We added a better validation failure, and that's it. Okay, good. So the homework, there's a video where you're going to pick off pretty much where we left off just now. There's two parts to it where you're building up the same project, [02:51:00] the starting point, the wrong canvas,

the starting point here. Okay. First of all, there's a reading where I want you to go through, and I'm sending you to the official Rails guide on testing. I'm just calling out some sections to read. Now it's going to be the first example of many where when you read this, it's going to feel like a [02:51:30] lot, maybe like a little bit over your head.

So don't get too tripped on, tripped up on understanding, feeling like you need to understand every single thing. Just read through it once. Ask questions on Piazza if you have questions, but then move on to the project, and what I want you to do is just take a stab at writing some tests using the information from these sections.

We are not writing automated tests for you anymore. I want you to get in the habit of writing your own automated tests. [02:52:00] So try it. If you can get it, that's great. If you can't get it, that's okay because there's a bunch, there's examples already in the project that you can look at and then copy, paste, and use.

But I just want you to attempt writing your own tests first and like understand where to put the file for your tests, how to run the tests. Then you can use these, and this is an especially important context to have automated tests because the whole point is we're refactoring our AD1 code and making it better [02:52:30] while keeping the functionality exactly the same.

Already today, every time I made a change, I had to like click through everything. I add a movie, delete a movie, edit a movie, click through like five or six things to make sure that I didn't break anything. Once you get bored of manually testing your app, you'll understand the value of having an automated test suite that you could just run when you're trying to improve a code base without introducing bugs into it.

Okay, so first thing to do is read through this. Don't get tripped up. Attempt to write [02:53:00] some of your own tests, but ultimately you can look at the examples that are included in the project already, the project. Is helper methods and the starting the code base that you'll start with is pretty much what we left off today.

There's one video to follow along with, and by the end, you're going to be in position Next time in class, we're going to close the gap between the code that we learned and everything that you saw on the scaffold [02:53:30] generated code. We'll be able to finish that up by next time. Alright, how you feeling? It's a lot of stuff.

This is, this is how it's going to, it's how we roll and have to have two people. Make sure to book a lot of boss hours and talk through anything that seems fuzzy and use Piazza as always. I forgot to mention that on the homepage here, there's a link to piza and a link to a Slack. You we're going to have a slack now, which we didn't have [02:54:00] app to.

One rule of thumb is if it's a quick question that nobody's going to care about tomorrow, ask it on Slack, like something if you missed a URL during class or whatever. Slack is great for that. If it's something that we might refer to in the future, or you might want to refer to in the future, ask it on Piazza so that it has a URL that we can share with each other.

All right, that's it for today. Great to see you all. I'll see you next week.[02:54:30] 