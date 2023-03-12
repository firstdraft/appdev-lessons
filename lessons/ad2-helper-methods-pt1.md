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
                Prefix Verb   URI Pattern                         Controller#Action
                  root  GET    /                                   movies#index
                movies  POST   /movies(.:format)                   movies#create
            movies_new  GET    /movies/new(.:format)               movies#new
                        GET    /movies(.:format)                   movies#index
                        GET    /movies/:id(.:format)               movies#show
                        PATCH  /movies/:id(.:format)               movies#update
                        GET    /movies/:id/edit(.:format)          movies#edit
                        DELETE /movies/:id(.:format)               movies#destroy
```

There's a whole bunch in here. You may need to make your terminal wider to prevent line wrapping, since it's trying to print a big table with the columns `Prefix`, `Verb`, `URI Pattern`, and `Controller#Action`. We just want to foucs on the top of the table.

What do those column names mean to you? Do the values in each row make sense? 

Hopefully they do now! We have our different HTTP verbs, the paths we defined in our routes, and the controller and action related to each route. 

What about the `Prefix`? 

Well, we just saw that Rails comes with the method `root` that always defines the **/** homepage route. `Prefix` means that Rails has defined a method that we can call _anywhere_ in our view templates, controller actions, etc., that will return the URL _with_ the defined HTTP verb. And look, there's some other methods defined in the `Prefix` column!

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

What if we change the code to `<%= movies_new_path %>`? Refresh **/movies** after this change, and it renders `"/movies/new"`. Following this patter, `<%= root_path %>` just renders `"/"`, etc. for the other routes and methods.

You might be wondering why that matters. Well, the routes we mentioned so far that already have a method assigned to them were automatically assigned by Rails. These were static routes, without dynamic ID numbers in the path, so Rails just puts the segments together and gives you the method. But, for all the rest of the routes that do contain `:id`, there's no methods. We get to define those methods ourselves!

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

And we can check in our `app/views/movies/index.html.erb` view template by changing the embedded Ruby to: `<%= details_path %>`, and on the live app we should see... and error!

```bash
No route matches {:action=>"show", :controller=>"movies"}, missing required keys: {:id}
```

That's because there is a flexible (a.k.a. dyanmic) segment in the route, so Rails can't produce the URL unless you tell it what to put in that spot!

Cool. So we need to provide an argument. Change the embedded Ruby to `<%= details_path(42) %>`. Refresh **/movies**. It should now render the string `"/movies/42"`.

There's a couple of benefits to these route **helper methods**. 

One, is that there is actually two versions of the method, `_path` and `_url`. If you change the method in the view template to `details_url(42)` and refresh **/movies**, then you will see the full URL of the Gitpod app, including the path! This is very cool because that means I can use fully qualified URLs if I want to using this method. But then, when I deploy my code to my Heroku app, and it's running on mydomain.com, this method will automatically work -- no matter what server it's running on! No need to **hard code** anything and then later need to change it when I move my app around.

That URL benefit is pretty nice, but we usually use the `_path` version anyway. 

The biggest benefit of using the route helper methods is the following. If you name your routes in your `config/routes.rb` diligently, and outside of this file, everywhere else in your application, _never_ refer to URLs and only refer to the methods associated with them, then if you ever have to change the URL from `movies` to `films` (or `zebra` or anything!), you don't need to do this throughout your codebase and risk breaking everything.

With our new route helper methods, we're never going to refer to these URLs as actual strings anymore. We're always going to refer to them through these names that we give them. 

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

That's it! We've now provided names for all of our routes. Now we want to use these every single place in our application where we are using URLs like this, we're going to replace them. Let me go start to take a look at my URLs.

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

Refresh **/movies** in the live app. If all went well, there should be no error messages and if you view source on the page, you won't see any Ruby, but just the string that the method returned: `"/movies/new"`. Same as before!

This is a pattern that should be repeating throughout the day. Use view source constantly to confirm that the handwritten HTML that we did before matches up with the HTML that these helper methods are producing for us. Then we know that we're using them correctly. 

Time for a **/git** commit after all that preparation!

## Cleaning up the Routes 00:23:00 to 

Gave names to routes and started using them. Now we're going to go through and find every reference to a URL anywhere in our application and replace it. Here's another one here. This is going to the. [00:23:00] Movie show path. So I want to say movie path and it expects the argument of the ID number of a movie. So I've got the movie here, and we'll put the ID number in.

Okay. And that should still work. I'm going to go. Attempt it, click on show and it still works fine. Great. [00:23:30] Next, we'll look at the show template and here's an href. So I want this to be movies path, and this should be edit movie path argument.

Of this [00:24:00] movie ID and this should be Movie Path, again. Movie

Path. The movie id.

Okay. Great. So that's that. And I think we're good on the show page [00:24:30] can edit the movie works, delete the movie works show. And then finally, if I go back and I go to the other two templates, which are new, we have an action here to slash movies, which is just the index route. So it. Movies path, and I think that's it for URLs here on the [00:25:00] edit page, we have movies slash movie id, so this is the same route as again, so as the single movie resource essentially, right?

