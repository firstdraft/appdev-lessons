# AD2 Helper Methods Pt 1

**BENP: Document based on descript transcription of AD2 WS 2023 Helper Methods Part 1 Video. Mixed in is the Rails Testing assignment.**

## Introducing the Project 00:00:00 to 00:03:00

Finally, this is a very important project to us: [Helper Methods (Part 1)](https://github.com/appdev-projects/helper-methods). Open the project on Canvas. Once your Gitpod workspace is up, do a `bin/setup` to ensure all the setup is run. 

We're going to close the gap between the code we wrote in AD1 and the code that professional Rails developers write. So the very long and explicit, but easy to understand, raw HTML that we used in our view templates is going to be replaced with very short Ruby methods that we're going to embed into the templats.

That will produce the exact same HTML in the end, but allow us to write a lot less code. It'll be a lot less error prone, and it'll be more security, along with other benefits, all done automatically for us. 

We'll start by making a few syntax changes to make our code more professional and in-line with what you might find in Rails Guides or on StackOverflow. Once we finish those clean-ups, we'll begin our first new task: refactoring our routes using more succinct forms of `get`, `post`, `patch`, `delete`, and, ultimately, `resources`.

After the Gitpod workspace is setup and you have your live app started by running `rails server`, have a look around. It should look familiar. I can add a movie, view the details, edit the record, etc. 

## Testing 

Before we go further, let's get something clear about testing.

We are not writing automated tests for you anymore. I want you to get in the habit of writing your own automated tests. So try it! If you can get it, that's great. If you can't get it, that's okay because there's examples already in the project that you can look at and then copy, paste, and use.

You should at least attempt writing your own tests to try and understand where to put the file for your tests, how to run the tests, etc. It is especially important in this context to have automated tests, because the whole point here is that we're refactoring our AD1 code. We're making it better while keeping the functionality exactly the same, so we want to be sure we don't break anything!

Every time we made changes during the Getting Started lesson, we had to click through everything to check our work. Add a movie, delete a movie, edit a movie, did errors display, did validations pass, etc. Once you get bored of manually testing your app, you'll understand the value of having an automated test suite that you can just run when you're trying to improve a code base without introducing bugs into it.

Read Sections 1, 2, 4, 5, 6, and 7 of the [Rails Guide on Testing](https://guides.RubyonRails.org/testing.html). These are the kinds of tests that we write most frequently.

In the Helper Methods Part 1 project, we have one fully functional web resource, `movies`. Create a test file, `test/system/movie_test.rb`, and take a stab at writing some System tests in it to lock down the current functionality of the application. For example, try adding a test that checks to make sure the URL **/movies** has an `<h1>` element on it. Run your tests with:

```bash
Rails test test/system/movie_test.rb
```

After you’ve spent 20-30 minutes on it, you’re allowed to look at the example specs in `test/system/example_specs.rb`. You can copy-paste some or all of them into your own test file.

As we refactor for the rest of the project, you should run the tests periodically to ensure you didn’t break anything.

## Cleaning up `config/routes.rb` 00:03:00 to 00:09:30

Now let's start to refactor the heck out of this code (with our tests, perhaps) and we're going to be making lots of changes. Therefore, as always, I'm going to have my **/git** interface ready to go so that I can go back if something goes terribly wrong. Consider also jotting down some notes to turn into a TIL blog post.

Let's head over to routes to begin with:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get("/", { :controller => "movies", :action => "index" })

  # Routes for the Movie resource:

  # CREATE
  post("/movies", { :controller => "movies", :action => "create" })
  get("/movies/new", { :controller => "movies", :action => "new" })
          
  # READ
  get("/movies", { :controller => "movies", :action => "index" })
  get("/movies/:id", { :controller => "movies", :action => "show" })
  
  # UPDATE
  patch("/movies/:id", { :controller => "movies", :action => "update" })
  get("/movies/:id/edit", { :controller => "movies", :action => "edit" })
  
  # DELETE
  delete("/movies/:id", { :controller => "movies", :action => "destroy" })

  #------------------------------
end
```

This looks familiar from our getting started lesson. It's basically where we left off. We can see the different HTTP verbs and our RESTfully named routes. But, right away we see there's optional syntaxes that we need to change. 

 - Anywhere you see the old `Hash` syntax (`:symbol` keys with hash rockets `=>`): switch to [the new `Hash` syntax](https://chapters.firstdraft.com/chapters/787#new-hash-syntax).
 - Anywhere you see [optional curly braces around `Hash` arguments](https://chapters.firstdraft.com/chapters/787#curly-braces-around-hash-arguments): remove them.
 - _Optionally_ drop the parentheses around arguments.

The last point is optional since it's not something that I always do. I like the parentheses around arguments to a method to make it clear to me that _these_ are the arguments that go with _this_ method: `method(argument_one, argument_two)`.

Especially if there's an order of operations with multiple method calls on the same line of code. My convention is: if there's no other methods on this line. There's no order of operations concerns. I will leave out the parentheses.

Type those changes out by hand to get some muscle memory!

In the end, our routes should look like:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get "/", controller: "movies", action: "index"

  # CREATE
  post "/movies", controller: "movies", action: "create"
  get "/movies/new", controller: "movies", action: "new"
          
  # READ
  get "/movies", controller: "movies", action: "index"
  get "/movies/:id", controller: "movies", action: "show"
  
  # UPDATE
  patch "/movies/:id", controller: "movies", action: "update"
  get "/movies/:id/edit", controller: "movies", action: "edit"
  
  # DELETE
  delete "/movies/:id", controller: "movies", action: "destroy"

  #------------------------------
end
```

We can actually go farther with this shortening. Rather than saying `get "/movies", controller: "movies", action: "create"` when writing routes, we can replace that whole thing as `get "/movies" => movies#create`. 

All we are doing here is passing a hash argument to the `get` method, and this hash is `{ "/movies" => "movies#create" }` (with the curly braces dropped because it is the last argument to the method).

Remember, the `#` octothorpe symbol is used to indicate an `Object#method`, which, in this example, is `MoviesController#create`. 

Actually, we can go even shorter for the homepage route at the URL path **/**. We can just write: `root movies#index`. `root` is a method provided by Rails to define the "homepage". It doesn't need a URL path, because the homepage is always **/**.

Try to do this refactoring on your own for all of the routes.

In the end you should have:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  root "movies#index"

  # CREATE
  post "/movies" => "movies#create"
  get "/movies/new" => "movies#new"
          
  # READ
  get "/movies" => "movies#index"
  get "/movies/:id" => "movies#show"
  
  # UPDATE
  patch "/movies/:id" => "movies#update"
  get "/movies/:id/edit" => "movies#edit"
  
  # DELETE
  delete "/movies/:id" => "movies#destroy"

  #------------------------------
end
```

Just imagine how much typing it would've saved us if we were doing this from the very beginning! But, as beginners, it would've been very confusing. 

This is going to be the pattern of this lesson. We're going to start writing the very abbreviated versions of everything.That's the kind of code you're going to be reading out in the world.

Click around in the app (or better yet, run some automated tests). Everything should be working exactly as before after this refactoring. This is a perfect time for **/git** commit!

## Route Helper Methods 00:09:30 to 00:23:00

Next, let's talk about a built-in `rake task` that comes with Rails, much like `rails db:migrate` or `rails console`. At the terminal, run `rails routes`:

```bash
gitpod /workspace/helper-methods:(main) $ rails routes
                Prefix  Verb   URI Pattern                         Controller#Action
                  root  GET    /                                   movies#index
                movies  POST   /movies(.:format)                   movies#create
            movies_new  GET    /movies/new(.:format)               movies#new
                        GET    /movies(.:format)                   movies#index
                        GET    /movies/:id(.:format)               movies#show
                        PATCH  /movies/:id(.:format)               movies#update
                        GET    /movies/:id/edit(.:format)          movies#edit
                        DELETE /movies/:id(.:format)               movies#destroy
```

There's a whole bunch in here. You may need to make your terminal wider to prevent line wrapping, since it's trying to print a big table with the columns `Prefix`, `Verb`, `URI Pattern`, and `Controller#Action`. We just want to focus on the top of the table.

What do those column names mean to you? Do the values in each row make sense? 

Hopefully they do now! We have our different HTTP verbs, the paths we defined in our routes, and the controller and action related to each route. 

What about the `Prefix`? 

Well, we just saw that Rails comes with the method `root` that always defines the **/** homepage route. `Prefix` means that Rails has defined a method that we can call _anywhere_ in our view templates, controller actions, etc., that will return the path as a string. And look, there's some other methods defined in the `Prefix` column!

You can also view all of this route information in your browser by navigating your live app to **/rails/info/routes**, and you will see a searchable table, with the actual full names (not just the "prefix") of the helper methods (e.g., `root` is actually `root_path`):

![](/assets/rails-info-route.png)

Let's see these route methods in action in one of our view templates. Open `app/views/movies/index.html.erb` and add some embedded Ruby:

```html
<!-- app/views/movies/index.html.erb -->

<h1>
  List of all movies
</h1>

<hr>

<div>
  <%= movies_path %>
</div>
...

```
{: mark_lines="9-11"}

Now refresh the **/movies** page in the live app to see what that embedded Ruby renders. What do you know, it rendered the string `"/movies"`! 

What if we change the code to `<%= movies_new_path %>`? Refresh **/movies** after this change, and it renders `"/movies/new"`. Following this pattern, `<%= root_path %>` just renders `"/"`.

You might be wondering why that matters. Well, the routes we mentioned so far that already have a method assigned to them were automatically assigned by Rails. These were static routes, without dynamic ID numbers in the path, so Rails just puts the segments together and gives you the method. But, for all the rest of the routes that do contain `:id`, there are no methods defined yet. We get to define those methods ourselves!

Back in `config/routes.rb`, what if we add some code to give the movie details page its own method:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  root "movies#index"

  # CREATE
  post "/movies" => "movies#create"
  get "/movies/new" => "movies#new"
          
  # READ
  get "/movies" => "movies#index"
  get "/movies/:id" => "movies#show", as: :details
  
  # UPDATE
  patch "/movies/:id" => "movies#update"
  get "/movies/:id/edit" => "movies#edit"
  
  # DELETE
  delete "/movies/:id" => "movies#destroy"

  #------------------------------
end
```
{: mark_lines="12"}

With the `as:` option, I got to pick a method name (in the form of a symbol). And back on **/rails/info/routes** we see:

![](/assets/rails-info-route-details.png)

And we can check in our `app/views/movies/index.html.erb` view template by changing the embedded Ruby to: `<%= details_path %>`, and on the live app we should see... an error!

```bash
No route matches {:action=>"show", :controller=>"movies"}, missing required keys: {:id}
```

That's because there is a flexible (a.k.a. dynamic) segment in the route, so Rails can't produce the path unless you tell it what to put in that spot!

Cool. So we need to provide an argument. Change the embedded Ruby to `<%= details_path(42) %>`. Refresh **/movies**. It should now render the string `"/movies/42"`.

There's a couple of benefits to these route **helper methods**. 

One, is that there is actually two versions of the method, `_path` and `_url`. If you change the method in the view template to `details_url(42)` and refresh **/movies**, then you will see the full URL of the Gitpod app, including the path! 

This is very cool, because it means I can use fully qualified URLs. And when I deploy my code to my Heroku app, and it's running on mydomain.com, this method will automatically work -- no matter what server it's running on! No need to hard code anything, and then later need to change it when I move my app around.

The biggest benefit of using the route helper methods is the following. If you name your routes once in your `config/routes.rb`, and outside of this file in your application, _never_ refer to paths or URLs and only refer to the methods associated with them, then if you ever have to change the URL from `movies` to `films` (or `zebra` or anything!), you don't need to do this throughout your codebase and risk breaking everything.

With our new route helper methods, we're never going to refer to these paths as actual strings anymore. We're always going to refer to them through these method names that we give them. 

Now let's get these names down per the conventions that most Rails developers use:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  root "movies#index"

  # CREATE
  post "/movies" => "movies#create", as: :movies # movies_url and movies_path 
  get "/movies/new" => "movies#new", as: :new_movie # new_movie_url and new_movie_path
          
  # READ
  get "/movies" => "movies#index" # we defined a method for this path 4 lines above
  get "/movies/:id" => "movies#show", as: :movie # movie_url and movie_path
  
  # UPDATE
  patch "/movies/:id" => "movies#update" # we defined a method for this path 4 lines above
  get "/movies/:id/edit" => "movies#edit", as: :edit_movie # edit_movie_url and edit_movie_path
  
  # DELETE
  delete "/movies/:id" => "movies#destroy" # we defined a method for this path 4 lines above

  #------------------------------
end
```
{: mark_lines="7-8 11-12 15-16 19"}

Note that we don't need to define methods twice for paths that already have a method defined. These methods just return a string with the path name, they ignore the HTTP verb, so there's no difference between naming a route helper method for `delete` or `patch` above; both will return `"/movies/ID"`. We defined the method `movie_path` and `movie_url` for all three `get`, `patch`, and `delete` HTTP verbs for this route just by adding it once.

That's it! We've now provided names for all of our routes. Now we want to use these every single place in our application where we are using string paths. Let me go start to take a look at my paths.

There's one I see right away in the `app/views/movies/index.html.erb` we were using to demonstrate the helper methods:

```html
<!-- app/views/movies/index.html.erb -->

...
<div>
  <a href="/movies/new">Add a new movie</a>
</div>
...
```
{: mark_lines="5"}

That should be:

```html
<!-- app/views/movies/index.html.erb -->

...
<div>
  <a href="<%= new_movie_path %>">Add a new movie</a>
</div>
...
```
{: mark_lines="5"}

Refresh **/movies** in the live app. If all went well, there should be no error messages and if you "view source" on the page, you won't see any Ruby, just the string that the method returned: `"/movies/new"`. Same as before!

This is a pattern that should be repeated throughout the day. Use view source constantly to confirm that the handwritten HTML that we did before matches up with the HTML that these helper methods are producing for us. Then we know that we're using them correctly. 

Time for a **/git** commit after all that preparation!

## Cleaning up the Routes 00:23:00 to 00:32:30

Now that we gave names to our routes, we're going to go through and find every reference to a URL anywhere in our application and replace it.

For instance, at the bottom the `<table>` in the `index` view template:

```html
<!-- app/views/movies/index.html.erb -->

...
    <td>
      <%= time_ago_in_words(a_movie.updated_at) %> ago
    </td>

    <td>
      <a href="/movies/<%= a_movie.id %>">
        Show details
      </a>
    </td>
  </tr>
  <% end %>
</table>
```
{: mark_lines="9"}

Should be:

```html
<!-- app/views/movies/index.html.erb -->

...
    <td>
      <%= time_ago_in_words(a_movie.updated_at) %> ago
    </td>

    <td>
      <a href="<%= movie_path(a_movie.id) %>">
        Show details
      </a>
    </td>
  </tr>
  <% end %>
</table>
```
{: mark_lines="9"}

We supply the movie ID as an argument to our new method. And if we try and refresh our live app and click one of the "Show details" links on the **/movies** page, it should work. We can also "view source" and see the HTML we expect in that link location: `"/movies/ID"`. Great!

Now on to the `show` template for the details page, there's three links near the top to change:

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
        <a href="/movies/<%= @the_movie.id %>/edit">
          Edit Movie
        </a>
      </div>

      <div>
        <a href="/movies/<%= @the_movie.id %>" data-method="delete">
          Delete Movie
        </a>
      </div>
    </div>
...
```
{: mark_lines="11 17 23"}

Those index, edit, and delete links should be using the helper methods:

```html
<!-- app/views/movies/show.html.erb -->

<div>
  <div>
    <h1>
      Movie #<%= @the_movie.id %> details
    </h1>

    <div>
      <div>
        <a href="<%= movies_path %>">
          Go back
        </a>
      </div>

      <div>
        <a href="<%= edit_movie_path(@the_movie.id) %>">
          Edit Movie
        </a>
      </div>

      <div>
        <a href="<%= movie_path(@the_movie.id) %>" data-method="delete">
          Delete Movie
        </a>
      </div>
    </div>
...
```
{: mark_lines="11 17 23"}

Again, we supply arguments to the helper methods that need an ID number.

Test those links out manually to be sure everything worked.

And finally on the `new` and `edit` pages, we'll make two changes:

```html
<!-- app/views/movies/new.html.erb -->

<h1>New movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<form action="<%= movies_path %>" method="post">
...
```
{: mark_lines="9"}

```html
<!-- app/views/movies/edit.html.erb -->

<h1>Edit movie</h1>

<% @the_movie.errors.full_messages.each do |message| %>
  <p style="color: red;"><%= message %></p>
<% end %>

<form action="<%= movie_path(@the_movie.id) %>" method="post">
...
```
{: mark_lines="9"}

Now we've seen that there's only one name (`movie_path(id)`) for a single movie resource, and then there's three actions that modify that single movie resource with different HTTP verbs: `post` to show details, `patch` to edit, and `delete` to destroy. 

Now here's something cool. Wherever we wrote:

```ruby
movie_path(@the_movie.id)
```

We can be bit more concice and omit the `.id`:

```ruby
movie_path(@the_movie)
```

If we just give `movie_path` an instance of `ActiveRecord` Rails will figure out the ID number for us by searching that record for the `id` column. Try and go back through the view templates and remove the `.id` for that helper method.

Now we need to clean up the routes in our `app/controllers/movies_controller.rb` file, since we were using them a lot for redirects. For instance, in the `create` action:

```ruby
# app/controllers/movies_controller.rb

class MoviesController < ApplicationController
  ...
  def create
    @the_movie = Movie.new
    @the_movie.title = params.fetch("query_title")
    @the_movie.description = params.fetch("query_description")

    if @the_movie.valid?
      @the_movie.save
      redirect_to(movies_url, { :notice => "Movie created successfully." })
    else
      render template: "movies/new.html.erb"
    end
  end
  ...
```
{: mark_lines="12"}

Wait! Why did we change `"/movies"` in that `redirect_to` after the save to `movies_url`, rather than the `movies_path` we've been using? We have both methods available to us, and technically, we should only use paths on the client facing view templates, whereas. But, when we're sending responses back, we should use the fully qualified URL, including the domain name.

Can you find the other places in the code where we need to change the path to the `_url` helper method? (Hint: look for any `redirect_to`s, and remember `movie_url` takes an argument of the `ActiveRecord` instance with or without the `.id`.) 

While we're at it in the `movies_controller.rb` file, try to go through and change all of the old syntax to our new syntax. For instance, in the `create` action, this:

```ruby
redirect_to(movies_url, { :notice => "Movie created successfully." })
```

Should be:

```ruby
redirect_to movies_url, notice: "Movie created successfully."
```

We won't need to go back and change things like this going forward, because we'll always be writing code from the get go with our new syntax.

Once you've changed all the syntax, and confirmed you didn't break anything by clicking around in the live app or by running some automated tests, do a **/git** commit.

## Shorten Template Names 00:32:30 to

Let's do another thing to make our code more concise and in line with what you'll see professional developers using. Whenever we render a template in our `movies` controller, we were writing out the whole name:

```ruby
# app/controller/movies_controller.rb

  ...
  def new
    @the_movie = Movie.new

    render template: "movies/new.html.erb"
  end
  ...
```
{: mark_lines="7"}

Actually, we don't need the extension, Rails assumes the file is in `.html.erb` format, so we can just write:

```ruby
  def new
    @the_movie = Movie.new

    render template: "movies/new"
  end
```
{: mark_lines="4"}

Also, we don't actually need `template:` because if you pass the `render` method a single string argument, it assumes that is a view template!

```ruby
  def new
    @the_movie = Movie.new

    render "movies/new"
  end
```
{: mark_lines="4"}

Next, if the folder name that the view templates are located inside of, matches the name of the controller, and if the action name matches the name of the template, we can just get rid of the whole string! (And the method!)

```ruby
  def new
    @the_movie = Movie.new
  end
```

Wow! Rails looks at the controller `MoviesController` and assumes the view template is in `app/views/movies`, and then looks at the action `new` and assumes the template is named `new.html.erb`, and then it assumes you want to render that template given that action (which we do).

Try and go through the code in the controller and delete any render statements where the template matches the action name.

One hint, in the `index` action, where we have:

```ruby
  ...
  def index
    ...
      format.html do
        render template: "movies/index.html.erb"
      end
    end
  end
```
{: mark_lines="4-6"}

We can just get rid of that whole loop block:

```ruby
  ...
  def index
    ...
      format.html
    end
  end
```
{: mark_lines="4"}

To just indicate that we support the HTML format with this action.



So with that, we can now get rid of a lot of code in here. We can get rid of this render movies index, which means that we can just get rid of this whole block and just say, we support html. Now just do the [00:34:30] default behavior for html. That means here we can drop movies show because it matches with the index or with the action name.

That means here we already are doing the best that we can because this doesn't match well, we can actually, we can drop this if we. Because the controller name matches, but it doesn't match the action name. So we have to keep the template here. We can drop this [00:35:00] here. We're redirecting. And we're redirecting.

So there's no render statements there. No render statements there. Okay, so now we dropped even more code. Go back and everything still works fine. Show all those renderings are still working perfectly fine. All right, that's a great chunk of refactoring. Let's make a get. And meanwhile, we're going to check out what's next up on our list.

All right, we're going to next look at Link two methods,[00:35:30] 

dropped as many render statements as possible.

Okay. Next we're going to talk about a very, very useful helper method called Link two.

And link two is the first example of a helper method that produces an actual H TML element. And [00:36:00] as you might guess, it produces an A element. So lemme show you how this works. With a simple example, say go to Google, and then you put the URL over here that you want to populate. The A attribute. Then if we take a look at our index, take a look at the view source of this, here's the output, [00:36:30] right?

So this produced, this doesn't seem like very much help right now because it's almost as verbose as just writing out the. H itself. But you'll see that we get tons of benefits out of this. So first of all, let's do this using this. So this is the content for the link that goes here. This is the url. So this J, [00:37:00] that's just the new.

This is just Ruby. So we don't need it within, if I do string, it's going to literally populate that. Well, that's not what we want. Right? We that, that's the whole point of the route Helper methods. They're Ruby. And now we're inside embedded Ruby here. So we're going to call that method. That method will return the string that we want to put right there.

Beautiful. So now we have a nice link and we can get rid of this. And from [00:37:30] now on, our goal is going to be, we are never going to write a raw a element ever again in a age Erb. If we're writing a plain h and l file in the public folder, for example, well sure. Then we don't, we can't embed Ruby, so we have to write a tags.

But within our templates from now on, we're going to attempt to never write a raw a element. Again, there's lots of benefits that I'll describe as we go along [00:38:00] to doing this, but just now keep it in your mind and make it an. If you, if you even come across an A element anywhere in your code from now on, just try to replace it then and there with the equivalent link two version.

All right, let's do that now. So here's one, I'm going to say

link two. And the first argument is the copy, the content for the A element. And the second argument is [00:38:30] where, what should be the at? Now I can delete this. Let me just, I'll leave it in for now, and then we can take a look at the source code and we can see that it produces the same exact output down here.

Then I'm going to delete the old version. All right, so far so good. Now we will cont continue. Well, I'll let you replace the rest, but I want to show you one really cool thing. Here. [00:39:00] Now we have a link to show details. The argument telling it where to go is a route helper. This is where it starts to get really, really, this is where people start to refer the Rails magic.

And it's not magic, it's just you have to know how things are working step by step. But what if, so this method, A url, right? That's it's a route helper. It returns a string that contains url, and [00:39:30] this method expects a U URL as a second argument. And this method, I'm able to give it an active record object as its argument, and then it by default assumes that you're going to use the ID to populate that second segment.

What if

I give the link to method? An active record object where it's expecting a string. [00:40:00] Right? So this link to, it's expecting something like https, www.google.com. It wants a string URL as its second argument, because that's going to become the hf. What if we now just, we're giving it an active, an instance of active record, right?

We're giving it movie. First, how the heck is the Link Two method? It's going to turn [00:40:30] a record from the movie table into a url.

Well, here's what it does secretly, the link two checks and it says,

so.

It tries to takes, it takes his expression, says [00:41:00] this, says what class are you? Then it does a down case. Then it does a plus URL on it, and then it calls that method. So it looks for a named route helper method. That matches the name of this class, because that's the convention. If you have a table called movie, you're going to have routes that are, [00:41:30] as we discussed, you're going to have restful routes that are movies slash id movies slash id slash edit.

You're going to have those restful routes if you have those restful routes, and if you name them conventionally, then you're going to have this helper. . And so if you're doing everything by convention, think about how many things have to go by convention here for all, with all this whole thing to work. But if you're doing everything conventionally now, someday, when it [00:42:00] comes time for you to write a link to the details page of this active record object, you can simply just say, link to show details.

Give it the object itself. and it's just going to go figure out how to put together the URL for the details page of that object, whatever that is.

So refresh and we get [00:42:30] the same thing. Oh, and it's still films because I forgot to, to change that name back. So that's, that's the beauty of it. Like if some new developer on your team joins, they don't need to know what the URLs are named. They can just link to the. And if everything's conventional, it's just going to figure out how to get the URL for the details page from the routes file.

But while I'm here, I should put this back to [00:43:00] movies, but that's, that's exactly the power of it, is that a new developer wouldn't have had to know that. All right, let's go back and take a minute and go to the edit page and the other. And anywhere you see an A element, so pause the video. Anywhere you see an A element, replace it with a link to element and then come back and we'll do the next thing.