So we're saying Patch the single movie resource. So this is where Restful Routing comes in. There's only one name for this single movie resource, and there's one name. Plural movie resource. And then there's three actions that modify that single movie resource with different verbs. So movie path, [00:25:30] at the movie.id, and so all goes well if we go to edit this, and then we view source.

it again, just produces that same string for us as we did before with embedding it, but it does it in a much more robust way. Alright, now we can also just check and make sure that works. Cool. Great. All right. [00:26:00] So far so good. Here's something cool. Let's. Take a look at this. So we've got movie slash two here being output by this helper method right now.

And you know, I could put like 53 just to prove to you that we're working on the same, I'm working on that template, but putting the movie.id, I can be a bit more concise here actually. If I omit the.id [00:26:30] from movie path, it will assume. If we just give it an instance of active record and not an instance of integer, the these, all of these route helper methods are pretty smart and they expect that they're going to be used in conjunction with active record objects because we are after all building a Rails application.

So if you give it an instance of active record, it uses the ID attribute, [00:27:00] so you don't have to explicitly peel off that attribute. If you want to use a different a. You're welcome to do so. But if you're using the ID attribute, that is the default and you can just give it to these helper methods. It'll use it by default.

So I can go back and every place I was calling.id here, I can take that off. So that's pretty nice. Um, and then you can do that as well if you want. Take it off here, take it off here. [00:27:30] And that's even more. All right, so now that's pretty much it for Route Helper Methods. They're really cool, very helpful.

Actually, you know what? That's not, that's not cool. That's not in, that's not, uh, all we have to do because we use these, uh, over here. No, not over here. That's the name of a template. That's not a url, but we do use them here in redirects a lot. So we should here do Move [00:28:00] Bees url. This is. Technically speaking, you should use URLs and not pads in, in the view template.

You should use pads that's on the client, on the server. When we're sending, when we're sending responses back, we should use the fully qualified url, including the https s so that's what, that's when the URL helper really comes in handy. All right. This [00:28:30] is going to be. Movie url and the argument is the movie and the.id is implicit.

Similarly here, same thing.

And this is going to be movies url. Oh boy. And we said that whenever we encountered old syntax, we were going to change it. So, [00:29:00] Let's do that now. Whenever we have notice, we're going to say, notice. Whenever we see alert like this, we're going to, I guess, where's the only place we're going to say alert And we're supposed to get rid of all of this situation.

Supposed to get rid of all this situation too[00:29:30] 

and get rid of this.

Lots of refactoring to do here. I should have made a get commit before doing this. Um, this looks good, this, let's make this [00:30:00] consistent.

Let's make this consistent.

Okay, nice and neat. It looks like, [00:30:30] and we've removed all references to URLs. We still have template names in here, which are not URLs, so the, our route helpers can't help us with this. Uh, but. Oh C syntax error line 41. Syntax error. Let's check it out. Uh, yes.

Okay, so [00:31:00] everything looks good. Delete, add. All right, sweet. Let's make a get commit.

And we're now in great shape. We've named our routes. If we need for some reason to change one of those URLs to films, we just change it in our routes dot rb and like maybe just this one. For some reason, [00:31:30] somebody wants to change to films. No problem. Now the rest of our application or the show. At this point, the rest of our application is totally fine.

We're going to go back, show details, and it just adapts automatically. Everything is totally fine now. Great. Let's make a commit. Finished using named route helpers [00:32:00] instead of raw.

All right. Now, as we were doing that refactoring, I saw something that we should talk about. We've got these template names that are very explicit and excellent, but we can shorten these a lot too. Now that we're comfortable with the difference between render Ringa template versus sending people to a url, this is an internal file name within our code [00:32:30] base, somewhere that users.

whereas redirecting to a URL is sending them somewhere on the internet that's public that they see anyways, so we use this kind of extension to make it very obvious and APTA one, that this is an internal thing in our code base with the E R b, but we don't need this Rails assumes if we just say this, that the format is going to be uh, H L E R B template.

If you have some other format J on CSV xm. [00:33:00] Template, then you have to include that extension. But if you omit it, HTML ERB is the assumed extension. Secondly, we can also, if this folder name that the view templates are located inside, matches the name of the controller, and if the action name matches the name of the template, we can just get rid.

[00:33:30] First of all, one thing to note is that you can also, if you're rendering a template without any other options, there are other options that you could potentially pass to this method. But if you're not, you could just give the string directly as the argument to render and omit even more typing. Although I actually don't do that typically, cuz many times I'm going to be passing other options to this method.

But you could just say render like, And then if the folder name matches the controller name [00:34:00] and the template name matches the action name, you can omit the render method altogether, and Rails will assume that that is what you're trying to do. It'll, you're telling it to go to the app views movies folder and look for a template inside called New HTML rb.

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

